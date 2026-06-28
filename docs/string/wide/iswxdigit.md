# iswxdigit

Definido no cabeçalho [`<wctype.h>`](<#/doc/string/wide>) | | (desde C95)

```c
int iswxdigit( wint_t ch );
```

Verifica se o caractere largo fornecido corresponde (se estreitado) a um caractere numérico hexadecimal, ou seja, um de `0123456789abcdefABCDEF`.

### Parâmetros

- **ch** — caractere largo

### Valor de retorno

Valor diferente de zero se o caractere largo for um caractere numérico hexadecimal, zero caso contrário.

### Observações

[iswdigit](<#/doc/string/wide/iswdigit>) e `iswxdigit` são as únicas funções padrão de classificação de caracteres largos que não são afetadas pela localidade C atualmente instalada.

### Exemplo

Algumas localidades oferecem classes de caracteres adicionais que detectam dígitos não-ASCII

Execute este código
```c
    #include <locale.h>
    #include <stdio.h>
    #include <wchar.h>
    #include <wctype.h>
    
    void test(wchar_t a3, wchar_t u3, wchar_t j3)
    {
        printf("\t  '%lc'  '%lc' '%lc'\n", a3, u3, j3);
        printf("iswxdigit: %d   %d   %d\n",
               !!iswxdigit(a3),
               !!iswxdigit(u3),
               !!iswxdigit(j3));
        printf("jdigit:    %d   %d   %d\n",
               !!iswctype(a3, wctype("jdigit")),
               !!iswctype(u3, wctype("jdigit")),
               !!iswctype(j3, wctype("jdigit")));
    }
    
    int main(void)
    {
        wchar_t a3 = L'9';  // the ASCII digit 9
        wchar_t u3 = L'〩'; // the CJK numeral 9
        wchar_t j3 = L'９'; // the full-width digit 9
    
        setlocale(LC_ALL, "en_US.utf8");
        puts("In American locale:");
        test(a3, u3, j3);
    
        setlocale(LC_ALL, "ja_JP.utf8");
        puts("\nIn Japanese locale:");
        test(a3, u3, j3);
    }
```

Saída possível:
```
    In American locale:
    	  '9'  '〩' '９'
    iswxdigit: 1    0    0
    jdigit:    0    0    0
    
    In Japanese locale:
    	  '9'  '〩' '９'
    iswxdigit: 1    0    0
    jdigit:    0    0    1
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.30.2.1.12 A função iswxdigit (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.30.2.1.12 A função iswxdigit (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.30.2.1.12 A função iswxdigit (p: 451)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.25.2.1.12 A função iswxdigit (p: 397)

### Veja também

[ isxdigit](<#/doc/string/byte/isxdigit>) | verifica se um caractere é um caractere hexadecimal
(função)
[Documentação C++](<#/>) para iswxdigit
Valores ASCII | caracteres | [`iscntrl`](<#/doc/string/byte/iscntrl>)
[`iswcntrl`](<#/doc/string/wide/iswcntrl>) | [`isprint`](<#/doc/string/byte/isprint>)
[`iswprint`](<#/doc/string/wide/iswprint>) | [`isspace`](<#/doc/string/byte/isspace>)
[`iswspace`](<#/doc/string/wide/iswspace>) | [`isblank`](<#/doc/string/byte/isblank>)
[`iswblank`](<#/doc/string/wide/iswblank>) | [`isgraph`](<#/doc/string/byte/isgraph>)
[`iswgraph`](<#/doc/string/wide/iswgraph>) | [`ispunct`](<#/doc/string/byte/ispunct>)
[`iswpunct`](<#/doc/string/wide/iswpunct>) | [`isalnum`](<#/doc/string/byte/isalnum>)
[`iswalnum`](<#/doc/string/wide/iswalnum>) | [`isalpha`](<#/doc/string/byte/isalpha>)
[`iswalpha`](<#/doc/string/wide/iswalpha>) | [`isupper`](<#/doc/string/byte/isupper>)
[`iswupper`](<#/doc/string/wide/iswupper>) | [`islower`](<#/doc/string/byte/islower>)
[`iswlower`](<#/doc/string/wide/iswlower>) | [`isdigit`](<#/doc/string/byte/isdigit>)
[`iswdigit`](<#/doc/string/wide/iswdigit>) | [`isxdigit`](<#/doc/string/byte/isxdigit>)
`iswxdigit`
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