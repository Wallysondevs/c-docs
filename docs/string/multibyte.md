# Strings multibyte terminadas em nulo

Uma string multibyte terminada em nulo (NTMBS), ou "string multibyte", é uma sequência de bytes não nulos seguida por um byte com valor zero (o caractere nulo de terminação).

Cada caractere armazenado na string pode ocupar mais de um byte. A codificação usada para representar caracteres em uma string de caracteres multibyte é específica da localidade: pode ser UTF-8, GB18030, EUC-JP, Shift-JIS, etc. Por exemplo, o array de char {'\xe4','\xbd','\xa0','\xe5','\xa5','\xbd','\0'} é uma NTMBS contendo a string "你好" na codificação multibyte UTF-8: os primeiros três bytes codificam o caractere 你, os próximos três bytes codificam o caractere 好. A mesma string codificada em GB18030 é o array de char {'\xc4', '\xe3', '\xba', '\xc3', '\0'}, onde cada um dos dois caracteres é codificado como uma sequência de dois bytes.

Em algumas codificações multibyte, qualquer sequência de caracteres multibyte pode representar caracteres diferentes dependendo das sequências de bytes anteriores, conhecidas como "sequências de mudança de estado". Tais codificações são conhecidas como dependentes de estado: o conhecimento do estado de mudança de estado atual é necessário para interpretar cada caractere. Uma NTMBS é válida apenas se começar e terminar no estado de mudança de estado inicial: se uma sequência de mudança de estado foi usada, a sequência de restauração de estado correspondente deve estar presente antes do caractere nulo de terminação. Exemplos de tais codificações são BOCU-1 e [SCSU](<https://www.unicode.org/reports/tr6>).

Uma string de caracteres multibyte é compatível em layout com [string de bytes terminada em nulo](<#/doc/string/byte>) (NTBS), ou seja, pode ser armazenada, copiada e examinada usando as mesmas facilidades, exceto para o cálculo do número de caracteres. Se a localidade correta estiver em vigor, as funções de E/S também manipulam strings multibyte. Strings multibyte podem ser convertidas de e para wide strings usando as seguintes funções de conversão dependentes da localidade:

### Funções

##### Conversões de caracteres multibyte/wide

---
Definido no cabeçalho `[`<stdlib.h>`](<#/doc/program>)`
[ mblen](<#/doc/string/multibyte/mblen>) | retorna o número de bytes no próximo caractere multibyte
(função)
[ mbtowc](<#/doc/string/multibyte/mbtowc>) | converte o próximo caractere multibyte para wide character
(função)
[ wctombwctomb_s](<#/doc/string/multibyte/wctomb>)(C11) | converte um wide character para sua representação multibyte
(função)
[ mbstowcsmbstowcs_s](<#/doc/string/multibyte/mbstowcs>)(C11) | converte uma string de caracteres multibyte estreita para wide string
(função)
[ wcstombswcstombs_s](<#/doc/string/multibyte/wcstombs>)(C11) | converte uma wide string para string de caracteres multibyte estreita
(função)
Definido no cabeçalho `[`<wchar.h>`](<#/doc/string/wide>)`
[ mbsinit](<#/doc/string/multibyte/mbsinit>)(desde C95) | verifica se o objeto mbstate_t representa o estado de mudança de estado inicial
(função)
[ btowc](<#/doc/string/multibyte/btowc>)(desde C95) | expande um caractere estreito de byte único para wide character, se possível
(função)
[ wctob](<#/doc/string/multibyte/wctob>)(desde C95) | restringe um wide character para um caractere estreito de byte único, se possível
(função)
[ mbrlen](<#/doc/string/multibyte/mbrlen>)(desde C95) | retorna o número de bytes no próximo caractere multibyte, dado o estado
(função)
[ mbrtowc](<#/doc/string/multibyte/mbrtowc>)(desde C95) | converte o próximo caractere multibyte para wide character, dado o estado
(função)
[ wcrtombwcrtomb_s](<#/doc/string/multibyte/wcrtomb>)(desde C95)(C11) | converte um wide character para sua representação multibyte, dado o estado
(função)
[ mbsrtowcsmbsrtowcs_s](<#/doc/string/multibyte/mbsrtowcs>)(desde C95)(C11) | converte uma string de caracteres multibyte estreita para wide string, dado o estado
(função)
[ wcsrtombswcsrtombs_s](<#/doc/string/multibyte/wcsrtombs>)(desde C95)(C11) | converte uma wide string para string de caracteres multibyte estreita, dado o estado
(função)
Definido no cabeçalho `<uchar.h>`
[ mbrtoc8](<#/doc/string/multibyte/mbrtoc8>)(C23) | converte um caractere multibyte estreito para codificação UTF-8
(função)
[ c8rtomb](<#/doc/string/multibyte/c8rtomb>)(C23) | converte uma string UTF-8 para codificação multibyte estreita
(função)
[ mbrtoc16](<#/doc/string/multibyte/mbrtoc16>)(C11) | converte um caractere multibyte estreito para codificação UTF-16
(função)
[ c16rtomb](<#/doc/string/multibyte/c16rtomb>)(C11) | converte um caractere UTF-16 para codificação multibyte estreita
(função)
[ mbrtoc32](<#/doc/string/multibyte/mbrtoc32>)(C11) | converte um caractere multibyte estreito para codificação UTF-32
(função)
[ c32rtomb](<#/doc/string/multibyte/c32rtomb>)(C11) | converte um caractere UTF-32 para codificação multibyte estreita
(função)

### Tipos

Definido no cabeçalho `[`<wchar.h>`](<#/doc/string/wide>)`
---
[ mbstate_t](<#/doc/string/multibyte/mbstate_t>)(desde C95) | informações de estado de conversão necessárias para iterar strings de caracteres multibyte
(classe)
Definido no cabeçalho `<uchar.h>`
[ char8_t](<#/doc/string/multibyte/char8_t>)(C23) | tipo de caractere de 8 bits
(typedef)
[ char16_t](<#/doc/string/multibyte/char16_t>)(C11) | tipo de caractere de 16 bits
(typedef)
[ char32_t](<#/doc/string/multibyte/char32_t>)(C11) | tipo de caractere de 32 bits
(typedef)

### Macros

Definido no cabeçalho `[`<limits.h>`](<#/doc/types/limits>)`
---
MB_LEN_MAX | número máximo de bytes em um caractere multibyte, para qualquer localidade suportada
(constante de macro)
Definido no cabeçalho `[`<stdlib.h>`](<#/doc/program>)`
MB_CUR_MAX | número máximo de bytes em um caractere multibyte, na localidade atual
(variável de macro)

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.10 Tamanhos de tipos inteiros <limits.h> (p: TBD)

    

  * 7.22 Utilitários gerais <stdlib.h> (p: TBD)

    

  * 7.28 Utilitários Unicode <uchar.h> (p: TBD)

    

  * 7.29 Utilitários estendidos de caracteres multibyte e wide <wchar.h> (p: TBD)

    

  * 7.31.12 Utilitários gerais <stdlib.h> (p: TBD)

    

  * 7.31.16 Utilitários estendidos de caracteres multibyte e wide <wchar.h> (p: TBD)

    

  * K.3.6 Utilitários gerais <stdlib.h> (p: TBD)

    

  * K.3.9 Utilitários estendidos de caracteres multibyte e wide <wchar.h> (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.10 Tamanhos de tipos inteiros <limits.h> (p: TBD)

    

  * 7.22 Utilitários gerais <stdlib.h> (p: TBD)

    

  * 7.28 Utilitários Unicode <uchar.h> (p: TBD)

    

  * 7.29 Utilitários estendidos de caracteres multibyte e wide <wchar.h> (p: TBD)

    

  * 7.31.12 Utilitários gerais <stdlib.h> (p: TBD)

    

  * 7.31.16 Utilitários estendidos de caracteres multibyte e wide <wchar.h> (p: TBD)

    

  * K.3.6 Utilitários gerais <stdlib.h> (p: TBD)

    

  * K.3.9 Utilitários estendidos de caracteres multibyte e wide <wchar.h> (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.10 Tamanhos de tipos inteiros <limits.h> (p: 222)

    

  * 7.22 Utilitários gerais <stdlib.h> (p: 340-360)

    

  * 7.28 Utilitários Unicode <uchar.h> (p: 398-401)

    

  * 7.29 Utilitários estendidos de caracteres multibyte e wide <wchar.h> (p: 402-446)

    

  * 7.31.12 Utilitários gerais <stdlib.h> (p: 456)

    

  * 7.31.16 Utilitários estendidos de caracteres multibyte e wide <wchar.h> (p: 456)

    

  * K.3.6 Utilitários gerais <stdlib.h> (p: 604-614)

    

  * K.3.9 Utilitários estendidos de caracteres multibyte e wide <wchar.h> (p: 627-651)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.10 Tamanhos de tipos inteiros <limits.h> (p: 203)

    

  * 7.20 Utilitários gerais <stdlib.h> (p: 306-324)

    

  * 7.24 Utilitários estendidos de caracteres multibyte e wide <wchar.h> (p: 348-392)

    

  * 7.26.10 Utilitários gerais <stdlib.h> (p: 402)

    

  * 7.26.12 Utilitários estendidos de caracteres multibyte e wide <wchar.h> (p: 402)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.1.4 Limites <float.h> e <limits.h>

    

  * 4.10 UTILITÁRIOS GERAIS <stdlib.h>

    

  * 4.13.7 Utilitários gerais <stdlib.h>

### Veja também

[Documentação C++](<#/>) para Strings multibyte terminadas em nulo
---