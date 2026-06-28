# round, roundf, roundl, lround, lroundf, lroundl, llround, llroundf, llroundl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float roundf( float arg );  // desde C99
double round( double arg );  // desde C99
long double roundl( long double arg );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define round( arg )  // desde C99
Definido no cabeçalho ``<math.h>``
long lroundf( float arg );  // desde C99
long lround( double arg );  // desde C99
long lroundl( long double arg );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define lround( arg )  // desde C99
Definido no cabeçalho ``<math.h>``
long long llroundf( float arg );  // desde C99
long long llround( double arg );  // desde C99
long long llroundl( long double arg );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define llround( arg )  // desde C99
```

1-3) Calcula o valor inteiro mais próximo de `arg` (em formato de ponto flutuante), arredondando casos de meio-ponto para longe de zero, independentemente do modo de arredondamento atual.

5-7, 9-11) Calcula o valor inteiro mais próximo de `arg` (em formato inteiro), arredondando casos de meio-ponto para longe de zero, independentemente do modo de arredondamento atual.

4,8,12) Macros genéricas de tipo: Se `arg` tiver o tipo `long double`, `roundl`, `lroundl`, `llroundl` é chamado. Caso contrário, se `arg` tiver um tipo inteiro ou o tipo `double`, `round`, `lround`, `llround` é chamado. Caso contrário, `roundf`, `lroundf`, `llroundf` é chamado, respectivamente.

### Parâmetros

- **arg** — valor de ponto flutuante

### Valor de retorno

Se nenhum erro ocorrer, o valor inteiro mais próximo de `arg`, arredondando casos de meio-ponto para longe de zero, é retornado.

Se ocorrer um erro de domínio, um valor definido pela implementação é retornado.

### Tratamento de erros

Os erros são relatados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Se o resultado de `lround` ou `llround` estiver fora do intervalo representável pelo tipo de retorno, um erro de domínio ou um erro de faixa pode ocorrer.

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559):

Para as funções `round`, `roundf` e `roundl`:

*   O [modo de arredondamento](<#/doc/numeric/fenv/FE_round>) atual não tem efeito.
*   Se `arg` for ±∞, ele é retornado, não modificado.
*   Se `arg` for ±0, ele é retornado, não modificado.
*   Se `arg` for NaN, NaN é retornado.

Para as famílias de funções `lround` e `llround`:

*   [FE_INEXACT](<#/doc/numeric/fenv/FE_exceptions>) nunca é levantado.
*   O [modo de arredondamento](<#/doc/numeric/fenv/FE_round>) atual não tem efeito.
*   Se `arg` for ±∞, [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado e um valor definido pela implementação é retornado.
*   Se o resultado do arredondamento estiver fora do intervalo do tipo de retorno, [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado e um valor definido pela implementação é retornado.
*   Se `arg` for NaN, [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado e um valor definido pela implementação é retornado.

### Notas

[FE_INEXACT](<#/doc/numeric/fenv/FE_exceptions>) pode ser (mas não é obrigatório) levantado por `round` ao arredondar um valor finito não inteiro.

Os maiores valores de ponto flutuante representáveis são inteiros exatos em todos os formatos de ponto flutuante padrão, então `round` nunca transborda por si só; no entanto, o resultado pode transbordar qualquer tipo inteiro (incluindo [intmax_t](<#/doc/types/integer>)), quando armazenado em uma variável inteira.

[POSIX especifica](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/lround.html>) que todos os casos em que `lround` ou `llround` levantam [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) são erros de domínio.

A versão `double` de `round` comporta-se como se implementada da seguinte forma:
```c
    #include <math.h>
    #pragma STDC FENV_ACCESS ON
    
    double round(double x)
    {
        return signbit(x) ? ceil(x - 0.5) : floor(x + 0.5);
    }
