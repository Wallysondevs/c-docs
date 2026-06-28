# mbsinit

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
int mbsinit( const ``mbstate_t`* ps);  // desde C95
```

Se `ps` não for um ponteiro nulo, a função `mbsinit` determina se o objeto `[`mbstate_t`](<#/doc/string/multibyte/mbstate_t>)` apontado descreve o estado de conversão inicial.

### Notas

Embora um `[`mbstate_t`](<#/doc/string/multibyte/mbstate_t>)` inicializado com zero sempre represente o estado de conversão inicial, pode haver outros valores de `[`mbstate_t`](<#/doc/string/multibyte/mbstate_t>)` que também representam o estado de conversão inicial.

### Parâmetros

- **ps** — ponteiro para o objeto mbstate_t a ser examinado

### Valor de retorno

​0​ se `ps` não for um ponteiro nulo e não representar o estado de conversão inicial, um valor diferente de zero caso contrário.

### Exemplo

Execute este código
```c
    #include <locale.h>
    #include <string.h>
    #include <stdio.h>
    #include <wchar.h>
     
    int main(void)
    {
        // allow mbrlen() to work with UTF-8 multibyte encoding
        setlocale(LC_ALL, "en_US.utf8");
        // UTF-8 narrow multibyte encoding
        const char* str = u8"水"; // or u8"\u6c34" or "\xe6\xb0\xb4"
        static mbstate_t mb; // zero-initialize
        (void)mbrlen(&str[0], 1, &mb);
        if (!mbsinit(&mb)) {
            printf("After processing the first 1 byte of %s,\n"
                   "the conversion state is not initial\n\n", str);
        }
     
        (void)mbrlen(&str[1], strlen(str), &mb);
        if (mbsinit(&mb)) {
            printf("After processing the remaining 2 bytes of %s,\n"
                   "the conversion state is initial conversion state\n", str);
        }
    }
```

Saída:
```
    After processing the first 1 byte of 水,
    the conversion state is not initial
     
    After processing the remaining 2 bytes of 水,
    the conversion state is initial conversion state
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.29.6.2.1 A função mbsinit (p: 322) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.29.6.2.1 A função mbsinit (p: 441-442) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.24.6.2.1 A função mbsinit (p: 387-388) 

### Veja também

[`mbstate_t`](<#/doc/string/multibyte/mbstate_t>)`(C95) | informações de estado de conversão necessárias para iterar strings de caracteres multibyte`
`(classe)`
[Documentação C++](<#/>) para mbsinit