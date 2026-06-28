# log1p, log1pf, log1pl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float log1pf( float arg );  // desde C99
double log1p( double arg );  // desde C99
long double log1pl( long double arg );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define log1p( arg )  // desde C99
```

1-3) Calcula o logaritmo natural (base e) de 1 + arg. Esta função é mais precisa do que a expressão [log](<#/doc/numeric/math/log>)(1 + arg) se arg estiver próximo de zero.

4) Macro de tipo genérico: Se arg tiver o tipo long double, `log1pl` é chamada. Caso contrário, se arg tiver um tipo inteiro ou o tipo double, `log1p` é chamada. Caso contrário, `log1pf` é chamada.

### Parâmetros

- **arg** — valor de ponto flutuante

### Valor de retorno

Se nenhum erro ocorrer, ln(1 + arg) é retornado.

Se ocorrer um erro de domínio, um valor definido pela implementação é retornado (NaN onde suportado).

Se ocorrer um erro de polo, -[HUGE_VAL](<#/doc/numeric/math/HUGE_VAL>), `-HUGE_VALF`, ou `-HUGE_VALL` é retornado.

Se ocorrer um erro de intervalo devido a underflow, o resultado correto (após arredondamento) é retornado.

### Tratamento de erros

Erros são reportados conforme especificado em [math_errhandling](<#/doc/numeric/math/math_errhandling>).

Ocorre um erro de domínio se arg for menor que -1.

Pode ocorrer um erro de polo se arg for -1.

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559),

*   Se o argumento for ±0, ele é retornado sem modificação.
*   Se o argumento for -1, -∞ é retornado e [FE_DIVBYZERO](<#/doc/numeric/fenv/FE_exceptions>) é levantado.
*   Se o argumento for menor que -1, NaN é retornado e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado.
*   Se o argumento for +∞, +∞ é retornado.
*   Se o argumento for NaN, NaN é retornado.

### Notas

As funções [expm1](<#/doc/numeric/math/expm1>) e `log1p` são úteis para cálculos financeiros, por exemplo, ao calcular pequenas taxas de juros diárias: (1+x)n -1 pode ser expresso como [expm1](<#/doc/numeric/math/expm1>)(n * log1p(x)). Essas funções também simplificam a escrita de funções hiperbólicas inversas precisas.

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
        printf("log1p(0) = %f\n", log1p(0));
        printf("Interest earned in 2 days on $100, compounded daily at 1%%\n"
               " on a 30/360 calendar = %f\n",
               100*expm1(2*log1p(0.01/360)));
        printf("log(1+1e-16) = %g, but log1p(1e-16) = %g\n",
               log(1+1e-16), log1p(1e-16));
    
        // special values
        printf("log1p(-0) = %f\n", log1p(-0.0));
        printf("log1p(+Inf) = %f\n", log1p(INFINITY));
    
        // error handling
        errno = 0; feclearexcept(FE_ALL_EXCEPT);
        printf("log1p(-1) = %f\n", log1p(-1));
        if (errno == ERANGE)
            perror("    errno == ERANGE");
        if (fetestexcept(FE_DIVBYZERO))
            puts("    FE_DIVBYZERO raised");
    }
```

Saída possível:
```
    log1p(0) = 0.000000
    Interest earned in 2 days on $100, compounded daily at 1%
     on a 30/360 calendar = 0.005556
    log(1+1e-16) = 0, but log1p(1e-16) = 1e-16
    log1p(-0) = -0.000000
    log1p(+Inf) = Inf
    log1p(-1) = -Inf
        errno == ERANGE: Result too large
        FE_DIVBYZERO raised
```

### Referências

*   Padrão C23 (ISO/IEC 9899:2024):

    *   7.12.6.9 As funções log1p (p: TBD)

    *   7.25 Matemática de tipo genérico <tgmath.h> (p: TBD)

    *   F.10.3.9 As funções log1p (p: TBD)
*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.12.6.9 As funções log1p (p: TBD)

    *   7.25 Matemática de tipo genérico <tgmath.h> (p: TBD)

    *   F.10.3.9 As funções log1p (p: TBD)
*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.12.6.9 As funções log1p (p: 245)

    *   7.25 Matemática de tipo genérico <tgmath.h> (p: 373-375)

    *   F.10.3.9 As funções log1p (p: 522)
*   Padrão C99 (ISO/IEC 9899:1999):

    *   7.12.6.9 As funções log1p (p: 226)

    *   7.22 Matemática de tipo genérico <tgmath.h> (p: 335-337)

    *   F.9.3.9 As funções log1p (p: 459)

### Veja também

[ loglogflogl](<#/doc/numeric/math/log>)(C99)(C99) | calcula o logaritmo natural (base-_e_) (\\({\small \ln{x} }\\)ln(x))
(função)
[ log10log10flog10l](<#/doc/numeric/math/log10>)(C99)(C99) | calcula o logaritmo comum (base-_10_) (\\({\small \log_{10}{x} }\\)log10(x))
(função)
[ log2log2flog2l](<#/doc/numeric/math/log2>)(C99)(C99)(C99) | calcula o logaritmo de base-2 (\\({\small \log_{2}{x} }\\)log2(x))
(função)
[ expm1expm1fexpm1l](<#/doc/numeric/math/expm1>)(C99)(C99)(C99) | calcula _e_ elevado à potência dada, menos um (\\({\small e^x-1}\\)ex-1)
(função)
[Documentação C++](<#/>) para log1p