# iswprint

Definido no cabeçalho [`<wctype.h>`](<#/doc/string/wide>)

```c
int iswprint( wint_t ch );  // desde C95
```

Verifica se o caractere largo fornecido pode ser impresso, ou seja, se é um número (`0123456789`), uma letra maiúscula (`ABCDEFGHIJKLMNOPQRSTUVWXYZ`), uma letra minúscula (`abcdefghijklmnopqrstuvwxyz`), um caractere de pontuação (`!"#$%&'()*+,-./:;<=>?@[\]^_`{!}~`), espaço ou qualquer caractere imprimível específico da localidade C atual.

### Parâmetros

- **ch** — caractere largo

### Valor de retorno

Valor diferente de zero se o caractere largo puder ser impresso, zero caso contrário.

### Notas

[ISO 30112](<http://www.open-std.org/JTC1/SC35/WG5/docs/30112d10.pdf>) especifica quais caracteres Unicode estão incluídos na categoria de impressão POSIX.

### Exemplo

Execute este código
```c
    #include <locale.h>
    #include <stdio.h>
    #include <wchar.h>
    #include <wctype.h>
     
    int main(void)
    {
        wchar_t c = L'\u2002'; // Unicode character 'EN SPACE'
        printf("in the default locale, iswprint(%#x) = %d\n", c, !!iswprint(c));
        setlocale(LC_ALL, "en_US.utf8");
        printf("in Unicode locale, iswprint(%#x) = %d\n", c, !!iswprint(c));
        wchar_t c2 = L'\x82'; // break permitted
        printf("in Unicode locale, iswprint(%#x) = %d\n", c2, !!iswprint(c2));
    }
```

Saída:
```
    in the default locale, iswprint(0x2002) = 0
    in Unicode locale, iswprint(0x2002) = 1
    in Unicode locale, iswprint(0x82) = 0
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.30.2.1.8 A função iswprint (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.30.2.1.8 A função iswprint (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.30.2.1.8 A função iswprint (p: 450)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.25.2.1.8 A função iswprint (p: 396)

### Veja também

[ isprint](<#/doc/string/byte/isprint>) | verifica se um caractere é um caractere imprimível
(função)
[C++ documentation](<#/>) para iswprint
Valores ASCII | caracteres | [`iscntrl`](<#/doc/string/byte/iscntrl>)
[`iswcntrl`](<#/doc/string/wide/iswcntrl>) | [`isprint`](<#/doc/string/byte/isprint>)
`iswprint` | [`isspace`](<#/doc/string/byte/isspace>)
[`iswspace`](<#/doc/string/wide/iswspace>) | [`isblank`](<#/doc/string/byte/isblank>)
[`iswblank`](<#/doc/string/wide/iswblank>) | [`isgraph`](<#/doc/string/byte/isgraph>)
[`iswgraph`](<#/doc/string/wide/iswgraph>) | [`ispunct`](<#/doc/string/byte/ispunct>)
[`iswpunct`](<#/doc/string/wide/iswpunct>) | [`isalnum`](<#/doc/string/byte/isalnum>)
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
71–90 | `\x47`–`\x5A` | `\107`–`\132` | `GHIJKLMNOP` `QRSTUVWXYZ` | `0` | `≠0` | `0` | `0` | `≠0` | `0` | `≠0` | `≠0` | `≠0` | `0` | `0` | `0`
91–96 | `\x5B`–`\x60` | `\133`–`\140` | `[\]^_` | `0` | `≠0` | `0` | `0` | `≠0` | `≠0` | `0` | `0` | `0` | `0` | `0` | `0`
97–102 | `\x61`–`\x66` | `\141`–`\146` | `abcdef` | `0` | `≠0` | `0` | `0` | `≠0` | `0` | `≠0` | `≠0` | `0` | `≠0` | `0` | `≠0`
103–122 | `\x67`–`\x7A` | `\147`–`\172` | `ghijklmnop` `qrstuvwxyz` | `0` | `≠0` | `0` | `0` | `≠0` | `0` | `≠0` | `≠0` | `0` | `≠0` | `0` | `0`
123–126 | `\x7B`–`\x7E` | `\173`–`\176` | `{|}~` | `0` | `≠0` | `0` | `0` | `≠0` | `≠0` | `0` | `0` | `0` | `0` | `0` | `0`
127 | `\x7F` | `\177` | caractere backspace (`DEL`) | `≠0` | `0` | `0` | `0` | `0` | `0` | `0` | `0` | `0` | `0` | `0` | `0`