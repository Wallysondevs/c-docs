# exp2, exp2f, exp2l

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float exp2f( float n );  // desde C99
double exp2( double n );  // desde C99
long double exp2l( long double n );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define exp2( n )  // desde C99
```

1-3) Calcula 2 elevado à potência `n` fornecida.

4) Macro de tipo genérico: Se `n` tiver o tipo long double, `exp2l` é chamada. Caso contrário, se `n` tiver um tipo inteiro ou o tipo double, `exp2` é chamada. Caso contrário, `exp2f` é chamada.

### Parâmetros

- **n** — valor de ponto flutuante

### Valor de retorno

Se nenhum erro ocorrer, o exponencial de base 2 de `n` (2n ) é retornado.

Se ocorrer um erro de intervalo devido a estouro (overflow), `+HUGE_VAL`, `+HUGE_VALF`, ou `+HUGE_VALL` é retornado.

Se ocorrer um erro de intervalo devido a subfluxo (underflow), o resultado correto (após arredondamento) é retornado.

### Tratamento de erros

Os erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559),

  * Se o argumento for ±0, 1 é retornado
  * Se o argumento for -∞, +0 é retornado
  * Se o argumento for +∞, +∞ é retornado
  * Se o argumento for NaN, NaN é retornado

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
        printf("exp2(5) = %f\n", exp2(5));
        printf("exp2(0.5) = %f\n", exp2(0.5));
        printf("exp2(-4) = %f\n", exp2(-4));
        // special values
        printf("exp2(-0.9) = %f\n", exp2(-0.9));
        printf("exp2(-Inf) = %f\n", exp2(-INFINITY));
        //error handling
        errno = 0; feclearexcept(FE_ALL_EXCEPT);
        printf("exp2(1024) = %f\n", exp2(1024));
        if (errno == ERANGE)
            perror("    errno == ERANGE");
        if (fetestexcept(FE_OVERFLOW))
            puts("    FE_OVERFLOW raised");
    }
```

Saída possível:
```
    exp2(5) = 32.000000
    exp2(0.5) = 1.414214
    exp2(-4) = 0.062500
    exp2(-0.9) = 0.535887
    exp2(-Inf) = 0.000000
    exp2(1024) = Inf
        errno == ERANGE: Result too large
        FE_OVERFLOW raised
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.12.6.2 As funções exp2 (p: TBD)

    

  * 7.25 Matemática de tipo genérico <tgmath.h> (p: TBD)

    

  * F.10.3.2 As funções exp2 (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.12.6.2 As funções exp2 (p: 177)

    

  * 7.25 Matemática de tipo genérico <tgmath.h> (p: 272-273)

    

  * F.10.3.2 As funções exp2 (p: 379)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.12.6.2 As funções exp2 (p: 242-243)

    

  * 7.25 Matemática de tipo genérico <tgmath.h> (p: 373-375)

    

  * F.10.3.2 As funções exp2 (p: 521)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.12.6.2 As funções exp2 (p: 223)

    

  * 7.22 Matemática de tipo genérico <tgmath.h> (p: 335-337)

    

  * F.9.3.2 As funções exp2 (p: 458)

### Veja também

[ expexpfexpl](<#/doc/numeric/math/exp>)(C99)(C99) | calcula _e_ elevado à potência fornecida (\\({\small e^x}\\)ex)
(função)
[ expm1expm1fexpm1l](<#/doc/numeric/math/expm1>)(C99)(C99)(C99) | calcula _e_ elevado à potência fornecida, menos um (\\({\small e^x-1}\\)ex-1)
(função)
[ log2log2flog2l](<#/doc/numeric/math/log2>)(C99)(C99)(C99) | calcula o logaritmo de base 2 (\\({\small \log_{2}{x} }\\)log2(x))
(função)
[Documentação C++](<#/>) para exp2