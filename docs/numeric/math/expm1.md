# expm1, expm1f, expm1l

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float expm1f( float arg );  // desde C99
double expm1( double arg );  // desde C99
long double expm1l( long double arg );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define expm1( arg )  // desde C99
```

1-3) Calcula _e_ (número de Euler, `2.7182818`) elevado à potência `arg` fornecida, menos 1.0. Esta função é mais precisa do que a expressão [exp](<#/doc/numeric/math/exp>)(arg)-1.0 se `arg` estiver próximo de zero.

4) Macro genérica de tipo: Se `arg` tiver o tipo long double, `expm1l` é chamada. Caso contrário, se `arg` tiver um tipo inteiro ou o tipo double, `expm1` é chamada. Caso contrário, `expm1f` é chamada.

### Parâmetros

- **arg** — valor de ponto flutuante

### Valor de retorno

Se nenhum erro ocorrer, earg -1 é retornado.

Se ocorrer um erro de intervalo devido a overflow, [+HUGE_VAL](<#/doc/numeric/math/HUGE_VAL>), `+HUGE_VALF`, ou `+HUGE_VALL` é retornado.

Se ocorrer um erro de intervalo devido a underflow, o resultado correto (após arredondamento) é retornado.

### Tratamento de erros

Os erros são reportados conforme especificado em math_errhandling.

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559),

  * Se o argumento for ±0, ele é retornado, inalterado
  * Se o argumento for -∞, -1 é retornado
  * Se o argumento for +∞, +∞ é retornado
  * Se o argumento for NaN, NaN é retornado

### Notas

As funções `expm1` e [log1p](<#/doc/numeric/math/log1p>) são úteis para cálculos financeiros, por exemplo, ao calcular pequenas taxas de juros diárias: (1+x)n
-1 pode ser expresso como expm1(n * [log1p](<#/doc/numeric/math/log1p>)(x)). Essas funções também simplificam a escrita de funções hiperbólicas inversas precisas.

Para o tipo double compatível com IEEE, o overflow é garantido se 709.8 < arg.

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
        printf("expm1(1) = %f\n", expm1(1));
        printf("Interest earned in 2 days on $100, compounded daily at 1%%\n"
               " on a 30/360 calendar = %f\n",
               100*expm1(2*log1p(0.01/360)));
        printf("exp(1e-16)-1 = %g, but expm1(1e-16) = %g\n",
               exp(1e-16)-1, expm1(1e-16));
        // special values
        printf("expm1(-0) = %f\n", expm1(-0.0));
        printf("expm1(-Inf) = %f\n", expm1(-INFINITY));
        //error handling
        errno = 0; feclearexcept(FE_ALL_EXCEPT);
        printf("expm1(710) = %f\n", expm1(710));
        if (errno == ERANGE)
            perror("    errno == ERANGE");
        if (fetestexcept(FE_OVERFLOW))
            puts("    FE_OVERFLOW raised");
    }
```

Saída possível:
```
    expm1(1) = 1.718282
    Interest earned in 2 days on $100, compounded daily at 1%
     on a 30/360 calendar = 0.005556
    exp(1e-16)-1 = 0, but expm1(1e-16) = 1e-16
    expm1(-0) = -0.000000
    expm1(-Inf) = -1.000000
    expm1(710) = inf
        errno == ERANGE: Resultado muito grande
        FE_OVERFLOW levantado
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.12.6.3 As funções expm1 (p: TBD)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: TBD)

    

  * F.10.3.3 As funções expm1 (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.12.6.3 As funções expm1 (p: 177)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 272-273)

    

  * F.10.3.3 As funções expm1 (p: 379)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.12.6.3 As funções expm1 (p: 243)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    

  * F.10.3.3 As funções expm1 (p: 521)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.12.6.3 As funções expm1 (p: 223-224)

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337)

    

  * F.9.3.3 As funções expm1 (p: 458)

### Veja também

[ expexpfexpl](<#/doc/numeric/math/exp>)(C99)(C99) | calcula _e_ elevado à potência fornecida (\\({\small e^x}\\)ex)
(função)
[ exp2exp2fexp2l](<#/doc/numeric/math/exp2>)(C99)(C99)(C99) | calcula _2_ elevado à potência fornecida (\\({\small 2^x}\\)2x)
(função)
[ log1plog1pflog1pl](<#/doc/numeric/math/log1p>)(C99)(C99)(C99) | calcula o logaritmo natural (base-_e_) de 1 mais o número fornecido (\\({\small \ln{(1+x)} }\\)ln(1+x))
(função)
[Documentação C++](<#/>) para expm1