# nearbyint, nearbyintf, nearbyintl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float nearbyintf( float arg );  // desde C99
double nearbyint( double arg );  // desde C99
long double nearbyintl( long double arg );  // desde C99
Definido no cabeçalho `<tgmath.h>`
#define nearbyint( arg )  // desde C99
```

1-3) Arredonda o argumento de ponto flutuante `arg` para um valor inteiro em formato de ponto flutuante, usando o [modo de arredondamento atual](<#/doc/numeric/fenv/FE_round>).

4) Macro genérica de tipo: Se `arg` tiver o tipo `long double`, `nearbyintl` é chamada. Caso contrário, se `arg` tiver um tipo inteiro ou o tipo `double`, `nearbyint` é chamada. Caso contrário, `nearbyintf` é chamada, respectivamente.

### Parâmetros

- **arg** — valor de ponto flutuante

### Valor de retorno

O valor inteiro mais próximo de `arg`, de acordo com o [modo de arredondamento atual](<#/doc/numeric/fenv/FE_round>), é retornado.

### Tratamento de erros

Esta função não está sujeita a nenhum dos erros especificados em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559),

*   [FE_INEXACT](<#/doc/numeric/fenv/FE_exceptions>) nunca é levantada.
*   Se `arg` for ±∞, é retornado, sem modificação.
*   Se `arg` for ±0, é retornado, sem modificação.
*   Se `arg` for NaN, NaN é retornado.

### Observações

A única diferença entre `nearbyint` e [rint](<#/doc/numeric/math/rint>) é que `nearbyint` nunca levanta [FE_INEXACT](<#/doc/numeric/fenv/FE_exceptions>).

Os maiores valores de ponto flutuante representáveis são inteiros exatos em todos os formatos de ponto flutuante padrão, portanto `nearbyint` nunca causa estouro por si só; entretanto, o resultado pode causar estouro em qualquer tipo inteiro (incluindo [intmax_t](<#/doc/types/integer>)), quando armazenado em uma variável inteira.

Se o modo de arredondamento atual for [FE_TONEAREST](<#/doc/numeric/fenv/FE_round>), esta função arredonda para o número par mais próximo em casos de "meio-termo" (como [rint](<#/doc/numeric/math/rint>), mas diferente de [round](<#/doc/numeric/math/round>)).

### Exemplo

Execute este código
```c
    #include <fenv.h>
    #include <math.h>
    #include <stdio.h>
     
    int main(void)
    {
    // #pragma STDC FENV_ACCESS ON
        fesetround(FE_TONEAREST);
        printf("rounding to nearest:\nnearbyint(+2.3) = %+.1f  ", nearbyint(2.3));
        printf("nearbyint(+2.5) = %+.1f  ", nearbyint(2.5));
        printf("nearbyint(+3.5) = %+.1f\n", nearbyint(3.5));
        printf("nearbyint(-2.3) = %+.1f  ", nearbyint(-2.3));
        printf("nearbyint(-2.5) = %+.1f  ", nearbyint(-2.5));
        printf("nearbyint(-3.5) = %+.1f\n", nearbyint(-3.5));
     
        fesetround(FE_DOWNWARD);
        printf("rounding down: \nnearbyint(+2.3) = %+.1f  ", nearbyint(2.3));
        printf("nearbyint(+2.5) = %+.1f  ", nearbyint(2.5));
        printf("nearbyint(+3.5) = %+.1f\n", nearbyint(3.5));
        printf("nearbyint(-2.3) = %+.1f  ", nearbyint(-2.3));
        printf("nearbyint(-2.5) = %+.1f  ", nearbyint(-2.5));
        printf("nearbyint(-3.5) = %+.1f\n", nearbyint(-3.5));
     
        printf("nearbyint(-0.0) = %+.1f\n", nearbyint(-0.0));
        printf("nearbyint(-Inf) = %+.1f\n", nearbyint(-INFINITY));
    }
```

Saída:
```
    rounding to nearest:
    nearbyint(+2.3) = +2.0  nearbyint(+2.5) = +2.0  nearbyint(+3.5) = +4.0
    nearbyint(-2.3) = -2.0  nearbyint(-2.5) = -2.0  nearbyint(-3.5) = -4.0
    rounding down:
    nearbyint(+2.3) = +2.0  nearbyint(+2.5) = +2.0  nearbyint(+3.5) = +3.0
    nearbyint(-2.3) = -3.0  nearbyint(-2.5) = -3.0  nearbyint(-3.5) = -4.0
    nearbyint(-0.0) = -0.0
    nearbyint(-Inf) = -inf
```

### Referências

*   Padrão C23 (ISO/IEC 9899:2024):

    *   7.12.9.3 As funções nearbyint (p: TBD)

    *   7.25 Matemática genérica de tipo <tgmath.h> (p: TBD)

    *   F.10.6.3 As funções nearbyint (p: TBD)

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.12.9.3 As funções nearbyint (p: TBD)

    *   7.25 Matemática genérica de tipo <tgmath.h> (p: TBD)

    *   F.10.6.3 As funções nearbyint (p: TBD)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.12.9.3 As funções nearbyint (p: 251-252)

    *   7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    *   F.10.6.3 As funções nearbyint (p: 526)

*   Padrão C99 (ISO/IEC 9899:1999):

    *   7.12.9.3 As funções nearbyint (p: 232)

    *   7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337)

    *   F.9.6.3 As funções nearbyint (p: 463)

### Veja também

[ rintrintfrintllrintlrintflrintlllrintllrintfllrintl](<#/doc/numeric/math/rint>)(C99)(C99)(C99)(C99)(C99)(C99)(C99)(C99)(C99) | arredonda para um inteiro usando o modo de arredondamento atual com exceção se o resultado for diferente
(função)
[ roundroundfroundllroundlroundflroundlllroundllroundfllroundl](<#/doc/numeric/math/round>)(C99)(C99)(C99)(C99)(C99)(C99)(C99)(C99)(C99) | arredonda para o inteiro mais próximo, arredondando para longe de zero em casos de "meio-termo"
(função)
[ fegetroundfesetround](<#/doc/numeric/fenv/feround>)(C99)(C99) | obtém ou define a direção de arredondamento
(função)
[Documentação C++](<#/>) para nearbyint