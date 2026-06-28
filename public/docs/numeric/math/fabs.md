# fabs, fabsf, fabsl, fabsd32, fabsd64, fabsd128

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)`

```c
float fabsf( float arg );  // desde C99
double fabs( double arg );
long double fabsl( long double arg );  // desde C99
_Decimal32 fabsd32( _Decimal32 arg );  // desde C23
_Decimal64 fabsd64( _Decimal64 arg );  // desde C23
_Decimal128 fabsd128( _Decimal128 arg );  // desde C23
Definido no cabeçalho `<tgmath.h>``
#define fabs( arith )  // desde C99
```

  
1-6) Calcula o valor absoluto de um valor de ponto flutuante arg. As funções com parâmetros de ponto flutuante decimal são declaradas se e somente se a implementação predefinir `__STDC_IEC_60559_DFP__` (ou seja, a implementação suporta números de ponto flutuante decimal). | (desde C23)  
  
7) Macro genérica de tipo: Se o argumento tiver o tipo _Decimal128, _Decimal64, _Decimal32,(desde C23)long double, double, ou float, `fabsd128`, `fabsd64`, `fabsd32`,(desde C23)`fabsl`, `fabs`, ou `fabsf` é chamada, respectivamente. Caso contrário, se o argumento tiver um tipo inteiro, `fabs` é chamada. Caso contrário, se o argumento for complexo, então a macro invoca a função complexa correspondente ([cabsf](<#/doc/numeric/complex/cabs>), [cabs](<#/doc/numeric/complex/cabs>), [cabsl](<#/doc/numeric/complex/cabs>)). Caso contrário, o comportamento é indefinido.

### Parâmetros

arg  |  \-  |  valor de ponto flutuante   
arith  |  \-  |  valor de ponto flutuante ou inteiro   
  
### Valor de retorno

Se bem-sucedida, retorna o valor absoluto de arg (\\(\small |arg| \\)|arg|). O valor retornado é exato e não depende de nenhum modo de arredondamento. 

### Tratamento de erros

Esta função não está sujeita a nenhuma das condições de erro especificadas em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>). 

Se a implementação suporta aritmética de ponto flutuante IEEE (IEC 60559), 

  * Se o argumento é ±0, +0 é retornado. 
  * Se o argumento é ±∞, +∞ é retornado. 
  * Se o argumento é NaN, NaN é retornado. 

### Exemplo

Execute este código
```c
    #include <math.h>
    #include <stdio.h>
    
    #define PI 3.14159
    
    // This numerical integration assumes all area is positive.
    double integrate(double f(double),
                     double a, double b, // assume a < b
                     unsigned steps) // assume steps > 0
    {
        const double dx = (b - a) / steps;
        double sum = 0.0;
        for (double x = a; x < b; x += dx)
            sum += fabs(f(x));
        return dx * sum;
    }
    
    int main(void)
    {
        printf("fabs(+3) = %f\n", fabs(+3.0));
        printf("fabs(-3) = %f\n", fabs(-3.0));
        // special values
        printf("fabs(-0) = %f\n", fabs(-0.0));
        printf("fabs(-Inf) = %f\n", fabs(-INFINITY));
    
        printf("Area under sin(x) in [-PI, PI] = %f\n", integrate(sin, -PI, PI, 5101));
    }
```

Saída: 
```
    fabs(+3) = 3.000000
    fabs(-3) = 3.000000
    fabs(-0) = 0.000000
    fabs(-Inf) = inf
    Area under sin(x) in [-PI, PI] = 4.000000
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.12.7.2 As funções fabs (p: TBD) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: TBD) 

    

  * F.10.4.2 As funções fabs (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.12.7.2 As funções fabs (p: 181) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 272-273) 

    

  * F.10.4.2 As funções fabs (p: 382) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.12.7.2 As funções fabs (p: 248) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375) 

    

  * F.10.4.2 As funções fabs (p: 524) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.12.7.2 As funções fabs (p: 228-229) 

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337) 

    

  * F.9.4.2 As funções fabs (p: 460) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.5.6.2 A função fabs 

### Veja também

[ abslabsllabs](<#/doc/numeric/math/abs>)(C99) |  calcula o valor absoluto de um valor inteiro (\\(\small{|x|}\\)|x|)   
(função)  
[ copysigncopysignfcopysignl](<#/doc/numeric/math/copysign>)(C99)(C99)(C99) |  produz um valor com a magnitude de um dado valor e o sinal de outro dado valor   
(função)  
[ signbit](<#/doc/numeric/math/signbit>)(C99) |  verifica se o número dado é negativo   
(macro de função)  
[ cabscabsfcabsl](<#/doc/numeric/complex/cabs>)(C99)(C99)(C99) |  calcula a magnitude de um número complexo   
(função)  
[Documentação C++](<#/>) para fabs