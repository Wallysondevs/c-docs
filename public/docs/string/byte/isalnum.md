# isalnum

Definido no cabeçalho [`<ctype.h>`](<#/doc/string/byte>)

```c
int isalnum( int ch );
```

Verifica se o caractere fornecido é um caractere alfanumérico, conforme classificado pela localidade C atual. Na localidade padrão, os seguintes caracteres são alfanuméricos:

  * Dígitos (`0123456789`),
  * Letras maiúsculas (`ABCDEFGHIJKLMNOPQRSTUVWXYZ`),
  * Letras minúsculas (`abcdefghijklmnopqrstuvwxyz`).

O comportamento é indefinido se o valor de ch não for representável como unsigned char e não for igual a [EOF](<#/doc/io>).

### Parâmetros

- **ch** — caractere a ser classificado

### Valor de retorno

Valor diferente de zero se o caractere for alfanumérico, ​0​ caso contrário.

### Exemplo

Demonstra o uso de `isalnum` com diferentes localidades (específicas do SO).

Execute este código
```c
    #include <ctype.h>
    #include <locale.h>
    #include <stdio.h>
    
    int main(void)
    {
        unsigned char c = '\xdf'; // Letra alemã ß em ISO-8859-1
    
        printf("isalnum('\\xdf') in default C locale returned %d\n", !!isalnum(c));
    
        if (setlocale(LC_CTYPE, "de_DE.iso88591"))
            printf("isalnum('\\xdf') in ISO-8859-1 locale returned %d\n", !!isalnum(c));
    }
```

Saída possível:
```
    isalnum('\xdf') in default C locale returned 0
    isalnum('\xdf') in ISO-8859-1 locale returned 1
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.4.1.1 A função isalnum (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.4.1.1 A função isalnum (p: 145)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.4.1.1 A função isalnum (p: 200)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.4.1.1 A função isalnum (p: 181)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.3.1.1 A função isalnum

### Veja também

[ iswalnum](<#/doc/string/wide/iswalnum>)(C95) | verifica se um caractere largo é alfanumérico
(função)
[Documentação C++](<#/>) para isalnum
Valores ASCII | caracteres | [`iscntrl`](<#/doc/string/byte/iscntrl>)
[`iswcntrl`](<#/doc/string/wide/iswcntrl>) | [`isprint`](<#/doc/string/byte/isprint>)
[`iswprint`](<#/doc/string/wide/iswprint>) | [`isspace`](<#/doc/string/byte/isspace>)
[`iswspace`](<#/doc/string/wide/iswspace>) | [`isblank`](<#/doc/string/byte/isblank>)
[`iswblank`](<#/doc/string/wide/iswblank>) | [`isgraph`](<#/doc/string/byte/isgraph>)
[`iswgraph`](<#/doc/string/wide/iswgraph>) | [`ispunct`](<#/doc/string/byte/ispunct>)
[`iswpunct`](<#/doc/string/wide/iswpunct>) | `isalnum`
[`iswalnum`](<#/doc/string/wide/iswalnum>) | [`isalpha`](<#/doc/string/byte/isalpha>)
[`iswalpha`](<#/doc/string/wide/iswalpha>) | [`isupper`](<#/doc/string/byte/isupper>)
[`iswupper`](<#/doc/string/wide/iswupper>) | [`islower`](<#/doc/string/byte/islower>)
[`iswlower`](<#/doc/string/wide/iswlower>) | [`isdigit`](<#/doc/string/byte/isdigit>)
[`iswdigit`](<#/doc/string/wide/iswdigit>) | [`isxdigit`](<#/doc/string/byte/isxdigit>)
[`iswxdigit`](<#/doc/string/wide/iswxdigit>)
decimal | hexadecimal | octal
0–8 | `\x0`–`\x8` | `\0`–`\10` | códigos de controle (`NUL`, etc.) | `≠0` | `0` | `0` | `0` | `0` | `0` | `0` | `0` | `0` | `0` | `0` | `0`
9 | `\x9` | `\11` | tab (`\t`) | `≠0` | `0` | `≠0` | `≠0` | `0` | `0` | `0` | `0` | `0` | `0` | `0` | `0`
10–13 | `\xA`–`\xD` | `\12`–`\15` | espaços em branco (`\n`, `\v`, `\f`, `\r`) | `≠0` | `0` | `≠0` | `0` | `0` | `0` | `0` | `0` | `0` | `0` | `0` | `0`
14–31 | `\xE`–`\x1F` | `\16`–`\37` | códigos de controle | `≠0` | `0` | `0` | `0` | `0` | `0` | `0` | `0` | `0` | `0` | `0` | `0`
32 | `\x20` | `\40` | espaço | `0` | `≠0` | `≠0` | `≠0` | `0` | `0` | `0` | `0` | `0` | `0` | `0` | `0`
33–47 | `\x21`–`\x2F` | `\41`–`\57` | `!"#$%&'()*+,-./` | `0` | `≠0` | `0` | `0` | `≠0` | `≠0` | `0` | `0` | `0` | `0` | `0` | `0`
48–57 | `\x30`–`\x39` | `\60`–`\71` | `0123456789` | `0` | `≠0` | `0` | `0` | `≠0` | `0` | `≠0` | `0` | `0` | `0` | `≠0` | `≠0`
58–64 | `\x3A`–`\x40` | `\72`–`\100` | `:;<=>?@` | `0` | `≠0` | `0` | `0` | `≠0` | `≠0` | `0` | `0` | `0` | `0` | `0` | `0`
65–70 | `\x41`–`\x46` | `\101`–`\106` | `ABCDEF` | `0` | `≠0` | `0` | `0` | `≠0` | `0` | `≠0` | `≠0` | `≠0` | `0` | `0` | `≠0`
71–90 | `\x47`–`\x5A` | `\107`–`\132` | `GHIJKLMNOP`
`QRSTUVWXYZ` | `0` | `≠0` | `0` | `0` | `≠0` | `0` | `≠0` | `≠0` | `≠0` | `0` | `0` | `0`
91–96 | `\x5B`–`\x60` | `\133`–`\140` | `[\]^_` | `0` | `≠0` | `0` | `0` | `≠0` | `≠0` | `0` | `0` | `0` | `0` | `0` | `0`
97–102 | `\x61`–`\x66` | `\141`–`\146` | `abcdef` | `0` | `≠0` | `0` | `0` | `≠0` | `0` | `≠0` | `≠0` | `0` | `≠0` | `0` | `≠0`
103–122 | `\x67`–`\x7A` | `\147`–`\172` | `ghijklmnop`
`qrstuvwxyz` | `0` | `≠0` | `0` | `0` | `≠0` | `0` | `≠0` | `≠0` | `0` | `≠0` | `0` | `0`
123–126 | `\x7B`–`\x7E` | `\173`–`\176` | `{|}~` | `0` | `≠0` | `0` | `0` | `≠0` | `≠0` | `0` | `0` | `0` | `0` | `0` | `0`
127 | `\x7F` | `\177` | caractere de backspace (`DEL`) | `≠0` | `0` | `0` | `0` | `0` | `0` | `0` | `0` | `0` | `0` | `0` | `0`