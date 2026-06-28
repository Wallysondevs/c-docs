# mbtowc

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
int mbtowc( wchar_t* pwc, const char* s, ``size_t`` n )  // ate C99
int mbtowc( wchar_t* restrict pwc, const char* restrict s, ``size_t`` n )  // desde C99
```

Converte um caractere multibyte cujo primeiro byte é apontado por s para um caractere largo (wide character), escrito em *pwc se pwc não for nulo.

Se s for um ponteiro nulo, redefine o estado de conversão global e determina se sequências de mudança (shift sequences) são usadas.

### Notas

Cada chamada a `mbtowc` atualiza o estado de conversão global interno (um objeto estático do tipo `[`mbstate_t`](<#/doc/string/multibyte/mbstate_t>)`, conhecido apenas por esta função). Se a codificação multibyte usar estados de mudança (shift states), deve-se ter cuidado para evitar retrocessos ou múltiplas varreduras. Em qualquer caso, múltiplas threads não devem chamar `mbtowc` sem sincronização: `[`mbrtowc`](<#/doc/string/multibyte/mbrtowc>)` pode ser usada em vez disso.

### Parâmetros

- **pwc** — ponteiro para o caractere largo para saída
- **s** — ponteiro para o caractere multibyte
- **n** — limite no número de bytes em s que podem ser examinados

### Valor de retorno

Se s não for um ponteiro nulo, retorna o número de bytes contidos no caractere multibyte ou -1 se os primeiros bytes apontados por s não formarem um caractere multibyte válido ou ​0​ se s estiver apontando para o caractere nulo '\0'.

Se s for um ponteiro nulo, redefine seu estado de conversão interno para representar o estado de mudança inicial e retorna ​0​ se a codificação multibyte atual não for dependente de estado (não usa sequências de mudança) ou um valor diferente de zero se a codificação multibyte atual for dependente de estado (usa sequências de mudança).

### Exemplo

Execute este código
```c
    #include <locale.h>
    #include <stdio.h>
    #include <stdlib.h>
    #include <string.h>
    #include <wchar.h>
    
    // imprime string multibyte para stdout orientado a wide
    // equivalente a wprintf(L"%s\n", ptr);
    void print_mb(const char* ptr)
    {
        mbtowc(NULL, NULL, 0); // redefine o estado de conversão
        const char* end = ptr + strlen(ptr);
        int ret = 0;
        for (wchar_t wc; (ret = mbtowc(&wc, ptr, end - ptr)) > 0; ptr += ret)
            wprintf(L"%lc", wc);
        wprintf(L"\n");
    }
    
    int main(void)
    {
        setlocale(LC_ALL, "en_US.utf8");
        // codificação multibyte estreita UTF-8
        print_mb("z\u00df\u6c34\U0001F34C"); // ou "zß水🍌"
    }
```

Saída:
```
    zß水🍌
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.24.7.2 A função mbtowc (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.22.7.2 A função mbtowc (p: 260) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.22.7.2 A função mbtowc (p: 358) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.20.7.2 A função mbtowc (p: 322) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.10.7.2 A função mbtowc 

### Veja também

[`mbrtowc`](<#/doc/string/multibyte/mbrtowc>)`(C95) | converte o próximo caractere multibyte para caractere largo, dado o estado`
`(função)`
[`mblen`](<#/doc/string/multibyte/mblen>) | retorna o número de bytes no próximo caractere multibyte
`(função)`
[`Documentação C++`](<#/>)` para mbtowc`