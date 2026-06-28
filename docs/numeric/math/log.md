# log, logf, logl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float logf( float arg );  // desde C99
double log( double arg );
long double logl( long double arg );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define log( arg )  // desde C99
```

1-3) Calcula o logaritmo natural (base _e_) de arg.

4) Macro genérica de tipo: Se arg tiver o tipo long double, `logl` é chamada. Caso contrário, se arg tiver um tipo inteiro ou o tipo double, `log` é chamada. Caso contrário, `logf` é chamada. Se arg for complexo ou imaginário, então a macro invoca a função complexa correspondente ([clogf](<#/doc/numeric/complex/clog>), [clog](<#/doc/numeric/complex/clog>), [clogl](<#/doc/numeric/complex/clog>)).

### Parâmetros

- **arg** — valor de ponto flutuante

### Valor de retorno

Se nenhum erro ocorrer, o logaritmo natural (base-_e_) de arg (ln(arg) ou loge(arg)) é retornado.

Se ocorrer um erro de domínio, um valor definido pela implementação é retornado (NaN onde suportado).

Se ocorrer um erro de polo, [-HUGE_VAL](<#/doc/numeric/math/HUGE_VAL>), `-HUGE_VALF`, ou `-HUGE_VALL` é retornado.

### Tratamento de erros

Os erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Ocorre um erro de domínio se arg for menor que zero.

Pode ocorrer um erro de polo se arg for zero.

Se a implementação suporta aritmética de ponto flutuante IEEE (IEC 60559),

  * Se o argumento for ±0, -∞ é retornado e [FE_DIVBYZERO](<#/doc/numeric/fenv/FE_exceptions>) é levantado.
  * Se o argumento for 1, +0 é retornado
  * Se o argumento for negativo, NaN é retornado e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado.
  * Se o argumento for +∞, +∞ é retornado
  * Se o argumento for NaN, NaN é retornado.

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
        printf("log(1) = %f\n", log(1));
        printf("base-5 logarithm of 125 = %f\n", log(125) / log(5));
     
        // special values
        printf("log(1) = %f\n", log(1));
        printf("log(+Inf) = %f\n", log(INFINITY));
     
        // error handling
        errno = 0; feclearexcept(FE_ALL_EXCEPT);
        printf("log(0) = %f\n", log(0));
        if (errno == ERANGE)
            perror("    errno == ERANGE");
        if (fetestexcept(FE_DIVBYZERO))
            puts("    FE_DIVBYZERO raised");
    }
```

Output:
```
    log(1) = 0.000000
    base-5 logarithm of 125 = 3.000000
    log(1) = 0.000000
    log(+Inf) = inf
    log(0) = -inf
        errno == ERANGE: Numerical result out of range
        FE_DIVBYZERO raised
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.12.6.7 As funções log (p: TBD)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: TBD)

    

  * F.10.3.7 As funções log (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.12.6.7 As funções log (p: 178-179)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 272-273)

    

  * F.10.3.7 As funções log (p: 380)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.12.6.7 As funções log (p: 244-245)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    

  * F.10.3.7 As funções log (p: 522)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.12.6.7 As funções log (p: 225)

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337)

    

  * F.9.3.7 As funções log (p: 459)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.5.4.4 A função log

### Veja também

[ log10log10flog10l](<#/doc/numeric/math/log10>)(C99)(C99) | calcula o logaritmo comum (base-_10_) (\\({\small \log_{10}{x} }\\)log10(x))
(função)
[ log2log2flog2l](<#/doc/numeric/math/log2>)(C99)(C99)(C99) | calcula o logaritmo de base-2 (\\({\small \log_{2}{x} }\\)log2(x))
(função)
[ log1plog1pflog1pl](<#/doc/numeric/math/log1p>)(C99)(C99)(C99) | calcula o logaritmo natural (base-_e_) de 1 mais o número dado (\\({\small \ln{(1+x)} }\\)ln(1+x))
(função)
[ expexpfexpl](<#/doc/numeric/math/exp>)(C99)(C99) | calcula _e_ elevado à potência dada (\\({\small e^x}\\)ex)
(função)
[ clogclogfclogl](<#/doc/numeric/complex/clog>)(C99)(C99)(C99) | calcula o logaritmo natural complexo
(função)
[Documentação C++](<#/>) para log