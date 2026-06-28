# ldexp, ldexpf, ldexpl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float ldexpf( float arg, int exp );  // desde C99
double ldexp( double arg, int exp );
long double ldexpl( long double arg, int exp );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define ldexp( arg, exp )  // desde C99
```

  
1-3) Multiplica um valor de ponto flutuante arg pelo número 2 elevado à potência [exp](<#/doc/numeric/math/exp>).

4) Macro genérica de tipo: Se arg tiver o tipo long double, `ldexpl` é chamada. Caso contrário, se arg tiver um tipo inteiro ou o tipo double, `ldexp` é chamada. Caso contrário, `ldexpf` é chamada, respectivamente.

### Parâmetros

arg  |  \-  |  valor de ponto flutuante   
exp  |  \-  |  valor inteiro   
  
### Valor de retorno

Se nenhum erro ocorrer, arg multiplicado por 2 elevado à potência [exp](<#/doc/numeric/math/exp>) (arg×2exp  
) é retornado. 

Se ocorrer um erro de intervalo devido a overflow, [±HUGE_VAL](<#/doc/numeric/math/HUGE_VAL>), `±HUGE_VALF`, ou `±HUGE_VALL` é retornado. 

Se ocorrer um erro de intervalo devido a underflow, o resultado correto (após arredondamento) é retornado. 

### Tratamento de erros

Os erros são relatados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>). 

Se a implementação suporta aritmética de ponto flutuante IEEE (IEC 60559), 

  * A menos que ocorra um erro de intervalo, [FE_INEXACT](<#/doc/numeric/fenv/FE_exceptions>) nunca é levantado (o resultado é exato) 
  * A menos que ocorra um erro de intervalo, o [modo de arredondamento atual](<#/doc/numeric/fenv/FE_round>) é ignorado 
  * Se arg for ±0, ele é retornado, inalterado 
  * Se arg for ±∞, ele é retornado, inalterado 
  * Se [exp](<#/doc/numeric/math/exp>) for 0, então arg é retornado, inalterado 
  * Se arg for NaN, NaN é retornado. 

### Notas

Em sistemas binários (onde [FLT_RADIX](<#/doc/types/limits>) é 2), `ldexp` é equivalente a [scalbn](<#/doc/numeric/math/scalbn>). 

A função `ldexp` ("load exponent"), juntamente com sua dual, [frexp](<#/doc/numeric/math/frexp>), pode ser usada para manipular a representação de um número de ponto flutuante sem manipulações diretas de bits. 

Em muitas implementações, `ldexp` é menos eficiente do que a multiplicação ou divisão por uma potência de dois usando operadores aritméticos. 

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
        printf("ldexp(7, -4) = %f\n", ldexp(7, -4));
        printf("ldexp(1, -1074) = %g (minimum positive subnormal double)\n",
                ldexp(1, -1074));
        printf("ldexp(nextafter(1,0), 1024) = %g (largest finite double)\n",
                ldexp(nextafter(1,0), 1024));
     
        // special values
        printf("ldexp(-0, 10) = %f\n", ldexp(-0.0, 10));
        printf("ldexp(-Inf, -1) = %f\n", ldexp(-INFINITY, -1));
     
        // error handling
        errno = 0; feclearexcept(FE_ALL_EXCEPT);
        printf("ldexp(1, 1024) = %f\n", ldexp(1, 1024));
        if (errno == ERANGE)
            perror("    errno == ERANGE");
        if (fetestexcept(FE_OVERFLOW))
            puts("    FE_OVERFLOW raised");
    }
```

Saída possível: 
```
    ldexp(7, -4) = 0.437500
    ldexp(1, -1074) = 4.94066e-324 (minimum positive subnormal double)
    ldexp(nextafter(1,0), 1024) = 1.79769e+308 (largest finite double)
    ldexp(-0, 10) = -0.000000
    ldexp(-Inf, -1) = -inf
    ldexp(1, 1024) = inf
        errno == ERANGE: Numerical result out of range
        FE_OVERFLOW raised
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.12.6.6 As funções ldexp (p: TBD) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: TBD) 

    

  * F.10.3.6 As funções ldexp (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.12.6.6 As funções ldexp (p: TBD) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: TBD) 

    

  * F.10.3.6 As funções ldexp (p: TBD) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.12.6.6 As funções ldexp (p: 244) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375) 

    

  * F.10.3.6 As funções ldexp (p: 522) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.12.6.6 As funções ldexp (p: 225) 

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337) 

    

  * F.9.3.6 As funções ldexp (p: 459) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.5.4.3 A função ldexp 

### Veja também

[ frexpfrexpffrexpl](<#/doc/numeric/math/frexp>)(C99)(C99) | divide um número em significando e uma potência de 2   
(função)  
[ scalbnscalbnfscalbnlscalblnscalblnfscalblnl](<#/doc/numeric/math/scalbn>)(C99)(C99)(C99)(C99)(C99)(C99) | calcula eficientemente um número vezes [FLT_RADIX](<#/doc/types/limits>) elevado a uma potência   
(função)  
[Documentação C++](<#/>) para ldexp