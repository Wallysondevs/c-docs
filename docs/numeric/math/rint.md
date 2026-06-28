# rint, rintf, rintl, lrint, lrintf, lrintl, llrint, llrintf, llrintl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float rintf( float arg );  // desde C99
double rint( double arg );  // desde C99
long double rintl( long double arg );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define rint( arg )  // desde C99
Definido no cabeçalho ``<math.h>``
long lrintf( float arg );  // desde C99
long lrint( double arg );  // desde C99
long lrintl( long double arg );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define lrint( arg )  // desde C99
Definido no cabeçalho ``<math.h>``
long long llrintf( float arg );  // desde C99
long long llrint( double arg );  // desde C99
long long llrintl( long double arg );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define llrint( arg )  // desde C99
```

1-3) Arredonda o argumento de ponto flutuante `arg` para um valor inteiro em formato de ponto flutuante, usando o modo de arredondamento atual.

5-7, 9-11) Arredonda o argumento de ponto flutuante `arg` para um valor inteiro em formato inteiro, usando o modo de arredondamento atual.

4,8,12) Macros genéricas de tipo: Se `arg` tiver o tipo `long double`, `rintl`, `lrintl`, `llrintl` é chamado. Caso contrário, se `arg` tiver um tipo inteiro ou o tipo `double`, `rint`, `lrint`, `llrint` é chamado. Caso contrário, `rintf`, `lrintf`, `llrintf` é chamado, respectivamente.

### Parâmetros

- **arg** — valor de ponto flutuante

### Valor de retorno

Se nenhum erro ocorrer, o valor inteiro mais próximo de `arg`, de acordo com o [modo de arredondamento atual](<#/doc/numeric/fenv/FE_round>), é retornado.

### Tratamento de erros

Os erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Se o resultado de `lrint` ou `llrint` estiver fora do intervalo representável pelo tipo de retorno, um erro de domínio ou um erro de intervalo pode ocorrer.

Se a implementação suporta aritmética de ponto flutuante IEEE (IEC 60559),

Para a função `rint`:

* Se `arg` for ±∞, ele é retornado, sem modificação.
* Se `arg` for ±0, ele é retornado, sem modificação.
* Se `arg` for NaN, NaN é retornado.

Para as funções `lrint` e `llrint`:

* Se `arg` for ±∞, [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado e um valor definido pela implementação é retornado.
* Se o resultado do arredondamento estiver fora do intervalo do tipo de retorno, [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado e um valor definido pela implementação é retornado.
* Se `arg` for NaN, [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado e um valor definido pela implementação é retornado.

### Notas

[POSIX especifica](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/lrint.html>) que todos os casos em que `lrint` ou `llrint` levantam [FE_INEXACT](<#/doc/numeric/fenv/FE_exceptions>) são erros de domínio.

Conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>), [FE_INEXACT](<#/doc/numeric/fenv/FE_exceptions>) pode ser (mas não é obrigatório em plataformas de ponto flutuante não-IEEE) levantado por `rint` ao arredondar um valor finito não inteiro.

A única diferença entre `rint` e [nearbyint](<#/doc/numeric/math/nearbyint>) é que [nearbyint](<#/doc/numeric/math/nearbyint>) nunca levanta [FE_INEXACT](<#/doc/numeric/fenv/FE_exceptions>).

Os maiores valores de ponto flutuante representáveis são inteiros exatos em todos os formatos padrão de ponto flutuante, então `rint` nunca transborda por si só; no entanto, o resultado pode transbordar qualquer tipo inteiro (incluindo [intmax_t](<#/doc/types/integer>)), quando armazenado em uma variável inteira.

Se o modo de arredondamento atual for...

* [FE_DOWNWARD](<#/doc/numeric/fenv/FE_round>), então `rint` é equivalente a [floor](<#/doc/numeric/math/floor>).
* [FE_UPWARD](<#/doc/numeric/fenv/FE_round>), então `rint` é equivalente a [ceil](<#/doc/numeric/math/ceil>).
* [FE_TOWARDZERO](<#/doc/numeric/fenv/FE_round>), então `rint` é equivalente a [trunc](<#/doc/numeric/math/trunc>)
* [FE_TONEAREST](<#/doc/numeric/fenv/FE_round>), então `rint` difere de [round](<#/doc/numeric/math/round>) no sentido de que casos intermediários são arredondados para o número par mais próximo em vez de para longe de zero.

### Exemplo

Execute este código
```c
    #include <fenv.h>
    #include <limits.h>
    #include <math.h>
    #include <stdio.h>
    
    int main(void)
    {
    #pragma STDC FENV_ACCESS ON
        fesetround(FE_TONEAREST);
        printf("rounding to nearest (halfway cases to even):\n"
               "rint(+2.3) = %+.1f  ", rint(2.3));
        printf("rint(+2.5) = %+.1f  ", rint(2.5));
        printf("rint(+3.5) = %+.1f\n", rint(3.5));
        printf("rint(-2.3) = %+.1f  ", rint(-2.3));
        printf("rint(-2.5) = %+.1f  ", rint(-2.5));
        printf("rint(-3.5) = %+.1f\n", rint(-3.5));
    
        fesetround(FE_DOWNWARD);
        printf("rounding down: \nrint(+2.3) = %+.1f  ", rint(2.3));
        printf("rint(+2.5) = %+.1f  ", rint(2.5));
        printf("rint(+3.5) = %+.1f\n", rint(3.5));
        printf("rint(-2.3) = %+.1f  ", rint(-2.3));
        printf("rint(-2.5) = %+.1f  ", rint(-2.5));
        printf("rint(-3.5) = %+.1f\n", rint(-3.5));
        printf("rounding down with lrint: \nlrint(+2.3) = %ld  ", lrint(2.3));
        printf("lrint(+2.5) = %ld  ", lrint(2.5));
        printf("lrint(+3.5) = %ld\n", lrint(3.5));
        printf("lrint(-2.3) = %ld  ", lrint(-2.3));
        printf("lrint(-2.5) = %ld  ", lrint(-2.5));
        printf("lrint(-3.5) = %ld\n", lrint(-3.5));
    
        printf("lrint(-0.0) = %ld\n", lrint(-0.0));
        printf("lrint(-Inf) = %ld\n", lrint(-INFINITY)); // FE_INVALID raised
    
        // error handling
        feclearexcept(FE_ALL_EXCEPT);
        printf("rint(1.1) = %.1f\n", rint(1.1));
        if (fetestexcept(FE_INEXACT))
            puts("    FE_INEXACT was raised");
    
        feclearexcept(FE_ALL_EXCEPT);
        printf("lrint(LONG_MIN-2048.0) = %ld\n", lrint(LONG_MIN-2048.0));
        if (fetestexcept(FE_INVALID))
            puts("    FE_INVALID was raised");
    }
