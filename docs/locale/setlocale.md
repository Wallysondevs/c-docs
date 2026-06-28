# setlocale

Definido no cabeçalho [`<locale.h>`](<#/doc/locale>)

```c
char* setlocale( int category, const char* locale );
```

A função `setlocale` instala a localidade do sistema especificada ou uma parte dela como a nova localidade C. As modificações permanecem em vigor e influenciam a execução de todas as funções da biblioteca C sensíveis à localidade até a próxima chamada para `setlocale`. Se `locale` for um ponteiro nulo, `setlocale` consulta a localidade C atual sem modificá-la.

### Parâmetros

- **category** — identificador da categoria de localidade, uma das macros [`LC_xxx`](<#/doc/locale/LC_categories>). Pode ser nulo.
- **locale** — identificador de localidade específico do sistema. Pode ser "" para a localidade preferida pelo usuário ou "C" para a localidade mínima.

### Valor de retorno

ponteiro para uma string estreita terminada em nulo que identifica a localidade C após aplicar as alterações, se houver, ou ponteiro nulo em caso de falha.

Uma cópia da string retornada, juntamente com a categoria usada nesta chamada para `setlocale`, pode ser usada posteriormente no programa para restaurar a localidade ao estado no final desta chamada.

### Observações

Durante a inicialização do programa, o equivalente a setlocale([LC_ALL](<#/doc/locale/LC_categories>), "C"); é executado antes que qualquer código de usuário seja executado.

Embora o tipo de retorno seja char*, modificar os caracteres apontados é comportamento indefinido.

Como `setlocale` modifica o estado global que afeta a execução de funções dependentes da localidade, é comportamento indefinido chamá-la de uma thread, enquanto outra thread está executando qualquer uma das seguintes funções: [fprintf](<#/doc/io/fprintf>), [isprint](<#/doc/string/byte/isprint>), [iswdigit](<#/doc/string/wide/iswdigit>), [localeconv](<#/doc/locale/localeconv>), [tolower](<#/doc/string/byte/tolower>), [fscanf](<#/doc/io/fscanf>), [ispunct](<#/doc/string/byte/ispunct>), [iswgraph](<#/doc/string/wide/iswgraph>), [mblen](<#/doc/string/multibyte/mblen>), [toupper](<#/doc/string/byte/toupper>), [isalnum](<#/doc/string/byte/isalnum>), [isspace](<#/doc/string/byte/isspace>), [iswlower](<#/doc/string/wide/iswlower>), [mbstowcs](<#/doc/string/multibyte/mbstowcs>), [towlower](<#/doc/string/wide/towlower>), [isalpha](<#/doc/string/byte/isalpha>), [isupper](<#/doc/string/byte/isupper>), [iswprint](<#/doc/string/wide/iswprint>), [mbtowc](<#/doc/string/multibyte/mbtowc>), [towupper](<#/doc/string/wide/towupper>), [isblank](<#/doc/string/byte/isblank>), [iswalnum](<#/doc/string/wide/iswalnum>), [iswpunct](<#/doc/string/wide/iswpunct>), `setlocale`, [wcscoll](<#/doc/string/wide/wcscoll>), [iscntrl](<#/doc/string/byte/iscntrl>), [iswalpha](<#/doc/string/wide/iswalpha>), [iswspace](<#/doc/string/wide/iswspace>), [strcoll](<#/doc/string/byte/strcoll>), [wcstod](<#/doc/string/wide/wcstof>), [isdigit](<#/doc/string/byte/isdigit>), [iswblank](<#/doc/string/wide/iswblank>), [iswupper](<#/doc/string/wide/iswupper>), [strerror](<#/doc/string/byte/strerror>), [wcstombs](<#/doc/string/multibyte/wcstombs>), [isgraph](<#/doc/string/byte/isgraph>), [iswcntrl](<#/doc/string/wide/iswcntrl>), [iswxdigit](<#/doc/string/wide/iswxdigit>), [strtod](<#/doc/string/byte/strtof>), [wcsxfrm](<#/doc/string/wide/wcsxfrm>), [islower](<#/doc/string/byte/islower>), [iswctype](<#/doc/string/wide/iswctype>), [isxdigit](<#/doc/string/byte/isxdigit>).

POSIX também define uma localidade chamada "POSIX", que é sempre acessível e é exatamente equivalente à localidade mínima padrão "C".

POSIX também especifica que o ponteiro retornado, não apenas o conteúdo da string apontada, pode ser invalidado por chamadas subsequentes a `setlocale`.

### Exemplo

Execute este código
```c
    #include <locale.h>
    #include <stdio.h>
    #include <time.h>
    #include <wchar.h>
    
    int main(void)
    {
        // the C locale will be UTF-8 enabled English;
        // decimal dot will be German
        // date and time formatting will be Japanese
        setlocale(LC_ALL, "en_US.UTF-8");
        setlocale(LC_NUMERIC, "de_DE.utf8");
        setlocale(LC_TIME, "ja_JP.utf8");
    
        wchar_t str[100];
        time_t t = time(NULL);
        wcsftime(str, 100, L"%A %c", localtime(&t));
        wprintf(L"Number: %.2f\nDate: %ls\n", 3.14, str);
    }
```

Saída possível:
```
    Number: 3,14
    Date: 月曜日 2017年09月25日 13時00分15秒
```

### Referências

*   Padrão C23 (ISO/IEC 9899:2024):
    *   7.11.1.1 A função setlocale (p: TBD)
*   Padrão C17 (ISO/IEC 9899:2018):
    *   7.11.1.1 A função setlocale (p: 163-164)
*   Padrão C11 (ISO/IEC 9899:2011):
    *   7.11.1.1 A função setlocale (p: 224-225)
*   Padrão C99 (ISO/IEC 9899:1999):
    *   7.11.1.1 A função setlocale (p: 205-206)
*   Padrão C89/C90 (ISO/IEC 9899:1990):
    *   4.4.1.1 A função setlocale

### Veja também

[ LC_ALLLC_COLLATELC_CTYPELC_MONETARYLC_NUMERICLC_TIME](<#/doc/locale/LC_categories>) | categorias de localidade para **setlocale**
(constante de macro)
[documentação C++](<#/>) para setlocale

### Links externos

1.  | [Lista de nomes de localidades do Windows](<https://ss64.com/locale.html>).
2.  | [Lista de nomes de localidades do Linux](<https://lh.2xlibre.net/locales/>).