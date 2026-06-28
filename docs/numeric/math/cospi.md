# cospi, cospif, cospil, cospid32, cospid64, cospid128

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float cospif( float arg );  // desde C23
double cospi( double arg );  // desde C23
long double cospil( long double arg );  // desde C23
_Decimal32 cospid32( _Decimal32 arg );  // desde C23
_Decimal64 cospid64( _Decimal64 arg );  // desde C23
_Decimal128 cospid128( _Decimal128 arg );  // desde C23
Definido no cabeçalho ``<tgmath.h>``
#define cospi( arg )  // desde C23
```

  
1-6) Calcula o cosseno de `π·arg` medido em radianos, considerando `arg` como uma medida em meias-voltas.

7) Macro genérica de tipo: chama a função correta com base no tipo de `arg`. Se o argumento tiver tipo inteiro, (2) (`cospi`) é chamada.

As funções (4-6) são declaradas se e somente se a implementação predefinir `__STDC_IEC_60559_DFP__` (ou seja, se a implementação suportar números de ponto flutuante decimais).  | (desde C23)  
  
### Parâmetros

arg  |  \-  |  valor de ponto flutuante cujo produto com `π` representa um ângulo em radianos   
  
### Valor de retorno

Se nenhum erro ocorrer, o cosseno de `π·arg` (cos(π×arg)) no intervalo [-1, +1] é retornado.

### Tratamento de erros

Os erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559):

  * se o argumento for ±0, o resultado é 1.0;
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
    // Uma implementação ingênua de um subconjunto da família cospi
    double cospi(double arg)
    {
        return cos(arg * (double)3.1415926535897932384626433);
    }
    #endif
    
    int main(void)
    {
        const double pi = acos(-1);
    
        // uso típico
        printf("cospi(1) = %f, cos(pi) = %f\n", cospi(1), cos(pi));
        printf("cospi(0.5) = %f, cos(pi/2) = %f\n", cospi(0.5), cos(pi / 2));
        printf("cospi(-0.75) = %f, cos(-3*pi/4) = %f\n", cospi(-0.75), cos(-3 * pi / 4));
    
        // valores especiais
        printf("cospi(+0) = %f\n", cospi(0.0));
        printf("cospi(-0) = %f\n", cospi(-0.0));
    
        // tratamento de erros
        feclearexcept(FE_ALL_EXCEPT);
        printf("cospi(INFINITY) = %f\n", cospi(INFINITY));
        if (fetestexcept(FE_INVALID))
            puts("    FE_INVALID raised");
    }
```

Saída possível:
```
    cospi(1) = -1.000000, cos(pi) = -1.000000
    cospi(0.5) = 0.000000, cos(pi/2) = 0.000000
    cospi(-0.75) = -0.707107, cos(-3*pi/4) = -0.707107
    cospi(+0) = 1.000000
    cospi(-0) = 1.000000
    cospi(INFINITY) = -nan
        FE_INVALID raised
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.12.4.12 As funções cospi (p: 247)

    

  * 7.27 Matemática genérica de tipo <tgmath.h> (p: 387)

### Veja também

[ coscosfcosl](<#/doc/numeric/math/cos>)(C99)(C99) | calcula o cosseno (\\({\small\cos{x} }\\)cos(x))   
(função)