# mbrtoc32

Definido no cabeçalho [`<uchar.h>`](<#/doc/string/multibyte>)

```c
size_t mbrtoc32( char32_t restrict * pc32, const char * restrict s,
size_t n, mbstate_t * restrict ps );  // desde C11
```

Converte um único ponto de código de sua representação de caractere multibyte estreito para sua representação de caractere largo de 32 bits de comprimento variável (mas tipicamente, UTF-32).

Se `s` não for um ponteiro nulo, inspeciona no máximo `n` bytes da string de caracteres multibyte, começando com o byte apontado por `s` para determinar o número de bytes necessários para completar o próximo caractere multibyte (incluindo quaisquer sequências de mudança, e levando em conta o estado de conversão multibyte atual *ps). Se a função determinar que o próximo caractere multibyte em `s` está completo e é válido, ela o converte para o caractere largo de 32 bits correspondente e o armazena em *pc32 (se `pc32` não for nulo).

Se o caractere multibyte em `*s` corresponder a uma sequência multi-char32_t (não possível com UTF-32), então, após a primeira chamada a esta função, `*ps` é atualizado de tal forma que as próximas chamadas a `mbrtoc32` escreverão o char32_t adicional, sem considerar `*s`.

Se `s` for um ponteiro nulo, os valores de `n` e `pc32` são ignorados e a chamada é equivalente a mbrtoc32([NULL](<#/doc/types/NULL>), "", 1, ps).

Se o caractere largo produzido for o caractere nulo, o estado de conversão *ps representa o estado de mudança inicial.

Se a macro __STDC_UTF_32__ for definida, a codificação de 32 bits usada por esta função é UTF-32; caso contrário, é definida pela implementação. A macro é sempre definida e a codificação é sempre UTF-32.(desde C23) Em qualquer caso, a codificação de caracteres multibyte usada por esta função é especificada pela localidade C atualmente ativa.

### Parâmetros

- **pc32** — ponteiro para o local onde o caractere largo de 32 bits resultante será escrito
- **s** — ponteiro para a string de caracteres multibyte usada como entrada
- **n** — limite no número de bytes em s que podem ser examinados
- **ps** — ponteiro para o objeto de estado de conversão usado ao interpretar a string multibyte

### Valor de retorno

O primeiro dos seguintes que se aplica:

  * ​0​ se o caractere convertido de `s` (e armazenado em *pc32 se não nulo) foi o caractere nulo
  * o número de bytes [1...n] do caractere multibyte convertido com sucesso de `s`
  * ([size_t](<#/doc/types/size_t>))-3 se o próximo char32_t de um caractere multi-char32_t foi agora escrito em *pc32. Nenhum byte é processado da entrada neste caso.
  * ([size_t](<#/doc/types/size_t>))-2 se os próximos `n` bytes constituem um caractere multibyte incompleto, mas até agora válido. Nada é escrito em *pc32.
  * ([size_t](<#/doc/types/size_t>))-1 se ocorrer um erro de codificação. Nada é escrito em `*pc32`, o valor [EILSEQ](<#/doc/error/errno_macros>) é armazenado em [errno](<#/doc/error/errno>) e o valor de *ps é não especificado.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <locale.h>
    #include <string.h>
    #include <uchar.h>
    #include <assert.h>
    
    int main(void)
    {
        setlocale(LC_ALL, "en_US.utf8");
        char in[] = u8"zß水🍌"; // or "z\u00df\u6c34\U0001F34C"
        const size_t in_size = sizeof in / sizeof *in;
    
        printf("Processing %zu UTF-8 code units: [ ", in_size);
        for (size_t i = 0; i < in_size; ++i)
            printf("0x%02x ", (unsigned char)in[i]);
    
        puts("]");
    
        char32_t out[in_size];
        char32_t *p_out = out;
        char *p_in = in, *end = in + in_size;
        mbstate_t state;
        memset(&state, 0, sizeof(state));
        size_t rc;
        while ((rc = mbrtoc32(p_out, p_in, end - p_in, &state)))
        {
            assert(rc != (size_t)-3); // no surrogate pairs in UTF-32
            if (rc == (size_t)-1) break; // invalid input
            if (rc == (size_t)-2) break; // truncated input
            p_in += rc;
            ++p_out;
        }
    
        size_t out_size = p_out+1 - out;
        printf("into %zu UTF-32 code units: [ ", out_size);
        for (size_t i = 0; i < out_size; ++i)
            printf("0x%08X ", out[i]);
    
        puts("]");
    }
```

Saída:
```
    Processing 11 UTF-8 code units: [ 0x7a 0xc3 0x9f 0xe6 0xb0 0xb4 0xf0 0x9f 0x8d 0x8c 0x00 ]
    into 5 UTF-32 code units: [ 0x0000007A 0x000000DF 0x00006C34 0x0001F34C 0x00000000 ]
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.30.1.5 A função mbrtoc32 (p: 410)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.28.1.3 A função mbrtoc32 (p: 293-294)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.28.1.3 A função mbrtoc32 (p: 400-401)

### Veja também

[ c32rtomb](<#/doc/string/multibyte/c32rtomb>)(C11) | converte um caractere UTF-32 para codificação multibyte estreita
(função)
[Documentação C++](<#/>) para mbrtoc32