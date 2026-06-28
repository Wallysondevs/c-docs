# log2, log2f, log2l

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float log2f( float arg );  // desde C99
double log2( double arg );  // desde C99
long double log2l( long double arg );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define log2( arg )  // desde C99
```

1-3) Calcula o logaritmo de base 2 de arg.

4) Macro genérica de tipo: Se `arg` tiver o tipo long double, `log2l` é chamada. Caso contrário, se `arg` tiver um tipo inteiro ou o tipo double, `log2` é chamada. Caso contrário, `log2f` é chamada.

### Parâmetros

- **arg** — valor de ponto flutuante

### Valor de retorno

Se nenhum erro ocorrer, o logaritmo de base _2_ de `arg` (log2(arg) ou lb(arg)) é retornado.

Se ocorrer um erro de domínio, um valor definido pela implementação é retornado (NaN onde suportado).

Se ocorrer um erro de polo, [-HUGE_VAL](<#/doc/numeric/math/HUGE_VAL>), `-HUGE_VALF`, ou `-HUGE_VALL` é retornado.

### Tratamento de erros

Os erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Ocorre um erro de domínio se `arg` for menor que zero.

Pode ocorrer um erro de polo se `arg` for zero.

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559),

  * Se o argumento for ±0, -∞ é retornado e [FE_DIVBYZERO](<#/doc/numeric/fenv/FE_exceptions>) é levantado.
  * Se o argumento for 1, +0 é retornado
  * Se o argumento for negativo, NaN é retornado e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado.
  * Se o argumento for +∞, +∞ é retornado
  * Se o argumento for NaN, NaN é retornado

### Notas

Para `arg` inteiro, o logaritmo binário pode ser interpretado como o índice baseado em zero do bit 1 mais significativo na entrada.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <math.h>
    #include <float.h>
    #include <errno.h>
    #include <fenv.h>
    // #pragma STDC FENV_ACCESS ON
    int main(void)
    {
        printf("log2(65536) = %f\n", log2(65536));
        printf("log2(0.125) = %f\n", log2(0.125));
        printf("log2(0x020f) = %f (highest set bit is in position 9)\n", log2(0x020f));
        printf("base-5 logarithm of 125 = %f\n", log2(125)/log2(5));
        // special values
        printf("log2(1) = %f\n", log2(1));
        printf("log2(+Inf) = %f\n", log2(INFINITY));
        //error handling
        errno = 0; feclearexcept(FE_ALL_EXCEPT);
        printf("log2(0) = %f\n", log2(0));
        if(errno == ERANGE) perror("    errno == ERANGE");
        if(fetestexcept(FE_DIVBYZERO)) puts("    FE_DIVBYZERO raised");
    }
```

Saída possível:
```
    log2(65536) = 16.000000
    log2(0.125) = -3.000000
    log2(0x020f) = 9.041659 (highest set bit is in position 9)
    base-5 logarithm of 125 = 3.000000
    log2(1) = 0.000000
    log2(+Inf) = inf
    log2(0) = -inf
        errno == ERANGE: Numerical result out of range
        FE_DIVBYZERO raised
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.12.6.10 As funções log2 (p: 179)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 272-273)

    

  * F.10.3.10 As funções log2 (p: 381)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.12.6.10 As funções log2 (p: 246)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    

  * F.10.3.10 As funções log2 (p: 522)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.12.6.10 As funções log2 (p: 226)

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337)

    

  * F.9.3.10 As funções log2 (p: 459)

### Veja também

[ loglogflogl](<#/doc/numeric/math/log>)(C99)(C99) | calcula o logaritmo natural (base-_e_) (\\({\small \ln{x} }\\)ln(x))
(função)
[ log10log10flog10l](<#/doc/numeric/math/log10>)(C99)(C99) | calcula o logaritmo comum (base-_10_) (\\({\small \log_{10}{x} }\\)log10(x))
(função)
[ log1plog1pflog1pl](<#/doc/numeric/math/log1p>)(C99)(C99)(C99) | calcula o logaritmo natural (base-_e_) de 1 mais o número dado (\\({\small \ln{(1+x)} }\\)ln(1+x))
(função)
[ exp2exp2fexp2l](<#/doc/numeric/math/exp2>)(C99)(C99)(C99) | calcula _2_ elevado à potência dada (\\({\small 2^x}\\)2x)
(função)
[documentação C++](<#/>) para log2