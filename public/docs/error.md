# Tratamento de erros

### Números de erro

Definido no cabeçalho `<errno.h>`
---
[ errno](<#/doc/error/errno>) | macro que se expande para uma variável de número de erro thread-local compatível com POSIX
(variável macro)
[ E2BIG, EACCES, ..., EXDEV](<#/doc/error/errno_macros>) | macros para condições de erro padrão compatíveis com POSIX
(constante macro)

### Asserções

Definido no cabeçalho `<assert.h>`
---
[ assert](<#/doc/error/assert>) | aborta o programa se a condição especificada pelo usuário não for verdadeira. Pode ser desabilitado para builds de lançamento
(macro de função)
[ static_assert](<#/doc/error/static_assert>)(C11)(removido em C23) | emite um diagnóstico em tempo de compilação se o valor de uma expressão constante for falso
(macro de palavra-chave)

### Verificação de limites

A biblioteca padrão fornece versões com verificação de limites de algumas funções existentes ([gets_s](<#/doc/io/gets>), [fopen_s](<#/doc/io/fopen>), [printf_s](<#/doc/io/fprintf>), [strcpy_s](<#/doc/string/byte/strcpy>), [wcscpy_s](<#/doc/string/wide/wcscpy>), [mbstowcs_s](<#/doc/string/multibyte/mbstowcs>), [qsort_s](<#/doc/algorithm/qsort>), [getenv_s](<#/doc/program/getenv>), etc). Esta funcionalidade é _opcional_ e está disponível apenas se `__STDC_LIB_EXT1__` for definido. As seguintes macros e funções suportam esta funcionalidade.
---
Definido no cabeçalho `<errno.h>`
Definido no cabeçalho `[`<stdio.h>`](<#/doc/io>)`
errno_t(C11) | um typedef para o tipo `int`, usado para auto-documentar funções que retornam valores de [errno](<#/doc/error/errno>)
(typedef)
Definido no cabeçalho `[`<stddef.h>`](<#/doc/types>)`
Definido no cabeçalho `[`<stdio.h>`](<#/doc/io>)`
Definido no cabeçalho `[`<stdlib.h>`](<#/doc/program>)`
Definido no cabeçalho `[`<string.h>`](<#/doc/string/byte>)`
Definido no cabeçalho `[`<time.h>`](<#/doc/chrono>)`
Definido no cabeçalho `[`<wchar.h>`](<#/doc/string/wide>)`
rsize_t(C11) | um typedef para o mesmo tipo que [size_t](<#/doc/types/size_t>), usado para auto-documentar funções que verificam os limites de seus parâmetros em tempo de execução
(typedef)
Definido no cabeçalho `[`<stdint.h>`](<#/doc/types/integer>)`
RSIZE_MAX(C11) | maior tamanho aceitável para funções com verificação de limites, expande-se para uma constante ou variável que pode mudar em tempo de execução (por exemplo, conforme o tamanho da memória atualmente alocada muda)
(variável macro)
Definido no cabeçalho `[`<stdlib.h>`](<#/doc/program>)`
[ set_constraint_handler_s](<#/doc/error/set_constraint_handler_s>)(C11) | define o callback de erro para funções com verificação de limites
(função)
[ abort_handler_s](<#/doc/error/abort_handler_s>)(C11) | callback de aborto para as funções com verificação de limites
(função)
[ ignore_handler_s](<#/doc/error/ignore_handler_s>)(C11) | callback de ignorar para as funções com verificação de limites
(função)

Nota: implementações de funções com verificação de limites estão disponíveis como bibliotecas de código aberto [Safe C](<https://github.com/rurban/safeclib/>) e [Slibc](<https://code.google.com/archive/p/slibc/>), e como parte do Watcom C. Há também um conjunto incompatível de funções com verificação de limites disponível no Visual Studio.

(desde C11)

### Notas

Desde C23, [`static_assert`](<#/doc/language/static_assert>) é uma palavra-chave em si, que também pode ser uma macro predefinida, então `<assert.h>` não a fornece mais.

### Referências

Conteúdo estendido
---

*   C23 standard (ISO/IEC 9899:2024):
    *   7.2 Diagnostics <assert.h> (pág: TBD)
    *   7.5 Errors <errno.h> (pág: TBD)
    *   7.19 Common definitions <stddef.h> (pág: TBD)
    *   7.20 Integer types <stdint.h> (pág: TBD)
    *   7.21 Input/output <stdio.h> (pág: TBD)
    *   7.22 General utilities <stdlib.h> (pág: TBD)
    *   K.3.1.3 Use of errno (pág: TBD)
    *   K.3.2/2 errno_t (pág: TBD)
    *   K.3.3/2 rsize_t (pág: TBD)
    *   K.3.4/2 RSIZE_MAX (pág: TBD)
    *   7.31.3 Errors <errno.h> (pág: TBD)
    *   7.31.10 Integer types <stdint.h> (pág: TBD)
    *   7.31.11 Input/output <stdio.h> (pág: TBD)
    *   7.31.12 General utilities <stdlib.h> (pág: TBD)

*   C17 standard (ISO/IEC 9899:2018):
    *   7.2 Diagnostics <assert.h> (pág: TBD)
    *   7.5 Errors <errno.h> (pág: TBD)
    *   7.19 Common definitions <stddef.h> (pág: TBD)
    *   7.20 Integer types <stdint.h> (pág: TBD)
    *   7.21 Input/output <stdio.h> (pág: TBD)
    *   7.22 General utilities <stdlib.h> (pág: TBD)
    *   K.3.1.3 Use of errno (pág: TBD)
    *   K.3.2/2 errno_t (pág: TBD)
    *   K.3.3/2 rsize_t (pág: TBD)
    *   K.3.4/2 RSIZE_MAX (pág: TBD)
    *   7.31.3 Errors <errno.h> (pág: TBD)
    *   7.31.10 Integer types <stdint.h> (pág: TBD)
    *   7.31.11 Input/output <stdio.h> (pág: TBD)
    *   7.31.12 General utilities <stdlib.h> (pág: TBD)

*   C11 standard (ISO/IEC 9899:2011):
    *   7.2 Diagnostics <assert.h> (pág: 186-187)
    *   7.5 Errors <errno.h> (pág: 205)
    *   7.19 Common definitions <stddef.h> (pág: 288)
    *   7.20 Integer types <stdint.h> (pág: 289-295)
    *   7.21 Input/output <stdio.h> (pág: 296-339)
    *   7.22 General utilities <stdlib.h> (pág: 340-360)
    *   K.3.1.3 Use of errno (pág: 584)
    *   K.3.2/2 errno_t (pág: 585)
    *   K.3.3/2 rsize_t (pág: 585)
    *   K.3.4/2 RSIZE_MAX (pág: 585)
    *   7.31.3 Errors <errno.h> (pág: 455)
    *   7.31.10 Integer types <stdint.h> (pág: 456)
    *   7.31.11 Input/output <stdio.h> (pág: 456)
    *   7.31.12 General utilities <stdlib.h> (pág: 456)

*   C99 standard (ISO/IEC 9899:1999):
    *   7.2 Diagnostics <assert.h> (pág: 169)
    *   7.5 Errors <errno.h> (pág: 186)
    *   7.26.3 Errors <errno.h> (pág: 401)
    *   7.26.8 Integer types <stdint.h> (pág: 401)
    *   7.26.9 Input/output <stdio.h> (pág: 402)
    *   7.26.10 General utilities <stdlib.h> (pág: 402)

*   C89/C90 standard (ISO/IEC 9899:1990):
    *   4.2 DIAGNOSTICS <assert.h>
    *   4.1.3 Errors <errno.h>
    *   4.13.1 Errors <errno.h>
    *   4.13.6 Input/output <stdio.h>
    *   4.13.7 General utilities <stdlib.h>

### Veja também

[ math_errhandlingMATH_ERRNOMATH_ERREXCEPT](<#/doc/numeric/math/math_errhandling>)(C99)(C99)(C99) | define o mecanismo de tratamento de erros usado pelas funções matemáticas comuns
(constante macro)
[Documentação C++](<#/>) para Tratamento de erros