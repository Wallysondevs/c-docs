# mbrtoc16

Definido no cabeçalho [`<uchar.h>`](<#/doc/string/multibyte>)

```c
size_t mbrtoc16( char16_t* restrict pc16, const char* restrict s,
size_t n, mbstate_t* restrict ps );  // desde C11
```

Converte um único ponto de código de sua representação de caractere multibyte estreito para sua representação de caractere largo de 16 bits de comprimento variável (tipicamente, UTF-16).

Se s não for um ponteiro nulo, inspeciona no máximo n bytes da string de caracteres multibyte, começando com o byte apontado por `s` para determinar o número de bytes necessários para completar o próximo caractere multibyte (incluindo quaisquer sequências de mudança de estado, e levando em conta o estado de conversão multibyte atual *ps). Se a função determinar que o próximo caractere multibyte em `s` está completo e é válido, ela o converte para o caractere largo de 16 bits correspondente e o armazena em *pc16 (se pc16 não for nulo).

Se o caractere multibyte em *s corresponder a uma sequência multi-char16_t (por exemplo, um par substituto em UTF-16), então, após a primeira chamada a esta função, *ps é atualizado de tal forma que a próxima chamada a `mbrtoc16` escreverá o char16_t adicional, sem considerar *s.

Se s for um ponteiro nulo, os valores de n e pc16 são ignorados e a chamada é equivalente a mbrtoc16([NULL](<#/doc/types/NULL>), "", 1, ps).

Se o caractere largo produzido for o caractere nulo, o estado de conversão *ps representa o estado de mudança inicial.

Se a macro __STDC_UTF_16__ for definida, a codificação de 16 bits usada por esta função é UTF-16; caso contrário, é definida pela implementação. A macro é sempre definida e a codificação é sempre UTF-16.(desde C23) Em qualquer caso, a codificação de caracteres multibyte usada por esta função é especificada pela localidade C atualmente ativa.

### Parâmetros

- **pc16** — ponteiro para o local onde o caractere largo de 16 bits resultante será escrito
- **s** — ponteiro para a string de caracteres multibyte usada como entrada
- **n** — limite no número de bytes em s que podem ser examinados
- **ps** — ponteiro para o objeto de estado de conversão usado ao interpretar a string multibyte

### Valor de retorno

O primeiro dos seguintes que se aplica:

  * ​0​ se o caractere convertido de s (e armazenado em *pc16 se não nulo) foi o caractere nulo
  * o número de bytes [1...n] do caractere multibyte convertido com sucesso de s
  * ([size_t](<#/doc/types/size_t>))-3 se o próximo char16_t de um caractere multi-char16_t (por exemplo, um par substituto) foi agora escrito em *pc16. Nenhum byte é processado da entrada neste caso.
  * ([size_t](<#/doc/types/size_t>))-2 se os próximos `n` bytes constituem um caractere multibyte incompleto, mas até agora válido. Nada é escrito em *pc16.
  * ([size_t](<#/doc/types/size_t>))-1 se ocorrer um erro de codificação. Nada é escrito em *pc16, o valor [EILSEQ](<#/doc/error/errno_macros>) é armazenado em [errno](<#/doc/error/errno>) e o valor de *ps é não especificado.

### Exemplo

Execute este código
```c
    #include <locale.h>
    #include <stdio.h>
    #include <uchar.h>
    
    mbstate_t state;
    
    int main(void)
    {
        setlocale(LC_ALL, "en_US.utf8");
        const char in[] = u8"zß水🍌"; // or "z\u00df\u6c34\U0001F34C"
        const size_t in_sz = sizeof in / sizeof *in;
    
        printf("Processing %zu UTF-8 code units: [ ", in_sz);
        for (size_t n = 0; n < in_sz; ++n)
            printf("%#x ", (unsigned char)in[n]);
        puts("]");
    
        char16_t out[in_sz];
        const char *p_in = in, *end = in + in_sz;
        char16_t *p_out = out;
        for (size_t rc; (rc = mbrtoc16(p_out, p_in, end - p_in, &state));)
        {
            if (rc == (size_t)-1)     // invalid input
                break;
            else if(rc == (size_t)-2) // truncated input
                break;
            else if(rc == (size_t)-3) // UTF-16 high surrogate
                p_out += 1;
            else
            {
                p_in += rc;
                p_out += 1;
            };
        }
    
        const size_t out_sz = p_out - out + 1;
        printf("into %zu UTF-16 code units: [ ", out_sz);
        for (size_t x = 0; x < out_sz; ++x)
            printf("%#x ", out[x]);
        puts("]");
    }
```

Saída:
```
    Processing 11 UTF-8 code units: [ 0x7a 0xc3 0x9f 0xe6 0xb0 0xb4 0xf0 0x9f 0x8d 0x8c 0 ]
    into 6 UTF-16 code units: [ 0x7a 0xdf 0x6c34 0xd83c 0xdf4c 0 ]
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.30.1.3 A função mbrtoc16 (p: 408-409)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.28.1.1 A função mbrtoc16 (p: 398-399)

### Veja também

[ c16rtomb](<#/doc/string/multibyte/c16rtomb>)(C11) | converte um caractere UTF-16 para codificação multibyte estreita
(função)
[Documentação C++](<#/>) para mbrtoc16