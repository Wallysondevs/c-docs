# Numéricos

A biblioteca numérica do C inclui funções e tipos matemáticos comuns, bem como suporte para geração de números aleatórios.

### [Funções matemáticas comuns](<#/doc/numeric/math>)

O cabeçalho [`<math.h>`](<#/doc/numeric/math>) fornece [funções matemáticas da biblioteca padrão do C](<#/doc/numeric/math>) como [fabs](<#/doc/numeric/math/fabs>), [sqrt](<#/doc/numeric/math/sqrt>), e [sin](<#/doc/numeric/math/sin>).

### [Ambiente de ponto flutuante](<#/doc/numeric/fenv>)

O cabeçalho [`<fenv.h>`](<#/doc/numeric/fenv>) define [flags e funções relacionadas ao estado excepcional de ponto flutuante](<#/doc/numeric/fenv>), como overflow e divisão por zero.

### [Geração de números pseudoaleatórios](<#/doc/numeric/random>)

O cabeçalho [`<stdlib.h>`](<#/doc/program>) também inclui geração de números aleatórios no estilo C via [srand](<#/doc/numeric/random/srand>) e [rand](<#/doc/numeric/random/rand>).

### [Aritmética de números complexos](<#/doc/numeric/complex>)

O cabeçalho [`<complex.h>`](<#/doc/numeric/complex>) fornece tipos e funções para trabalhar com [números complexos](<#/doc/numeric/complex>).

### [Matemática genérica por tipo](<#/doc/numeric/tgmath>)

O cabeçalho [`<tgmath.h>`](<#/doc/numeric/tgmath>) fornece algumas macros para uma função que nomeia XXX:

  * função real:

  * variante float `XXXf`
  * variante double `XXX`
  * variante long double `XXXl`

  * função complexa:

  * variante float `cXXXf`
  * variante double `cXXX`
  * variante long double `cXXXl`

### [Manipulação de bits](<#/doc/numeric/bit_manip>) (desde C23)

O cabeçalho [`<stdbit.h>`](<#/doc/numeric>) fornece macros e funções para trabalhar com a [ordenação de bytes](<#/doc/numeric/bit_manip>) e a [representação de bytes e bits](<#/doc/numeric/bit_manip>) de objetos C.

### Aritmética de inteiros verificada (desde C23)

Fornece algumas [macros genéricas por tipo](<#/doc/language/generic>) para aritmética de inteiros verificada:

Definido no cabeçalho `[`<stdckdint.h>`](<#/doc/numeric>)`
---
[ ckd_add](<#/doc/numeric/ckd_add>)(C23) | operação de adição verificada em dois inteiros
(macro de função genérica por tipo)
[ ckd_sub](<#/doc/numeric/ckd_sub>)(C23) | operação de subtração verificada em dois inteiros
(macro de função genérica por tipo)
[ ckd_mul](<#/doc/numeric/ckd_mul>)(C23) | operação de multiplicação verificada em dois inteiros
(macro de função genérica por tipo)

### Veja também

[Documentação C++](<#/>) para a biblioteca Numéricos
---