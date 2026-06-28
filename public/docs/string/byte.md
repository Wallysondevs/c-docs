# Strings de bytes terminadas em nulo

Uma string de bytes terminada em nulo (NTBS) é uma sequência de bytes não nulos seguida por um byte com valor zero (o caractere nulo terminador). Cada byte em uma string de bytes codifica um caractere de algum conjunto de caracteres. Por exemplo, o array de caracteres `{'x63','x61','x74','\0'}` é uma NTBS que contém a string "cat" na codificação [ASCII](<#/doc/language/ascii>).

### Funções

##### Classificação de caracteres

---
Definido no cabeçalho `<ctype.h>`
[ isalnum](<#/doc/string/byte/isalnum>) | verifica se um caractere é alfanumérico
(função)
[ isalpha](<#/doc/string/byte/isalpha>) | verifica se um caractere é alfabético
(função)
[ islower](<#/doc/string/byte/islower>) | verifica se um caractere é minúsculo
(função)
[ isupper](<#/doc/string/byte/isupper>) | verifica se um caractere é maiúsculo
(função)
[ isdigit](<#/doc/string/byte/isdigit>) | verifica se um caractere é um dígito
(função)
[ isxdigit](<#/doc/string/byte/isxdigit>) | verifica se um caractere é um caractere hexadecimal
(função)
[ iscntrl](<#/doc/string/byte/iscntrl>) | verifica se um caractere é um caractere de controle
(função)
[ isgraph](<#/doc/string/byte/isgraph>) | verifica se um caractere é um caractere gráfico
(função)
[ isspace](<#/doc/string/byte/isspace>) | verifica se um caractere é um caractere de espaço
(função)
[ isblank](<#/doc/string/byte/isblank>)(desde C99) | verifica se um caractere é um caractere em branco
(função)
[ isprint](<#/doc/string/byte/isprint>) | verifica se um caractere é um caractere imprimível
(função)
[ ispunct](<#/doc/string/byte/ispunct>) | verifica se um caractere é um caractere de pontuação
(função)

##### Manipulação de caracteres

[ tolower](<#/doc/string/byte/tolower>) | converte um caractere para minúsculo
(função)
[ toupper](<#/doc/string/byte/toupper>) | converte um caractere para maiúsculo
(função)

Nota: funções adicionais cujos nomes começam com **to** ou **is**, seguidos por uma letra minúscula, podem ser adicionadas ao cabeçalho `ctype.h` no futuro e não devem ser definidas por programas que incluem esse cabeçalho.

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

##### Conversões de e para formatos numéricos

---
Definido no cabeçalho `[`<stdlib.h>`](<#/doc/program>)`
[ atof](<#/doc/string/byte/atof>) | converte uma string de bytes para um valor de ponto flutuante
(função)
[ atoiatolatoll](<#/doc/string/byte/atoi>)(desde C99) | converte uma string de bytes para um valor inteiro
(função)
[ strtolstrtoll](<#/doc/string/byte/strtol>)(desde C99) | converte uma string de bytes para um valor inteiro
(função)
[ strtoul strtoull](<#/doc/string/byte/strtoul>)(desde C99) | converte uma string de bytes para um valor inteiro sem sinal
(função)
[ strtofstrtodstrtold](<#/doc/string/byte/strtof>)(desde C99)(desde C99) | converte uma string de bytes para um valor de ponto flutuante
(função)
[ strfromfstrfromdstrfroml](<#/doc/string/byte/strfromf>)(C23)(C23)(C23) | converte um valor de ponto flutuante para uma string de bytes
(função)
Definido no cabeçalho `[`<inttypes.h>`](<#/doc/types/integer>)`
[ strtoimaxstrtoumax](<#/doc/string/byte/strtoimax>)(desde C99)(desde C99) | converte uma string de bytes para [intmax_t](<#/doc/types/integer>) ou [uintmax_t](<#/doc/types/integer>)
(função)

##### Manipulação de strings

Definido no cabeçalho `<string.h>`
[ strcpystrcpy_s](<#/doc/string/byte/strcpy>)(desde C11) | copia uma string para outra
(função)
[ strncpystrncpy_s](<#/doc/string/byte/strncpy>)(desde C11) | copia uma certa quantidade de caracteres de uma string para outra
(função)
[ strcatstrcat_s](<#/doc/string/byte/strcat>)(desde C11) | concatena duas strings
(função)
[ strncatstrncat_s](<#/doc/string/byte/strncat>)(desde C11) | concatena uma certa quantidade de caracteres de duas strings
(função)
[ strxfrm](<#/doc/string/byte/strxfrm>) | transforma uma string para que strcmp produza o mesmo resultado que strcoll
(função)
[ strdup](<#/doc/string/byte/strdup>)(C23) | aloca uma cópia de uma string
(função)
[ strndup](<#/doc/string/byte/strndup>)(C23) | aloca uma cópia de uma string de tamanho especificado
(função)

##### Análise de strings

Definido no cabeçalho `<string.h>`
[ strlenstrnlen_s](<#/doc/string/byte/strlen>)(desde C11) | retorna o comprimento de uma dada string
(função)
[ strcmp](<#/doc/string/byte/strcmp>) | compara duas strings
(função)
[ strncmp](<#/doc/string/byte/strncmp>) | compara uma certa quantidade de caracteres de duas strings
(função)
[ strcoll](<#/doc/string/byte/strcoll>) | compara duas strings de acordo com a localidade atual
(função)
[ strchr](<#/doc/string/byte/strchr>) | encontra a primeira ocorrência de um caractere
(função)
[ strrchr](<#/doc/string/byte/strrchr>) | encontra a última ocorrência de um caractere
(função)
[ strspn](<#/doc/string/byte/strspn>) | retorna o comprimento do segmento inicial máximo que consiste apenas nos caracteres encontrados em outra string de bytes
(função)
[ strcspn](<#/doc/string/byte/strcspn>) | retorna o comprimento do segmento inicial máximo que consiste apenas nos caracteres não encontrados em outra string de bytes
(função)
[ strpbrk](<#/doc/string/byte/strpbrk>) | encontra a primeira ocorrência de qualquer caractere de uma string, em outra string
(função)
[ strstr](<#/doc/string/byte/strstr>) | encontra a primeira ocorrência de uma substring de caracteres
(função)
[ strtokstrtok_s](<#/doc/string/byte/strtok>)(desde C11) | encontra o próximo token em uma string de bytes
(função)

##### Manipulação de arrays de caracteres

Definido no cabeçalho `<string.h>`
[ memchr](<#/doc/string/byte/memchr>) | procura em um array a primeira ocorrência de um caractere
(função)
[ memcmp](<#/doc/string/byte/memcmp>) | compara dois buffers
(função)
[ memsetmemset_explicitmemset_s](<#/doc/string/byte/memset>)(C23)(desde C11) | preenche um buffer com um caractere
(função)
[ memcpymemcpy_s](<#/doc/string/byte/memcpy>)(desde C11) | copia um buffer para outro
(função)
[ memmovememmove_s](<#/doc/string/byte/memmove>)(desde C11) | move um buffer para outro
(função)
[ memccpy](<#/doc/string/byte/memccpy>)(C23) | copia um buffer para outro, parando após o delimitador especificado
(função)

##### Diversos

Definido no cabeçalho `<string.h>`
[ strerrorstrerror_sstrerrorlen_s](<#/doc/string/byte/strerror>)(desde C11)(desde C11) | retorna uma versão textual de um dado código de erro
(função)

### Referências

Conteúdo estendido
---

*   Padrão C23 (ISO/IEC 9899:2024):

    *   7.4 Manipulação de caracteres <ctype.h> (p: TBD)

    *   7.8 Conversão de formato de tipos inteiros <inttypes.h> (p: TBD)

    *   7.22 Utilitários gerais <stdlib.h> (p: TBD)

    *   7.24 Manipulação de strings <string.h> (p: TBD)

    *   7.31.2 Manipulação de caracteres <ctype.h> (p: TBD)

    *   7.31.5 Conversão de formato de tipos inteiros <inttypes.h> (p: TBD)

    *   7.31.12 Utilitários gerais <stdlib.h> (p: TBD)

    *   7.31.13 Manipulação de strings <string.h> (p: TBD)

    *   K.3.6 Utilitários gerais <stdlib.h> (p: TBD)

    *   K.3.7 Manipulação de strings <string.h> (p: TBD)

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.4 Manipulação de caracteres <ctype.h> (p: TBD)

    *   7.8 Conversão de formato de tipos inteiros <inttypes.h> (p: TBD)

    *   7.22 Utilitários gerais <stdlib.h> (p: TBD)

    *   7.24 Manipulação de strings <string.h> (p: TBD)

    *   7.31.2 Manipulação de caracteres <ctype.h> (p: TBD)

    *   7.31.5 Conversão de formato de tipos inteiros <inttypes.h> (p: TBD)

    *   7.31.12 Utilitários gerais <stdlib.h> (p: TBD)

    *   7.31.13 Manipulação de strings <string.h> (p: TBD)

    *   K.3.6 Utilitários gerais <stdlib.h> (p: TBD)

    *   K.3.7 Manipulação de strings <string.h> (p: TBD)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.4 Manipulação de caracteres <ctype.h> (p: 200-204)

    *   7.8 Conversão de formato de tipos inteiros <inttypes.h> (p: 217-220)

    *   7.22 Utilitários gerais <stdlib.h> (p: 340-360)

    *   7.24 Manipulação de strings <string.h> (p: 362-372)

    *   7.31.2 Manipulação de caracteres <ctype.h> (p: 455)

    *   7.31.5 Conversão de formato de tipos inteiros <inttypes.h> (p: 455)

    *   7.31.12 Utilitários gerais <stdlib.h> (p: 456)

    *   7.31.13 Manipulação de strings <string.h> (p: 456)

    *   K.3.6 Utilitários gerais <stdlib.h> (p: 604-613)

    *   K.3.7 Manipulação de strings <string.h> (p: 614-623)

*   Padrão C99 (ISO/IEC 9899:1999):

    *   7.4 Manipulação de caracteres <ctype.h> (p: 181-185)

    *   7.8 Conversão de formato de tipos inteiros <inttypes.h> (p: 198-201)

    *   7.20 Utilitários gerais <stdlib.h> (p: 306-324)

    *   7.21 Manipulação de strings <string.h> (p: 325-334)

    *   7.26.2 Manipulação de caracteres <ctype.h> (p: 401)

    *   7.26.4 Conversão de formato de tipos inteiros <inttypes.h> (p: 401)

    *   7.26.10 Utilitários gerais <stdlib.h> (p: 402)

    *   7.26.11 Manipulação de strings <string.h> (p: 402)

*   Padrão C89/C90 (ISO/IEC 9899:1990):

    *   4.3 MANIPULAÇÃO DE CARACTERES <ctype.h>

    *   4.10 UTILITÁRIOS GERAIS <stdlib.h>

    *   4.11 MANIPULAÇÃO DE STRINGS <string.h>

    *   4.13.2 Manipulação de caracteres <ctype.h>

    *   4.13.7 Utilitários gerais <stdlib.h>

    *   4.13.8 Manipulação de strings <string.h>

### Veja também

[Documentação C++](<#/>) para strings de bytes terminadas em nulo
---