```

### Exemplo

Execute este código
```c
    #include <assert.h>
    #include <fenv.h>
    #include <float.h>
    #include <limits.h>
    #include <math.h>
    #include <stdio.h>
    // #pragma STDC FENV_ACCESS ON
    
    double custom_round(double x)
    {
        return signbit(x) ? ceil(x - 0.5) : floor(x + 0.5);
    }
    
    void test_custom_round()
    {
        const double sample[] =
        {
            0.0, 2.3, 2.5 - DBL_EPSILON, 2.5, 2.5 + DBL_EPSILON, 2.7, INFINITY
        };
        for (size_t t = 0; t < sizeof sample / sizeof(double); ++t)
            assert(round(+sample[t]) == custom_round(+sample[t]) &&
                   round(-sample[t]) == custom_round(-sample[t]));
    }
    
    int main(void)
    {
        // round
        printf("round(+2.3) = %+.1f  ", round(2.3));
        printf("round(+2.5) = %+.1f  ", round(2.5));
        printf("round(+2.7) = %+.1f\n", round(2.7));
        printf("round(-2.3) = %+.1f  ", round(-2.3));
        printf("round(-2.5) = %+.1f  ", round(-2.5));
        printf("round(-2.7) = %+.1f\n", round(-2.7));
    
        printf("round(-0.0) = %+.1f\n", round(-0.0));
        printf("round(-Inf) = %+f\n",   round(-INFINITY));
    
        test_custom_round();
    
        // lround
        printf("lround(+2.3) = %+ld  ", lround(2.3));
        printf("lround(+2.5) = %+ld  ", lround(2.5));
        printf("lround(+2.7) = %+ld\n", lround(2.7));
        printf("lround(-2.3) = %+ld  ", lround(-2.3));
        printf("lround(-2.5) = %+ld  ", lround(-2.5));
        printf("lround(-2.7) = %+ld\n", lround(-2.7));
    
        printf("lround(-0.0) = %+ld\n", lround(-0.0));
        printf("lround(-Inf) = %+ld\n", lround(-INFINITY)); // FE_INVALID raised
    
        // error handling
        feclearexcept(FE_ALL_EXCEPT);
        printf("lround(LONG_MAX+1.5) = %ld\n", lround(LONG_MAX + 1.5));
        if (fetestexcept(FE_INVALID))
            puts("    FE_INVALID was raised");
    }
```

Saída possível:
```
    round(+2.3) = +2.0  round(+2.5) = +3.0  round(+2.7) = +3.0
    round(-2.3) = -2.0  round(-2.5) = -3.0  round(-2.7) = -3.0
    round(-0.0) = -0.0
    round(-Inf) = -inf
    lround(+2.3) = +2  lround(+2.5) = +3  lround(+2.7) = +3
    lround(-2.3) = -2  lround(-2.5) = -3  lround(-2.7) = -3
    lround(-0.0) = +0
    lround(-Inf) = -9223372036854775808
    lround(LONG_MAX+1.5) = -9223372036854775808
        FE_INVALID was raised
```

### Referências

*   Padrão C23 (ISO/IEC 9899:2024):

    *   7.12.9.6 As funções `round` (p: TBD)

    *   7.12.9.7 As funções `lround` e `llround` (p: TBD)

    *   7.25 Matemática genérica de tipo <tgmath.h> (p: TBD)

    *   F.10.6.6 As funções `round` (p: TBD)

    *   F.10.6.7 As funções `lround` e `llround` (p: TBD)

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.12.9.6 As funções `round` (p: 184)

    *   7.12.9.7 As funções `lround` e `llround` (p: 184-185)

    *   7.25 Matemática genérica de tipo <tgmath.h> (p: 272-273)

    *   F.10.6.6 As funções `round` (p: 384)

    *   F.10.6.7 As funções `lround` e `llround` (p: 385)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.12.9.6 As funções `round` (p: 253)

    *   7.12.9.7 As funções `lround` e `llround` (p: 253)

    *   7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    *   F.10.6.6 As funções `round` (p: 527)

    *   F.10.6.7 As funções `lround` e `llround` (p: 528)

*   Padrão C99 (ISO/IEC 9899:1999):

    *   7.12.9.6 As funções `round` (p: 233)

    *   7.12.9.7 As funções `lround` e `llround` (p: 234)

    *   7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337)

    *   F.9.6.6 As funções `round` (p: 464)

    *   F.9.6.7 As funções `lround` e `llround` (p: 464)

### Veja também

[ floorfloorffloorl](<#/doc/numeric/math/floor>)(C99) | calcula o maior inteiro não maior que o valor dado
(função)
[ ceilceilfceill](<#/doc/numeric/math/ceil>)(C99) | calcula o menor inteiro não menor que o valor dado
(função)
[ trunctruncftruncl](<#/doc/numeric/math/trunc>)(C99) | arredonda para o inteiro mais próximo não maior em magnitude que o valor dado
(função)
[Documentação C++](<#/>) para `round`