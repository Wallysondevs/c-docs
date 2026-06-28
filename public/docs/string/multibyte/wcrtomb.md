# wcrtomb, wcrtomb_s

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
size_t wcrtomb( char *s, wchar_t wc, mbstate_t *ps);  // desde C95
size_t wcrtomb( char *restrict s, wchar_t wc, mbstate_t *restrict ps);  // desde C99
errno_t wcrtomb_s(size_t *restrict retval, char *restrict s, rsize_t ssz,
wchar_t wc, mbstate_t *restrict ps);  // desde C11
```

Converte um caractere largo para sua representação multibyte estreita.

1) Se `s` não for um ponteiro nulo, a função determina o número de bytes necessários para armazenar a representação de caractere multibyte de `wc` (incluindo quaisquer sequências de mudança, e levando em conta o estado de conversão multibyte atual *ps), e armazena a representação de caractere multibyte no array de caracteres cujo primeiro elemento é apontado por `s`, atualizando *ps conforme necessário. No máximo MB_CUR_MAX bytes podem ser escritos por esta função.

Se `s` for um ponteiro nulo, a chamada é equivalente a wcrtomb(buf, L'\0', ps) para algum buffer interno `buf`.

Se wc for o caractere largo nulo L'\0', um byte nulo é armazenado, precedido por qualquer sequência de mudança necessária para restaurar o estado de mudança inicial e o parâmetro de estado de conversão *ps é atualizado para representar o estado de mudança inicial.

Se a macro de ambiente __STDC_ISO_10646__ for definida, os valores do tipo wchar_t são os mesmos que os identificadores curtos dos caracteres no conjunto Unicode requerido (tipicamente codificação UTF-32); caso contrário, é definido pela implementação. Em qualquer caso, a codificação de caracteres multibyte usada por esta função é especificada pela localidade C atualmente ativa.

2) O mesmo que (1), exceto que

se `s` for um ponteiro nulo, a chamada é equivalente a wcrtomb_s(&retval, buf, sizeof buf, L'\0', ps) com variáveis internas `retval` e `buf` (cujo tamanho é maior que MB_CUR_MAX)

o resultado é retornado no parâmetro de saída `retval`

os seguintes erros são detectados em tempo de execução e chamam a função [manipulador de restrição](<#/doc/error/set_constraint_handler_s>) atualmente instalada:

  * `retval` ou `ps` é um ponteiro nulo.
  * `ssz` é zero ou maior que RSIZE_MAX (a menos que `s` seja nulo)
  * `ssz` é menor que o número de bytes que seriam escritos (a menos que `s` seja nulo)
  * `s` é um ponteiro nulo, mas `ssz` não é zero

Assim como todas as funções com verificação de limites, `wcrtomb_s` é garantida para estar disponível apenas se __STDC_LIB_EXT1__ for definida pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir [`<wchar.h>`](<#/doc/string/wide>).

### Parâmetros

- **s** — ponteiro para um array de caracteres estreitos onde o caractere multibyte será armazenado
- **wc** — o caractere largo a ser convertido
- **ps** — ponteiro para o objeto de estado de conversão usado ao interpretar a string multibyte
- **ssz** — número máximo de bytes a serem escritos (o tamanho do buffer `s`)
- **retval** — ponteiro para um parâmetro de saída onde o resultado (número de bytes na string multibyte, incluindo quaisquer sequências de mudança) será armazenado

### Valor de retorno

1) Em caso de sucesso, retorna o número de bytes (incluindo quaisquer sequências de mudança) escritos no array de caracteres cujo primeiro elemento é apontado por `s`.

Em caso de falha (se wc não for um caractere largo válido), retorna ([size_t](<#/doc/types/size_t>))-1, armazena [EILSEQ](<#/doc/error/errno_macros>) em [errno](<#/doc/error/errno>), e deixa *ps em estado não especificado.

2) Retorna zero em caso de sucesso e diferente de zero em caso de falha, nesse caso, s[0] é definido como '\0' (a menos que `s` seja nulo ou `ssz` seja zero ou maior que RSIZE_MAX) e *retval é definido como ([size_t](<#/doc/types/size_t>))-1 (a menos que `retval` seja nulo)

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <locale.h>
    #include <string.h>
    #include <wchar.h>
    #include <stdlib.h>
    
    int main(void)
    {
        setlocale(LC_ALL, "en_US.utf8");
        mbstate_t state;
        memset(&state, 0, sizeof state);
        wchar_t in[] = L"zß水🍌"; // or "z\u00df\u6c34\U0001F34C"
        size_t in_sz = sizeof in / sizeof *in;
    
        printf("Processing %zu wchar_t units: [ ", in_sz);
        for(size_t n = 0; n < in_sz; ++n) printf("%#x ", (unsigned int)in[n]);
        puts("]");
    
        char out[MB_CUR_MAX * in_sz];
        char *p = out;
        for(size_t n = 0; n < in_sz; ++n) {
            int rc = wcrtomb(p, in[n], &state); 
            if(rc == -1) break;
            p += rc;
        }
    
        size_t out_sz = p - out;
        printf("into %zu UTF-8 code units: [ ", out_sz);
        for(size_t x = 0; x < out_sz; ++x) printf("%#x ", +(unsigned char)out[x]);
        puts("]");
    }
```

Saída:
```
    Processing 5 wchar_t units: [ 0x7a 0xdf 0x6c34 0x1f34c 0 ]
    into 11 UTF-8 code units: [ 0x7a 0xc3 0x9f 0xe6 0xb0 0xb4 0xf0 0x9f 0x8d 0x8c 0 ]
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    * 7.29.6.3.3 A função wcrtomb (p: 444)

    * K.3.9.3.1.1 A função wcrtomb_s (p: 647-648)

  * Padrão C99 (ISO/IEC 9899:1999):

    * 7.24.6.3.3 A função wcrtomb (p: 390)

### Veja também

[ wctombwctomb_s](<#/doc/string/multibyte/wctomb>)(C11) | converte um caractere largo para sua representação multibyte
(função)
[ mbrtowc](<#/doc/string/multibyte/mbrtowc>)(C95) | converte o próximo caractere multibyte para caractere largo, dado o estado
(função)
[documentação C++](<#/>) para wcrtomb