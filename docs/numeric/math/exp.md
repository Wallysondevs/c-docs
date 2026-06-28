# exp, expf, expl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float expf( float arg );  // desde C99
double exp( double arg );
long double expl( long double arg );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define exp( arg )  // desde C99
```

1-3) Calcula e ([número de Euler](<https://en.wikipedia.org/wiki/E_\(mathematical_constant\)> "enwiki:E \(mathematical constant\)"), 2.7182818...) elevado à potência arg fornecida.

4) Macro genérica de tipo: Se arg tiver o tipo long double, `expl` é chamada. Caso contrário, se arg tiver um tipo inteiro ou o tipo double, `exp` é chamada. Caso contrário, `expf` é chamada. Se arg for complexo ou imaginário, a macro invoca a função complexa correspondente ([cexpf](<#/doc/numeric/complex/cexp>), [cexp](<#/doc/numeric/complex/cexp>), [cexpl](<#/doc/numeric/complex/cexp>)).

### Parâmetros

- **arg** — valor de ponto flutuante

### Valor de retorno

Se nenhum erro ocorrer, o exponencial de base-_e_ de arg (earg ) é retornado.

Se ocorrer um erro de faixa devido a estouro (overflow), [+HUGE_VAL](<#/doc/numeric/math/HUGE_VAL>), `+HUGE_VALF`, ou `+HUGE_VALL` é retornado.

Se ocorrer um erro de faixa devido a subfluxo (underflow), o resultado correto (após arredondamento) é retornado.

### Tratamento de erros

Erros são relatados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559),

  * Se o argumento for ±0, 1 é retornado
  * Se o argumento for -∞, +0 é retornado
  * Se o argumento for +∞, +∞ é retornado
  * Se o argumento for NaN, NaN é retornado

### Observações

Para o tipo double compatível com IEEE, estouro (overflow) é garantido se 709.8 < arg, e subfluxo (underflow) é garantido se arg < -708.4.

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
        printf("exp(1) = %f\n", exp(1));
        printf("FV of $100, continuously compounded at 3%% for 1 year = %f\n",
                100*exp(0.03));
        // special values
        printf("exp(-0) = %f\n", exp(-0.0));
        printf("exp(-Inf) = %f\n", exp(-INFINITY));
        //error handling
        errno = 0; feclearexcept(FE_ALL_EXCEPT);
        printf("exp(710) = %f\n", exp(710));
        if (errno == ERANGE)
            perror("    errno == ERANGE");
        if (fetestexcept(FE_OVERFLOW))
            puts("    FE_OVERFLOW raised");
    }
```

Saída possível:
```
    exp(1) = 2.718282
    FV of $100, continuously compounded at 3% for 1 year = 103.045453
    exp(-0) = 1.000000
    exp(-Inf) = 0.000000
    exp(710) = inf
        errno == ERANGE: Numerical result out of range
        FE_OVERFLOW raised
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.12.6.1 As funções exp (p: TBD)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: TBD)

    

  * F.10.3.1 As funções exp (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.12.6.1 As funções exp (p: 175)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 272-273)

    

  * F.10.3.1 As funções exp (p: 379)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.12.6.1 As funções exp (p: 242)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    

  * F.10.3.1 As funções exp (p: 520)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.12.6.1 As funções exp (p: 223)

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337)

    

  * F.9.3.1 As funções exp (p: 458)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.5.4.1 A função exp

### Veja também

[ exp2exp2fexp2l](<#/doc/numeric/math/exp2>)(C99)(C99)(C99) | calcula _2_ elevado à potência fornecida (\\({\small 2^x}\\)2x)
(função)
[ expm1expm1fexpm1l](<#/doc/numeric/math/expm1>)(C99)(C99)(C99) | calcula _e_ elevado à potência fornecida, menos um (\\({\small e^x-1}\\)ex-1)
(função)
[ loglogflogl](<#/doc/numeric/math/log>)(C99)(C99) | calcula o logaritmo natural (base-_e_) (\\({\small \ln{x} }\\)ln(x))
(função)
[ cexpcexpfcexpl](<#/doc/numeric/complex/cexp>)(C99)(C99)(C99) | calcula o exponencial complexo de base-e
(função)
[Documentação C++](<#/>) para exp