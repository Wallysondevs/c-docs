# mbrlen

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
size_t mbrlen( const char* s, size_t n, mbstate_t* ps );  // desde C95
(até C99)  // até C99
size_t mbrlen( const char* restrict s, size_t n, mbstate_t* restrict ps );  // desde C99
```

Determina o tamanho, em bytes, da representação de um caractere multibyte.

Esta função é equivalente à chamada [mbrtowc](<#/doc/string/multibyte/mbrtowc>)([NULL](<#/doc/types/NULL>), s, n, ps ? ps : &internal) para algum objeto oculto internal do tipo [mbstate_t](<#/doc/string/multibyte/mbstate_t>), exceto que a expressão ps é avaliada apenas uma vez.

### Parâmetros

- **s** — ponteiro para um elemento de uma string de caracteres multibyte
- **n** — limite no número de bytes em s que podem ser examinados
- **ps** — ponteiro para a variável que mantém o estado de conversão

### Valor de retorno

O primeiro dos seguintes que se aplica:

* ​0​ se os próximos n ou menos bytes completarem o caractere nulo ou se s for um ponteiro nulo. Ambos os casos redefinem o estado de conversão.
* o número de bytes [1...n] que completam um caractere multibyte válido
* ([size_t](<#/doc/types/size_t>))-2 se os próximos n bytes fizerem parte de um caractere multibyte possivelmente válido, que ainda está incompleto após examinar todos os n bytes
* ([size_t](<#/doc/types/size_t>))-1 se ocorrer um erro de codificação. O valor de [errno](<#/doc/error/errno>) é [EILSEQ](<#/doc/error/errno_macros>); o estado de conversão é não especificado.

### Exemplo

Execute este código
```c
    #include <locale.h>
    #include <stdio.h>
    #include <string.h>
    #include <wchar.h>
    
    int main(void)
    {
        // allow mbrlen() to work with UTF-8 multibyte encoding
        setlocale(LC_ALL, "en_US.utf8");
    
        // UTF-8 narrow multibyte encoding
        const char* str = "水";
        size_t sz = strlen(str);
    
        mbstate_t mb;
        memset(&mb, 0, sizeof mb);
        int len1 = mbrlen(str, 1, &mb);
        if (len1 == -2)
            printf("The first 1 byte of %s is an incomplete multibyte char"
                   " (mbrlen returns -2)\n", str);
    
        int len2 = mbrlen(str + 1, sz - 1, &mb);
        printf("The remaining %zu  bytes of %s hold %d bytes of the multibyte"
               " character\n", sz - 1, str, len2);
    
        printf("Attempting to call mbrlen() in the middle of %s while in initial"
               " shift state returns %zd\n", str, mbrlen(str + 1, sz - 1, &mb));
    }
```

Saída:
```
    The first 1 byte of 水 is an incomplete multibyte char (mbrlen returns -2)
    The remaining 2  bytes of 水 hold 2 bytes of the multibyte character
    Attempting to call mbrlen() in the middle of 水 while in initial shift state returns -1
```

### Referências

* Padrão C23 (ISO/IEC 9899:2024):

* 7.29.6.3.1 A função mbrlen (p: TBD)

* Padrão C17 (ISO/IEC 9899:2018):

* 7.29.6.3.1 A função mbrlen (p: TBD)

* Padrão C11 (ISO/IEC 9899:2011):

* 7.29.6.3.1 A função mbrlen (p: 442)

* Padrão C99 (ISO/IEC 9899:1999):

* 7.24.6.3.1 A função mbrlen (p: 388)

### Veja também

[ mbrtowc](<#/doc/string/multibyte/mbrtowc>)(C95) | converte o próximo caractere multibyte para caractere largo, dado o estado
(função)
[ mblen](<#/doc/string/multibyte/mblen>) | retorna o número de bytes no próximo caractere multibyte
(função)
[Documentação C++](<#/>) para mbrlen