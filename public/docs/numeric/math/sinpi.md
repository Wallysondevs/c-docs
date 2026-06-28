# sinpi, sinpif, sinpil, sinpid32, sinpid64, sinpid128

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float sinpif( float arg );  // desde C23
double sinpi( double arg );  // desde C23
long double sinpil( long double arg );  // desde C23
_Decimal32 sinpid32( _Decimal32 arg );  // desde C23
_Decimal64 sinpid64( _Decimal64 arg );  // desde C23
_Decimal128 sinpid128( _Decimal128 arg );  // desde C23
Definido no cabeçalho ``<tgmath.h>``
#define sinpi( arg )  // desde C23
```

1-6) Calcula o seno de `π·arg` medido em radianos, considerando `arg` como uma medida em meias-revoluções.

7) Macro genérica de tipo: chama a função correta com base no tipo de `arg`. Se o argumento tiver tipo inteiro, (2) é chamada.

As funções (4-6) são declaradas se e somente se a implementação predefinir `__STDC_IEC_60559_DFP__` (ou seja, a implementação suporta números de ponto flutuante decimais). | (desde C23)

### Parâmetros

- **arg** — valor de ponto flutuante cujo produto com `π` representa um ângulo em radianos

### Valor de retorno

Se nenhum erro ocorrer, o seno de `π·arg` (sin(π×arg)) no intervalo [-1, +1] é retornado.

### Tratamento de erros

Erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Se a implementação suporta aritmética de ponto flutuante IEEE (IEC 60559):

  * se o argumento for ±0, ele é retornado sem modificação;
  * se o argumento for ±∞, NaN é retornado e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado;
  * se o argumento for NaN, NaN é retornado.

### Exemplo

Execute este código
```c
    #include <errno.h>
    #include <fenv.h>
    #include <math.h>
    #include <stdio.h>
     
    #ifndef __GNUC__
    #pragma STDC FENV_ACCESS ON
    #endif
     
    #if __STDC_VERSION__ < 202311L
    // A naive implementation of a subset of sinpi family
    double sinpi(double arg)
    {
        return sin(arg * (double)3.1415926535897932384626433);
    }
    #endif
     
    int main(void)
    {
        const double pi = acos(-1);
     
        // typical usage
        printf("sinpi(1) = %f, sin(pi) = %f\n", sinpi(1), sin(pi));
        printf("sinpi(0.5) = %f, sin(pi/2) = %f\n", sinpi(0.5), sin(pi / 2));
        printf("sinpi(-0.75) = %f, sin(-3*pi/4) = %f\n", sinpi(-0.75), sin(-3 * pi / 4));
     
        // special values
        printf("sinpi(+0) = %f\n", sinpi(0.0));
        printf("sinpi(-0) = %f\n", sinpi(-0.0));
     
        // error handling
        feclearexcept(FE_ALL_EXCEPT);
        printf("sinpi(INFINITY) = %f\n", sinpi(INFINITY));
        if (fetestexcept(FE_INVALID))
            puts("    FE_INVALID raised");
    }
```

Saída possível:
```
    sinpi(1) = 0.000000, sin(pi) = 0.000000
    sinpi(0.5) = 1.000000, sin(pi/2) = 1.000000
    sinpi(-0.75) = -0.707107, sin(-3*pi/4) = -0.707107
    sinpi(+0) = 0.000000
    sinpi(-0) = -0.000000
    sinpi(INFINITY) = -nan
        FE_INVALID raised
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    * 7.12.4.13 As funções sinpi (p: 247-248)

    * 7.27 Matemática genérica de tipo <tgmath.h> (p: 387)

### Veja também

[ sinsinfsinl](<#/doc/numeric/math/sin>)(C99)(C99) | calcula o seno (\\({\small\sin{x} }\\)sin(x))
(função)