# mbrtowc

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
size_t mbrtowc( wchar_t* pwc, const char* s, size_t n, mbstate_t* ps );  // desde C95
size_t mbrtowc( wchar_t *restrict pwc, const char *restrict s, size_t n,
mbstate_t *restrict ps );  // desde C99
```

Converte um caractere multibyte estreito para sua representação de caractere largo.

Se `s` não for um ponteiro nulo, inspeciona no máximo `n` bytes da string de caracteres multibyte, começando com o byte apontado por `s` para determinar o número de bytes necessários para completar o próximo caractere multibyte (incluindo quaisquer sequências de mudança de estado, e levando em conta o estado de conversão multibyte atual *ps). Se a função determinar que o próximo caractere multibyte em `s` está completo e é válido, ela o converte para o caractere largo correspondente e o armazena em *pwc (se `pwc` não for nulo).

Se `s` for um ponteiro nulo, os valores de `n` e `pwc` são ignorados e a chamada é equivalente a mbrtowc([NULL](<#/doc/types/NULL>), "", 1, ps).

Se o caractere largo produzido for o caractere nulo, o estado de conversão armazenado em *ps é o estado de mudança inicial.

Se a macro de ambiente __STDC_ISO_10646__ for definida, os valores do tipo wchar_t são os mesmos que os identificadores curtos dos caracteres no conjunto Unicode requerido (tipicamente codificação UTF-32); caso contrário, é definido pela implementação. Em qualquer caso, a codificação de caracteres multibyte usada por esta função é especificada pela localidade C atualmente ativa.

### Parâmetros

- **pwc** — ponteiro para o local onde o caractere largo resultante será escrito
- **s** — ponteiro para a string de caracteres multibyte usada como entrada
- **n** — limite no número de bytes em s que podem ser examinados
- **ps** — ponteiro para o estado de conversão usado ao interpretar a string de caracteres multibyte

### Valor de retorno

O primeiro dos seguintes que se aplica:

* ​0​ se o caractere convertido de `s` (e armazenado em pwc se não nulo) for o caractere nulo
* o número de bytes [1...n] do caractere multibyte convertido com sucesso de `s`
* ([size_t](<#/doc/types/size_t>))-2 se os próximos `n` bytes constituírem um caractere multibyte incompleto, mas até agora válido. Nada é escrito em *pwc.
* ([size_t](<#/doc/types/size_t>))-1 se ocorrer um erro de codificação. Nada é escrito em `*pwc`, o valor [EILSEQ](<#/doc/error/errno_macros>) é armazenado em [errno](<#/doc/error/errno>) e o valor de *ps é deixado não especificado.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <locale.h>
    #include <string.h>
    #include <wchar.h>
    
    int main(void)
    {
        setlocale(LC_ALL, "en_US.utf8");
        mbstate_t state;
        memset(&state, 0, sizeof state);
        char in[] = u8"z\u00df\u6c34\U0001F34C"; // or u8"zß水🍌"
        size_t in_sz = sizeof in / sizeof *in;
    
        printf("Processing %zu UTF-8 code units: [ ", in_sz);
        for(size_t n = 0; n < in_sz; ++n) printf("%#x ", (unsigned char)in[n]);
        puts("]");
    
        wchar_t out[in_sz];
        char *p_in = in, *end = in + in_sz;
        wchar_t *p_out = out;
        int rc;
        while((rc = mbrtowc(p_out, p_in, end - p_in, &state)) > 0)
        {
            p_in += rc;
            p_out += 1;
        }
    
        size_t out_sz = p_out - out + 1;
        printf("into %zu wchar_t units: [ ", out_sz);
        for(size_t x = 0; x < out_sz; ++x) printf("%#x ", out[x]);
        puts("]");
    }
```

Saída:
```
    Processing 11 UTF-8 code units: [ 0x7a 0xc3 0x9f 0xe6 0xb0 0xb4 0xf0 0x9f 0x8d 0x8c 0 ]
    into 5 wchar_t units: [ 0x7a 0xdf 0x6c34 0x1f34c 0 ]
```

### Referências

* Padrão C11 (ISO/IEC 9899:2011):

  * 7.29.6.3.2 A função mbrtowc (p: 443)

* Padrão C99 (ISO/IEC 9899:1999):

  * 7.24.6.3.2 A função mbrtowc (p: 389)

### Veja também

[ mbtowc](<#/doc/string/multibyte/mbtowc>) | converte o próximo caractere multibyte para caractere largo
(função)
[ wcrtombwcrtomb_s](<#/doc/string/multibyte/wcrtomb>)(C95)(C11) | converte um caractere largo para sua representação multibyte, dado o estado
(função)
[Documentação C++](<#/>) para mbrtowc