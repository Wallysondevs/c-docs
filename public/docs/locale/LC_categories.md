# LC_ALL, LC_COLLATE, LC_CTYPE, LC_MONETARY, LC_NUMERIC, LC_TIME

Definido no cabeçalho [`<locale.h>`](<#/doc/locale>)

```c
#define LC_ALL /* definido pela implementação */
#define LC_COLLATE /* definido pela implementação */
#define LC_CTYPE /* definido pela implementação */
#define LC_MONETARY /* definido pela implementação */
#define LC_NUMERIC /* definido pela implementação */
#define LC_TIME /* definido pela implementação */
```

Cada uma das constantes de macro acima se expande para expressões constantes inteiras com valores distintos que são adequados para uso como o primeiro argumento de [setlocale](<#/doc/locale/setlocale>).

Constante | Explicação
`LC_ALL` | seleciona a localidade C inteira
`LC_COLLATE` | seleciona a categoria de ordenação (collation) da localidade C
`LC_CTYPE` | seleciona a categoria de classificação de caracteres da localidade C
`LC_MONETARY` | seleciona a categoria de formatação monetária da localidade C
`LC_NUMERIC` | seleciona a categoria de formatação numérica da localidade C
`LC_TIME` | seleciona a categoria de formatação de data/hora da localidade C

Constantes de macro adicionais, com nomes que começam com `LC_` seguidos por pelo menos uma letra maiúscula, podem ser definidas em `locale.h`. Por exemplo, a especificação POSIX requer `LC_MESSAGES` (que controla, entre outras coisas, [perror](<#/doc/io/perror>) e [strerror](<#/doc/string/byte/strerror>)), ISO/IEC 30112:2014 ([rascunho de 2014](<https://www.open-std.org/JTC1/SC35/WG5/docs/30112d10.pdf>)) define adicionalmente `LC_IDENTIFICATION`, `LC_XLITERATE`, `LC_NAME`, `LC_ADDRESS`, `LC_TELEPHONE`, `LC_PAPER`, `LC_MEASUREMENT`, e `LC_KEYBOARD`, que são suportadas pela biblioteca C GNU (exceto por `LC_XLITERATE`).

### Exemplo

Execute este código
```c
    #include <locale.h>
    #include <stdio.h>
    #include <time.h>
    #include <wchar.h>
     
    int main(void)
    {
        setlocale(LC_ALL, "en_US.UTF-8"); // the C locale will be the UTF-8 enabled English
        setlocale(LC_NUMERIC, "de_DE.utf8"); // decimal dot will be German
        setlocale(LC_TIME, "ja_JP.utf8");    // date/time formatting will be Japanese
        wchar_t str[100];
        time_t t = time(NULL);
        wcsftime(str, 100, L"%A %c", localtime(&t));
        wprintf(L"Number: %.2f\nDate: %Ls\n", 3.14, str);
    }
```

Saída possível:
```
    Number: 3,14
    Date: 金曜日 2023年09月15日 20時04分14秒
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.11/3 Localização <locale.h> (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.11/3 Localização <locale.h> (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.11/3 Localização <locale.h> (p: 224)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.11/3 Localização <locale.h> (p: 205)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.4 LOCALIZAÇÃO <locale.h>

### Ver também

[ setlocale](<#/doc/locale/setlocale>) | obtém e define a localidade C atual
(função)
[Documentação C++](<#/>) para categorias de localidade