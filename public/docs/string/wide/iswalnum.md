# iswalnum

Definido no cabeçalho [`<wctype.h>`](<#/doc/string/wide>)

```c
int iswalnum( wint_t ch );  // desde C95
```

  
Verifica se o caractere largo fornecido é um caractere alfanumérico, ou seja, um número (0123456789), uma letra maiúscula (`ABCDEFGHIJKLMNOPQRSTUVWXYZ`), uma letra minúscula (`abcdefghijklmnopqrstuvwxyz`) ou qualquer caractere alfanumérico específico da localidade atual. 

### Parâmetros

ch  |  \-  |  caractere largo   
  
### Valor de retorno

Valor diferente de zero se o caractere largo for um caractere alfanumérico, zero caso contrário. 

### Observações

[ISO 30112](<https://www.open-std.org/JTC1/SC35/WG5/docs/30112d10.pdf>) especifica quais caracteres Unicode estão incluídos na categoria alfanumérica POSIX. 

### Exemplo

Execute este código
```
    #include <stdio.h>
    #include <locale.h>
    #include <wchar.h>
    #include <wctype.h>
     
    int main(void)
    {
        wchar_t c = L'\u13ad'; // the Cherokee letter HA ('Ꭽ')
        printf("in the default locale, iswalnum(%#x) = %d\n", c, !!iswalnum(c));
        setlocale(LC_ALL, "en_US.utf8");
        printf("in Unicode locale, iswalnum(%#x) = %d\n", c, !!iswalnum(c));
    }
```

Saída possível: 
```
    in the default locale, iswalnum(0x13ad) = 0
    in Unicode locale, iswalnum(0x13ad) = 1
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * TBD A função iswalnum (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.30.2.1.1 A função iswalnum (p: 327) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.30.2.1.1 A função iswalnum (p: 448) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.25.2.1.1 A função iswalnum (p: 394) 

### Veja também

[ isalnum](<#/doc/string/byte/isalnum>) |  verifica se um caractere é alfanumérico   
(função)  
[Documentação C++](<#/>) para iswalnum  
Valores ASCII  | caracteres  |  [`iscntrl`](<#/doc/string/byte/iscntrl>)  
[`iswcntrl`](<#/doc/string/wide/iswcntrl>) |  [`isprint`](<#/doc/string/byte/isprint>)  
[`iswprint`](<#/doc/string/wide/iswprint>) |  [`isspace`](<#/doc/string/byte/isspace>)  
[`iswspace`](<#/doc/string/wide/iswspace>) |  [`isblank`](<#/doc/string/byte/isblank>)  
[`iswblank`](<#/doc/string/wide/iswblank>) |  [`isgraph`](<#/doc/string/byte/isgraph>)  
[`iswgraph`](<#/doc/string/wide/iswgraph>) |  [`ispunct`](<#/doc/string/byte/ispunct>)   
[`iswpunct`](<#/doc/string/wide/iswpunct>) |  [`isalnum`](<#/doc/string/byte/isalnum>)   
`iswalnum` |  [`isalpha`](<#/doc/string/byte/isalpha>)   
[`iswalpha`](<#/doc/string/wide/iswalpha>) |  [`isupper`](<#/doc/string/byte/isupper>)  
[`iswupper`](<#/doc/string/wide/iswupper>) |  [`islower`](<#/doc/string/byte/islower>)  
[`iswlower`](<#/doc/string/wide/iswlower>) |  [`isdigit`](<#/doc/string/byte/isdigit>)  
[`iswdigit`](<#/doc/string/wide/iswdigit>) |  [`isxdigit`](<#/doc/string/byte/isxdigit>)  
[`iswxdigit`](<#/doc/string/wide/iswxdigit>)  
decimal  |  hexadecimal  |  octal   
0–8  | `\x0`–`\x8` | `\0`–`\10` | códigos de controle (`NUL`, etc.)  | `≠0` |  `0` |  `0` |  `0` |  `0` |  `0` |  `0` |  `0` |  `0` |  `0` |  `0` |  `0`  
9  | `\x9` | `\11` | tab (`\t`)  | `≠0` |  `0` | `≠0` | `≠0` |  `0` |  `0` |  `0` |  `0` |  `0` |  `0` |  `0` |  `0`  
10–13  | `\xA`–`\xD` | `\12`–`\15` | espaços em branco (`\n`, `\v`, `\f`, `\r`)  | `≠0` |  `0` | `≠0` |  `0` |  `0` |  `0` |  `0` |  `0` |  `0` |  `0` |  `0` |  `0`  
14–31  | `\xE`–`\x1F` | `\16`–`\37` | códigos de controle  | `≠0` |  `0` |  `0` |  `0` |  `0` |  `0` |  `0` |  `0` |  `0` |  `0` |  `0` |  `0`  
32  | `\x20` | `\40` | espaço  |  `0` | `≠0` | `≠0` | `≠0` |  `0` |  `0` |  `0` |  `0` |  `0` |  `0` |  `0` |  `0`  
33–47  | `\x21`–`\x2F` | `\41`–`\57` | `!"#$%&'()*+,-./` |  `0` | `≠0` |  `0` |  `0` | `≠0` | `≠0` |  `0` |  `0` |  `0` |  `0` |  `0` |  `0`  
48–57  | `\x30`–`\x39` | `\60`–`\71` | `0123456789` |  `0` | `≠0` |  `0` |  `0` | `≠0` |  `0` | `≠0` |  `0` |  `0` |  `0` | `≠0` | `≠0`  
58–64  | `\x3A`–`\x40` | `\72`–`\100` | `:;<=>?@` |  `0` | `≠0` |  `0` |  `0` | `≠0` | `≠0` |  `0` |  `0` |  `0` |  `0` |  `0` |  `0`  
65–70  | `\x41`–`\x46` | `\101`–`\106` | `ABCDEF` |  `0` | `≠0` |  `0` |  `0` | `≠0` |  `0` | `≠0` | `≠0` | `≠0` |  `0` |  `0` | `≠0`  
71–90  | `\x47`–`\x5A` | `\107`–`\132` | `GHIJKLMNOP`  
`QRSTUVWXYZ` |  `0` | `≠0` |  `0` |  `0` | `≠0` |  `0` | `≠0` | `≠0` | `≠0` |  `0` |  `0` |  `0`  
91–96  | `\x5B`–`\x60` | `\133`–`\140` | `[\]^_` |  `0` | `≠0` |  `0` |  `0` | `≠0` | `≠0` |  `0` |  `0` |  `0` |  `0` |  `0` |  `0`  
97–102  | `\x61`–`\x66` | `\141`–`\146` | `abcdef` |  `0` | `≠0` |  `0` |  `0` | `≠0` |  `0` | `≠0` | `≠0` |  `0` | `≠0` |  `0` | `≠0`  
103–122  | `\x67`–`\x7A` | `\147`–`\172` | `ghijklmnop`  
`qrstuvwxyz` |  `0` | `≠0` |  `0` |  `0` | `≠0` |  `0` | `≠0` | `≠0` |  `0` | `≠0` |  `0` |  `0`  
123–126  | `\x7B`–`\x7E` | `\173`–`\176` | `{|}~` |  `0` | `≠0` |  `0` |  `0` | `≠0` | `≠0` |  `0` |  `0` |  `0` |  `0` |  `0` |  `0`  
127  | `\x7F` | `\177` | caractere de backspace (`DEL`)  | `≠0` |  `0` |  `0` |  `0` |  `0` |  `0` |  `0` |  `0` |  `0` |  `0` |  `0` |  `0`