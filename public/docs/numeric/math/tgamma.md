# tgamma, tgammaf, tgammal

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float tgammaf( float arg );  // desde C99
double tgamma( double arg );  // desde C99
long double tgammal( long double arg );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define tgamma( arg )  // desde C99
```

1-3) Calcula a [função gama](<https://en.wikipedia.org/wiki/Gamma_function> "enwiki:Gamma function") de arg.

4) Macro de tipo genérico: Se arg tiver o tipo long double, `tgammal` é chamada. Caso contrário, se arg tiver um tipo inteiro ou o tipo double, `tgamma` é chamada. Caso contrário, `tgammaf` é chamada.

### Parâmetros

- **arg** — valor de ponto flutuante

### Valor de retorno

Se nenhum erro ocorrer, o valor da função gama de arg, ou seja, \\(\Gamma(\mathtt{arg}) = \displaystyle\int_0^\infty\\!\\! t^{\mathtt{arg}-1} e^{-t}\, dt\\)∫∞  
0 _t_ arg-1  
_e_ -t d _t_ , é retornado.

Se ocorrer um erro de domínio, um valor definido pela implementação (NaN onde suportado) é retornado.

Se ocorrer um erro de polo, ±[HUGE_VAL](<#/doc/numeric/math/HUGE_VAL>), `±HUGE_VALF`, ou `±HUGE_VALL` é retornado.

Se ocorrer um erro de intervalo devido a estouro (overflow), [±HUGE_VAL](<#/doc/numeric/math/HUGE_VAL>), `±HUGE_VALF`, ou `±HUGE_VALL` é retornado.

Se ocorrer um erro de intervalo devido a subfluxo (underflow), o valor correto (após arredondamento) é retornado.

### Tratamento de erros

Os erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Se arg for zero ou um inteiro menor que zero, um erro de polo ou um erro de domínio pode ocorrer.

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559):

  * Se o argumento for ±0, ±∞ é retornado e [FE_DIVBYZERO](<#/doc/numeric/fenv/FE_exceptions>) é levantado.
  * Se o argumento for um inteiro negativo, NaN é retornado e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado.
  * Se o argumento for -∞, NaN é retornado e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado.
  * Se o argumento for +∞, +∞ é retornado.
  * Se o argumento for NaN, NaN é retornado.

### Notas

Se arg for um número natural, tgamma(arg) é o fatorial de arg - 1. Muitas implementações calculam o fatorial exato no domínio inteiro se o argumento for um inteiro suficientemente pequeno.

Para o tipo double compatível com IEEE, o estouro (overflow) ocorre se 0 < x < 1/[DBL_MAX](<#/doc/types/limits>) ou se x > 171.7.

[POSIX exige](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/tgamma.html>) que um erro de polo ocorra se o argumento for zero, mas um erro de domínio ocorra quando o argumento for um inteiro negativo. Também especifica que, no futuro, erros de domínio podem ser substituídos por erros de polo para argumentos inteiros negativos (caso em que o valor de retorno nesses casos mudaria de NaN para ±∞).

Existe uma função não padrão chamada `gamma` em várias implementações, mas sua definição é inconsistente. Por exemplo, a versão `gamma` do glibc e 4.2BSD executa `lgamma`, mas a versão `gamma` do 4.4BSD executa `tgamma`.

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
        printf("tgamma(10) = %f, 9!=%f\n", tgamma(10), 2 * 3 * 4 * 5 * 6 * 7 * 8 * 9.0);
        printf("tgamma(0.5) = %f, sqrt(pi) = %f\n", tgamma(0.5), sqrt(acos(-1)));
    
        // special values
        printf("tgamma(+Inf) = %f\n", tgamma(INFINITY));
    
        // error handling
        errno = 0; feclearexcept(FE_ALL_EXCEPT);
        printf("tgamma(-1) = %f\n", tgamma(-1));
        if (errno == ERANGE)
            perror("    errno == ERANGE");
        else
            if (errno == EDOM)   perror("    errno == EDOM");
        if (fetestexcept(FE_DIVBYZERO))
            puts("    FE_DIVBYZERO raised");
        else if (fetestexcept(FE_INVALID))
            puts("    FE_INVALID raised");
    }
```

Saída possível:
```
    tgamma(10) = 362880.000000, 9!=362880.000000
    tgamma(0.5) = 1.772454, sqrt(pi) = 1.772454
    tgamma(+Inf) = inf
    tgamma(-1) = nan
        errno == EDOM: Numerical argument out of domain
        FE_INVALID raised
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.12.8.4 As funções tgamma (p: 250)

    

  * 7.25 Matemática de tipo genérico <tgmath.h> (p: 373-375)

    

  * F.10.5.4 As funções tgamma (p: 525)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.12.8.4 As funções tgamma (p: 250)

    

  * 7.25 Matemática de tipo genérico <tgmath.h> (p: 373-375)

    

  * F.10.5.4 As funções tgamma (p: 525)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.12.8.4 As funções tgamma (p: 250)

    

  * 7.25 Matemática de tipo genérico <tgmath.h> (p: 373-375)

    

  * F.10.5.4 As funções tgamma (p: 525)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.12.8.4 As funções tgamma (p: 231)

    

  * 7.22 Matemática de tipo genérico <tgmath.h> (p: 335-337)

    

  * F.9.5.4 As funções tgamma (p: 462)

### Veja também

[ lgammalgammaflgammal](<#/doc/numeric/math/lgamma>)(C99)(C99)(C99) | calcula o logaritmo natural (base-_e_) da função gama
(função)
[Documentação C++](<#/>) para tgamma

### Links externos

[Weisstein, Eric W. "Gamma Function."](<https://mathworld.wolfram.com/GammaFunction.html>) De MathWorld — Um Recurso Web da Wolfram.
---