# Strings largas terminadas em nulo

Uma string larga terminada em nulo é uma sequência de caracteres largos válidos, terminada com um caractere nulo.

### Funções

##### Classificação de caracteres

---
Definido no cabeçalho `<wctype.h>`
[ iswalnum](<#/doc/string/wide/iswalnum>)(C95) | verifica se um caractere largo é alfanumérico
(função)
[ iswalpha](<#/doc/string/wide/iswalpha>)(C95) | verifica se um caractere largo é alfabético
(função)
[ iswlower](<#/doc/string/wide/iswlower>)(C95) | verifica se um caractere largo é um caractere minúsculo
(função)
[ iswupper](<#/doc/string/wide/iswupper>)(C95) | verifica se um caractere largo é um caractere maiúsculo
(função)
[ iswdigit](<#/doc/string/wide/iswdigit>)(C95) | verifica se um caractere largo é um dígito
(função)
[ iswxdigit](<#/doc/string/wide/iswxdigit>)(C95) | verifica se um caractere largo é um caractere hexadecimal
(função)
[ iswcntrl](<#/doc/string/wide/iswcntrl>)(C95) | verifica se um caractere largo é um caractere de controle
(função)
[ iswgraph](<#/doc/string/wide/iswgraph>)(C95) | verifica se um caractere largo é um caractere gráfico
(função)
[ iswspace](<#/doc/string/wide/iswspace>)(C95) | verifica se um caractere largo é um caractere de espaço
(função)
[ iswblank](<#/doc/string/wide/iswblank>)(C99) | verifica se um caractere largo é um caractere em branco
(função)
[ iswprint](<#/doc/string/wide/iswprint>)(C95) | verifica se um caractere largo é um caractere imprimível
(função)
[ iswpunct](<#/doc/string/wide/iswpunct>)(C95) | verifica se um caractere largo é um caractere de pontuação
(função)
[ iswctype](<#/doc/string/wide/iswctype>)(C95) | classifica um caractere largo de acordo com a categoria [LC_CTYPE](<#/doc/locale/LC_categories>) especificada
(função)
[ wctype](<#/doc/string/wide/wctype>)(C95) | procura uma categoria de classificação de caracteres no locale C atual
(função)

##### Manipulação de caracteres

---
Definido no cabeçalho `<wctype.h>`
[ towlower](<#/doc/string/wide/towlower>)(C95) | converte um caractere largo para minúsculo
(função)
[ towupper](<#/doc/string/wide/towupper>)(C95) | converte um caractere largo para maiúsculo
(função)
[ towctrans](<#/doc/string/wide/towctrans>)(C95) | realiza o mapeamento de caracteres de acordo com a categoria de mapeamento [LC_CTYPE](<#/doc/locale/LC_categories>) especificada
(função)
[ wctrans](<#/doc/string/wide/wctrans>)(C95) | procura uma categoria de mapeamento de caracteres no locale C atual
(função)
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
[`iswxdigit`](<#/doc/string/wide/iswxdigit>)
decimal | hexadecimal | octal
0–8 | `\x0`–`\x8` | `\0`–`\10` | códigos de controle (`NUL`, etc.) | `≠0` | `0` | `0` | `0` | `0` | `0` | `0` | `0` | `0` | `0` | `0` | `0`
9 | `\x9` | `\11` | tabulação (`\t`) | `≠0` | `0` | `≠0` | `≠0` | `0` | `0` | `0` | `0` | `0` | `0` | `0` | `0`
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

##### Conversões para formatos numéricos

---
Definido no cabeçalho `<wchar.h>`
[ wcstolwcstoll](<#/doc/string/wide/wcstol>)(C95)(C99) | converte uma string larga para um valor inteiro
(função)
[ wcstoulwcstoull](<#/doc/string/wide/wcstoul>)(C95)(C99) | converte uma string larga para um valor inteiro sem sinal
(função)
[ wcstofwcstodwcstold](<#/doc/string/wide/wcstof>)(C99)(C95)(C99) | converte uma string larga para um valor de ponto flutuante
(função)
Definido no cabeçalho `[`<inttypes.h>`](<#/doc/types/integer>)`
[ wcstoimaxwcstoumax](<#/doc/string/wide/wcstoimax>)(C99)(C99) | converte uma string larga para [intmax_t](<#/doc/types/integer>) ou [uintmax_t](<#/doc/types/integer>)
(função)

##### Manipulação de strings

---
Definido no cabeçalho `<wchar.h>`
[ wcscpywcscpy_s](<#/doc/string/wide/wcscpy>)(C95)(C11) | copia uma string larga para outra
(função)
[ wcsncpywcsncpy_s](<#/doc/string/wide/wcsncpy>)(C95)(C11) | copia uma certa quantidade de caracteres largos de uma string para outra
(função)
[ wcscatwcscat_s](<#/doc/string/wide/wcscat>)(C95)(C11) | anexa uma cópia de uma string larga a outra
(função)
[ wcsncatwcsncat_s](<#/doc/string/wide/wcsncat>)(C95)(C11) | anexa uma certa quantidade de caracteres largos de uma string larga a outra
(função)
[ wcsxfrm](<#/doc/string/wide/wcsxfrm>)(C95) | transforma uma string larga para que wcscmp produza o mesmo resultado que wcscoll
(função)

##### Exame de strings

Definido no cabeçalho `<wchar.h>`
[ wcslenwcsnlen_s](<#/doc/string/wide/wcslen>)(C95)(C11) | retorna o comprimento de uma string larga
(função)
[ wcscmp](<#/doc/string/wide/wcscmp>)(C95) | compara duas strings largas
(função)
[ wcsncmp](<#/doc/string/wide/wcsncmp>)(C95) | compara uma certa quantidade de caracteres de duas strings largas
(função)
[ wcscoll](<#/doc/string/wide/wcscoll>)(C95) | compara duas strings largas de acordo com o locale atual
(função)
[ wcschr](<#/doc/string/wide/wcschr>)(C95) | encontra a primeira ocorrência de um caractere largo em uma string larga
(função)
[ wcsrchr](<#/doc/string/wide/wcsrchr>)(C95) | encontra a última ocorrência de um caractere largo em uma string larga
(função)
[ wcsspn](<#/doc/string/wide/wcsspn>)(C95) | retorna o comprimento do segmento inicial máximo que consiste
apenas nos caracteres largos encontrados em outra string larga
(função)
[ wcscspn](<#/doc/string/wide/wcscspn>)(C95) | retorna o comprimento do segmento inicial máximo que consiste
apenas nos caracteres largos _não_ encontrados em outra string larga
(função)
[ wcspbrk](<#/doc/string/wide/wcspbrk>)(C95) | encontra a primeira localização de qualquer caractere largo em uma string larga, em outra string larga
(função)
[ wcsstr](<#/doc/string/wide/wcsstr>)(C95) | encontra a primeira ocorrência de uma string larga dentro de outra string larga
(função)
[ wcstokwcstok_s](<#/doc/string/wide/wcstok>)(C95)(C11) | encontra o próximo token em uma string larga
(função)

##### Manipulação de arrays de caracteres largos

---
Definido no cabeçalho `<wchar.h>`
[ wmemcpywmemcpy_s](<#/doc/string/wide/wmemcpy>)(C95)(C11) | copia uma certa quantidade de caracteres largos entre dois arrays não sobrepostos
(função)
[ wmemmovewmemmove_s](<#/doc/string/wide/wmemmove>)(C95)(C11) | copia uma certa quantidade de caracteres largos entre dois arrays, possivelmente sobrepostos
(função)
[ wmemcmp](<#/doc/string/wide/wmemcmp>)(C95) | compara uma certa quantidade de caracteres largos de dois arrays
(função)
[ wmemchr](<#/doc/string/wide/wmemchr>)(C95) | encontra a primeira ocorrência de um caractere largo em um array de caracteres largos
(função)
[ wmemset](<#/doc/string/wide/wmemset>)(C95) | copia o caractere largo fornecido para cada posição em um array de caracteres largos
(função)

### Tipos

Definido no cabeçalho `[`<stddef.h>`](<#/doc/types>)`
---
Definido no cabeçalho `[`<stdlib.h>`](<#/doc/program>)`
Definido no cabeçalho `<wchar.h>`
wchar_t | tipo inteiro que pode conter qualquer caractere largo válido
(typedef)
Definido no cabeçalho `<wchar.h>`
Definido no cabeçalho `<wctype.h>`
wint_t(C95) | tipo inteiro que pode conter qualquer caractere largo válido e pelo menos mais um valor
(typedef)
Definido no cabeçalho `<wctype.h>`
wctrans_t(C95) | tipo escalar que contém mapeamento de caracteres específico do locale
(typedef)
wctype_t(C95) | tipo escalar que contém classificação de caracteres específica do locale
(typedef)

### Macros

Definido no cabeçalho `<wchar.h>`
---
Definido no cabeçalho `<wctype.h>`
WEOF(C95) | um valor não-caractere do tipo wint_t usado para indicar erros
(constante de macro)
Definido no cabeçalho `<wchar.h>`
Definido no cabeçalho `[`<stdint.h>`](<#/doc/types/integer>)`
WCHAR_MIN(C95) | o menor valor válido de wchar_t
(constante de macro)
WCHAR_MAX(C95) | o maior valor válido de wchar_t
(constante de macro)

### Referências

* Padrão C23 (ISO/IEC 9899:2024):

  * 7.19 Definições comuns <stddef.h> (p: TBD)

  * 7.29 Utilitários de caracteres multibyte estendidos e largos <wchar.h> (p: TBD)

  * 7.30 Utilitários de classificação e mapeamento de caracteres largos <wctype.h> (p: TBD)

  * 7.31.16 Utilitários de caracteres multibyte estendidos e largos <wchar.h> (p: TBD)

  * 7.31.17 Utilitários de classificação e mapeamento de caracteres largos <wctype.h> (p: TBD)

  * K.3.3 Definições comuns <stddef.h> (p: TBD)

  * K.3.9 Utilitários de caracteres multibyte estendidos e largos <wchar.h> (p: TBD)

* Padrão C17 (ISO/IEC 9899:2018):

  * 7.19 Definições comuns <stddef.h> (p: TBD)

  * 7.29 Utilitários de caracteres multibyte estendidos e largos <wchar.h> (p: TBD)

  * 7.30 Utilitários de classificação e mapeamento de caracteres largos <wctype.h> (p: TBD)

  * 7.31.16 Utilitários de caracteres multibyte estendidos e largos <wchar.h> (p: TBD)

  * 7.31.17 Utilitários de classificação e mapeamento de caracteres largos <wctype.h> (p: TBD)

  * K.3.3 Definições comuns <stddef.h> (p: TBD)

  * K.3.9 Utilitários de caracteres multibyte estendidos e largos <wchar.h> (p: TBD)

* Padrão C11 (ISO/IEC 9899:2011):

  * 7.19 Definições comuns <stddef.h> (p: 288)

  * 7.29 Utilitários de caracteres multibyte estendidos e largos <wchar.h> (p: 402-446)

  * 7.30 Utilitários de classificação e mapeamento de caracteres largos <wctype.h> (p: 447-454)

  * 7.31.16 Utilitários de caracteres multibyte estendidos e largos <wchar.h> (p: 456)

  * 7.31.17 Utilitários de classificação e mapeamento de caracteres largos <wctype.h> (p: 457)

  * K.3.3 Definições comuns <stddef.h> (p: 585)

  * K.3.9 Utilitários de caracteres multibyte estendidos e largos <wchar.h> (p: 627-651)

* Padrão C99 (ISO/IEC 9899:1999):

  * 7.17 Definições comuns <stddef.h> (p: 254)

  * 7.24 Utilitários de caracteres multibyte estendidos e largos <wchar.h> (p: 348-392)

  * 7.25 Utilitários de classificação e mapeamento de caracteres largos <wctype.h> (p: 393-400)

  * 7.26.12 Utilitários de caracteres multibyte estendidos e largos <wchar.h> (p: 402)

  * 7.26.13 Utilitários de classificação e mapeamento de caracteres largos <wctype.h> (p: 402)

* Padrão C89/C90 (ISO/IEC 9899:1990):

  * 4.1.5 Definições comuns <stddef.h>

### Veja também

[Documentação C++](<#/>) para strings largas terminadas em nulo
---