```

Saída possível:
```
    rounding to nearest (halfway cases to even):
    rint(+2.3) = +2.0  rint(+2.5) = +2.0  rint(+3.5) = +4.0
    rint(-2.3) = -2.0  rint(-2.5) = -2.0  rint(-3.5) = -4.0
    rounding down:
    rint(+2.3) = +2.0  rint(+2.5) = +2.0  rint(+3.5) = +3.0
    rint(-2.3) = -3.0  rint(-2.5) = -3.0  rint(-3.5) = -4.0
    rounding down with lrint:
    lrint(+2.3) = 2  lrint(+2.5) = 2  lrint(+3.5) = 3
    lrint(-2.3) = -3  lrint(-2.5) = -3  lrint(-3.5) = -4
    lrint(-0.0) = 0
    lrint(-Inf) = -9223372036854775808
    rint(1.1) = 1.0
        FE_INEXACT was raised
    lrint(LONG_MIN-2048.0) = -9223372036854775808
        FE_INVALID was raised
```

### Referências

* Padrão C23 (ISO/IEC 9899:2024):

  * 7.12.9.4 The rint functions (p: TBD)

  * 7.12.9.5 The lrint and llrint functions (p: TBD)

  * 7.25 Type-generic math <tgmath.h> (p: TBD)

  * F.10.6.4 The rint functions (p: TBD)

  * F.10.6.5 The lrint and llrint functions (p: TBD)

* Padrão C17 (ISO/IEC 9899:2018):

  * 7.12.9.4 The rint functions (p: 184)

  * 7.12.9.5 The lrint and llrint functions (p: 184)

  * 7.25 Type-generic math <tgmath.h> (p: 272-273)

  * F.10.6.4 The rint functions (p: 384)

  * F.10.6.5 The lrint and llrint functions (p: 384)

* Padrão C11 (ISO/IEC 9899:2011):

  * 7.12.9.4 The rint functions (p: 252)

  * 7.12.9.5 The lrint and llrint functions (p: 252)

  * 7.25 Type-generic math <tgmath.h> (p: 373-375)

  * F.10.6.4 The rint functions (p: 527)

  * F.10.6.5 The lrint and llrint functions (p: 527)

* Padrão C99 (ISO/IEC 9899:1999):

  * 7.12.9.4 The rint functions (p: 232-233)

  * 7.12.9.5 The lrint and llrint functions (p: 233)

  * 7.22 Type-generic math <tgmath.h> (p: 335-337)

  * F.9.6.4 The rint functions (p: 463)

  * F.9.6.5 The lrint and llrint functions (p: 463)

### Veja também

[ trunctruncftruncl](<#/doc/numeric/math/trunc>)(desde C99)(desde C99)(desde C99) | arredonda para o inteiro mais próximo não maior em magnitude que o valor dado
(função)
[ nearbyintnearbyintfnearbyintl](<#/doc/numeric/math/nearbyint>)(desde C99)(desde C99)(desde C99) | arredonda para um inteiro usando o modo de arredondamento atual
(função)
[ fegetroundfesetround](<#/doc/numeric/fenv/feround>)(desde C99)(desde C99) | obtém ou define a direção de arredondamento
(função)
[documentação C++](<#/>) para rint