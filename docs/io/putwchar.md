# putwchar

Definido no cabeçalho [`<wchar.h>`](<../string/wide.html> "c/string/wide")

```c
wint_t putwchar( wchar_t ch );  // desde C95
```

Escreve um caractere largo ch para `stdout`.

### Parâmetros

- **ch** — caractere largo a ser escrito

### Valor de retorno

ch em caso de sucesso, WEOF em caso de falha.

### Exemplo

Execute este código
```
    #include <locale.h>
    #include <stdio.h>
    #include <stdlib.h>
    #include <wchar.h>
     
    int main()
    {
        setlocale(LC_ALL, "en_US.utf8");
     
        const wchar_t data[] =
        {
            L'\u2200', // Unicode name: "FOR ALL"
            L'∀',
            L'\n',
        };
     
        for (size_t t = 0; t != (sizeof data / sizeof(wchar_t)); ++t)
        {
            if (putwchar(data[t]) == WEOF)
            {
                puts("I/O error in putwchar");
                return EXIT_FAILURE;
            }
        }
     
        return EXIT_SUCCESS;
    }
```

Saída possível:
```
    ∀∀
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

  * 7.31.3.9 A função putwchar (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

  * 7.29.3.9 A função putwchar (p: 310)

  * Padrão C11 (ISO/IEC 9899:2011):

  * 7.29.3.9 A função putwchar (p: 425)

  * Padrão C99 (ISO/IEC 9899:1999):

  * 7.24.3.9 A função putwchar (p: 370)

### Veja também

[ putchar](<#/doc/io/putchar>) | escreve um caractere para [stdout](<#/doc/io/std_streams>)
(função)
[ fputwcputwc](<#/doc/io/fputwc>)(C95) | escreve um caractere largo em um fluxo de arquivo
(função)
[Documentação C++](<#/>) para putwchar