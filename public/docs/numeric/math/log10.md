# log10, log10f, log10l

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float log10f( float arg );  // desde C99
double log10( double arg );
long double log10l( long double arg );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define log10( arg )  // desde C99
```

1-3) Calcula o logaritmo comum (base-10) de arg.

4) Macro genérica de tipo: Se arg tiver o tipo long double, `log10l` é chamada. Caso contrário, se arg tiver um tipo inteiro ou o tipo double, `log10` é chamada. Caso contrário, `log10f` é chamada.

### Parâmetros

- **arg** — valor de ponto flutuante

### Valor de retorno

Se nenhum erro ocorrer, o logaritmo comum (base-10) de arg (log10(arg) ou lg(arg)) é retornado.

Se ocorrer um erro de domínio, um valor definido pela implementação é retornado (NaN onde suportado).

Se ocorrer um erro de polo, [-HUGE_VAL](<#/doc/numeric/math/HUGE_VAL>), `-HUGE_VALF`, ou `-HUGE_VALL` é retornado.

### Tratamento de erros

Erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Ocorre um erro de domínio se arg for menor que zero.

Pode ocorrer um erro de polo se arg for zero.

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559),

*   Se o argumento for ±0, -∞ é retornado e [FE_DIVBYZERO](<#/doc/numeric/fenv/FE_exceptions>) é levantado.
*   Se o argumento for 1, +0 é retornado
*   Se o argumento for negativo, NaN é retornado e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado.
*   Se o argumento for +∞, +∞ é retornado
*   Se o argumento for NaN, NaN é retornado.

### Exemplo

Execute este código
```c
    #include <errno.h>
    #include <fenv.h>
    #include <float.h>
    #include <math.h>
    #include <stdio.h>
    // #pragma STDC FENV_ACCESS ON
    
    int main(void)
    {
        printf("log10(1000) = %f\n", log10(1000));
        printf("log10(0.001) = %f\n", log10(0.001));
        printf("base-5 logarithm of 125 = %f\n", log10(125) / log10(5));
    
        // special values
        printf("log10(1) = %f\n", log10(1));
        printf("log10(+Inf) = %f\n", log10(INFINITY));
    
        // error handling
        errno = 0; feclearexcept(FE_ALL_EXCEPT);
        printf("log10(0) = %f\n", log10(0));
        if (errno == ERANGE)
            perror("    errno == ERANGE");
        if (fetestexcept(FE_DIVBYZERO))
            puts("    FE_DIVBYZERO raised");
    }
```

Saída possível:
```
    log10(1000) = 3.000000
    log10(0.001) = -3.000000
    base-5 logarithm of 125 = 3.000000
    log10(1) = 0.000000
    log10(+Inf) = inf
    log10(0) = -inf
        errno == ERANGE: Numerical result out of range
        FE_DIVBYZERO raised
```

### Referências

*   Padrão C23 (ISO/IEC 9899:2024):

    *   7.12.6.8 As funções log10 (p: TBD)

    *   7.25 Matemática genérica de tipo <tgmath.h> (p: TBD)

    *   F.10.3.8 As funções log10 (p: TBD)

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.12.6.8 As funções log10 (p: 179)

    *   7.25 Matemática genérica de tipo <tgmath.h> (p: 272-273)

    *   F.10.3.8 As funções log10 (p: 380)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.12.6.8 As funções log10 (p: 245)

    *   7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    *   F.10.3.8 As funções log10 (p: 522)

*   Padrão C99 (ISO/IEC 9899:1999):

    *   7.12.6.8 As funções log10 (p: 225-226)

    *   7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337)

    *   F.9.3.8 As funções log10 (p: 459)

*   Padrão C89/C90 (ISO/IEC 9899:1990):

    *   4.5.4.5 A função log10

### Veja também

[ loglogflogl](<#/doc/numeric/math/log>)(C99)(C99) | calcula o logaritmo natural (base-e) (ln(x))
(função)
[ log2log2flog2l](<#/doc/numeric/math/log2>)(C99)(C99)(C99) | calcula o logaritmo base-2 (log2(x))
(função)
[ log1plog1pflog1pl](<#/doc/numeric/math/log1p>)(C99)(C99)(C99) | calcula o logaritmo natural (base-e) de 1 mais o número dado (ln(1+x))
(função)
[Documentação C++](<#/>) para log10