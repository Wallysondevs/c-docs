# cbrt, cbrtf, cbrtl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float cbrtf( float arg );  // desde C99
double cbrt( double arg );  // desde C99
long double cbrtl( long double arg );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define cbrt( arg )  // desde C99
```

1-3) Calcula a raiz cúbica de `arg`.

4) Macro de tipo genérico: Se `arg` tiver o tipo long double, `cbrtl` é chamada. Caso contrário, se `arg` tiver um tipo inteiro ou o tipo double, `cbrt` é chamada. Caso contrário, `cbrtf` é chamada.

### Parâmetros

- **arg** — valor de ponto flutuante

### Valor de retorno

Se nenhum erro ocorrer, a raiz cúbica de `arg` (\\(\small{\sqrt[3]{arg} }\\)3√arg) é retornada.

Se ocorrer um erro de intervalo devido a underflow, o resultado correto (após arredondamento) é retornado.

### Tratamento de erros

Os erros são relatados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559),

  * se o argumento for ±0 ou ±∞, ele é retornado, inalterado
  * se o argumento for NaN, NaN é retornado.

### Observações

cbrt(arg) não é equivalente a [pow](<#/doc/numeric/math/pow>)(arg, 1.0/3) porque o número racional \\(\small{\frac1{3} }\\)1
---
3
normalmente não é igual a 1.0/3 e std::pow não pode elevar uma base negativa a um expoente fracionário. Além disso, cbrt(arg) geralmente fornece resultados mais precisos do que [pow](<#/doc/numeric/math/pow>)(arg, 1.0/3) (veja o exemplo).

### Exemplo

Execute este código
```c
    #include <float.h>
    #include <math.h>
    #include <stdio.h>
     
    int main(void)
    {
        printf("Normal use:\n"
               "cbrt(729)      = %f\n", cbrt(729));
        printf("cbrt(-0.125)   = %f\n", cbrt(-0.125));
        printf("Special values:\n"
               "cbrt(-0)       = %f\n", cbrt(-0.0));
        printf("cbrt(+inf)     = %f\n", cbrt(INFINITY));
        printf("Accuracy:\n"
               "cbrt(343)      = %.*f\n", DBL_DECIMAL_DIG, cbrt(343));
        printf("pow(343,1.0/3) = %.*f\n", DBL_DECIMAL_DIG, pow(343, 1.0/3));
    }
```

Saída possível:
```
    Normal use:
    cbrt(729)      = 9.000000
    cbrt(-0.125)   = -0.500000
    Special values:
    cbrt(-0)       = -0.000000
    cbrt(+inf)     = inf
    Accuracy:
    cbrt(343)      = 7.00000000000000000
    pow(343,1.0/3) = 6.99999999999999911
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.12.7.1 As funções cbrt (p: TBD)

    

  * 7.25 Matemática de tipo genérico <tgmath.h> (p: TBD)

    

  * F.10.4.1 As funções cbrt (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.12.7.1 As funções cbrt (p: 180-181)

    

  * 7.25 Matemática de tipo genérico <tgmath.h> (p: 272-273)

    

  * F.10.4.1 As funções cbrt (p: 381-)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.12.7.1 As funções cbrt (p: 247)

    

  * 7.25 Matemática de tipo genérico <tgmath.h> (p: 373-375)

    

  * F.10.4.1 As funções cbrt (p: 524)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.12.7.1 As funções cbrt (p: 228)

    

  * 7.22 Matemática de tipo genérico <tgmath.h> (p: 335-337)

    

  * F.9.4.1 As funções cbrt (p: 460)

### Veja também

[ powpowfpowl](<#/doc/numeric/math/pow>)(C99)(C99) | calcula um número elevado à potência dada (\\(\small{x^y}\\)xy)
(função)
[ sqrtsqrtfsqrtl](<#/doc/numeric/math/sqrt>)(C99)(C99) | calcula a raiz quadrada (\\(\small{\sqrt{x} }\\)√x)
(função)
[ hypothypotfhypotl](<#/doc/numeric/math/hypot>)(C99)(C99)(C99) | calcula a raiz quadrada da soma dos quadrados de dois números dados (\\(\scriptsize{\sqrt{x^2+y^2} }\\)√x2
+y2
)
(função)
[documentação C++](<#/>) para cbrt