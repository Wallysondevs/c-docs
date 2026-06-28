# isalpha

Definido no cabeçalho [`<ctype.h>`](<#/doc/string/byte>)

```c
int isalpha( int ch );
```

Verifica se o caractere fornecido é um caractere alfabético, ou seja, uma letra maiúscula (`ABCDEFGHIJKLMNOPQRSTUVWXYZ`) ou uma letra minúscula (`abcdefghijklmnopqrstuvwxyz`).

Em localidades diferentes de "C", um caractere alfabético é um caractere para o qual [isupper()](<#/doc/string/byte/isupper>) ou [islower()](<#/doc/string/byte/islower>) retorna verdadeiro, ou qualquer outro caractere considerado alfabético pela localidade. Em qualquer caso, [iscntrl()](<#/doc/string/byte/iscntrl>), [isdigit()](<#/doc/string/byte/isdigit>), [ispunct()](<#/doc/string/byte/ispunct>) e [isspace()](<#/doc/string/byte/isspace>) retornarão falso para este caractere.

O comportamento é indefinido se o valor de `ch` não for representável como unsigned char e não for igual a [EOF](<#/doc/io>).

### Parâmetros

- **ch** — caractere a ser classificado

### Valor de retorno

Valor diferente de zero se o caractere for um caractere alfabético, zero caso contrário.

### Exemplo

Demonstra o uso de `isalpha` com diferentes localidades (específico do SO).

Execute este código
```c
    #include <ctype.h>
    #include <stdio.h>
    #include <locale.h>
    
    int main(void)
    {
        unsigned char c = '\xdf'; // German letter ß in ISO-8859-1
    
        printf("isalpha('\\xdf') in default C locale returned %d\n", !!isalpha(c));
    
        setlocale(LC_CTYPE, "de_DE.iso88591");
        printf("isalpha('\\xdf') in ISO-8859-1 locale returned %d\n", !!isalpha(c));
    }
```

Saída possível:
```
    isalpha('\xdf') in default C locale returned 0
    isalpha('\xdf') in ISO-8859-1 locale returned 1
```

### Referências

* Padrão C17 (ISO/IEC 9899:2018):

  * 7.4.1.2 A função isalpha (p: 145)

* Padrão C11 (ISO/IEC 9899:2011):

  * 7.4.1.2 A função isalpha (p: 200-201)

* Padrão C99 (ISO/IEC 9899:1999):

  * 7.4.1.2 A função isalpha (p: 181-182)

* Padrão C89/C90 (ISO/IEC 9899:1990):

  * 4.3.1.2 A função isalpha

### Veja também

[ iswalpha](<#/doc/string/wide/iswalpha>)(C95) | verifica se um caractere largo é alfabético
(função)
[Documentação C++](<#/>) para isalpha
Valores ASCII | caracteres | [`iscntrl`](<#/doc/string/byte/iscntrl>)
[`iswcntrl`](<#/doc/string/wide/iswcntrl>) | [`isprint`](<#/doc/string/byte/isprint>)
[`iswprint`](<#/doc/string/wide/iswprint>) | [`isspace`](<#/doc/string/byte/isspace>)
[`iswspace`](<#/doc/string/wide/iswspace>) | [`isblank`](<#/doc/string/byte/isblank>)
[`iswblank`](<#/doc/string/wide/iswblank>) | [`isgraph`](<#/doc/string/byte/isgraph>)
[`iswgraph`](<#/doc/string/wide/iswgraph>) | [`ispunct`](<#/doc/string/byte/ispunct>)
[`iswpunct`](<#/doc/string/wide/iswpunct>) | [`isalnum`](<#/doc/string/byte/isalnum>)
[`iswalnum`](<#/doc/string/wide/iswalnum>) | `isalpha`
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
127 | `\x7F` | `\177` | caractere backspace (`DEL`) | `≠0` | `0` | `0` | `0` | `0` | `0` | `0` | `0` | `0` | `0` | `0` | `0`