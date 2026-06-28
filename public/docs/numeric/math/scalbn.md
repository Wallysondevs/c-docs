# scalbn, scalbnf, scalbnl, scalbln, scalblnf, scalblnl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)`

```c
float scalbnf( float arg, int exp );  // desde C99
double scalbn( double arg, int exp );  // desde C99
long double scalbnl( long double arg, int exp );  // desde C99
Definido no cabeçalho `<tgmath.h>``
#define scalbn( arg, exp )  // desde C99
Definido no cabeçalho `<math.h>``
float scalblnf( float arg, long exp );  // desde C99
double scalbln( double arg, long exp );  // desde C99
long double scalblnl( long double arg, long exp );  // desde C99
Definido no cabeçalho `<tgmath.h>``
#define scalbln( arg, exp )  // desde C99
```

  
1-3,5-7) Multiplica um valor de ponto flutuante arg por [FLT_RADIX](<#/doc/types/limits>) elevado à potência [exp](<#/doc/numeric/math/exp>).

4,8) Macros genéricas de tipo: Se arg tiver o tipo long double, `scalbnl` ou `scalblnl` é chamada. Caso contrário, se arg tiver um tipo inteiro ou o tipo double, `scalbn` ou `scalbln` é chamada. Caso contrário, `scalbnf` ou `scalblnf` é chamada, respectivamente.

### Parâmetros

arg  |  \-  |  valor de ponto flutuante   
exp  |  \-  |  valor inteiro   
  
### Valor de retorno

Se nenhum erro ocorrer, arg multiplicado por [FLT_RADIX](<#/doc/types/limits>) elevado à potência de [exp](<#/doc/numeric/math/exp>) (arg×FLT_RADIXexp  
) é retornado. 

Se ocorrer um erro de intervalo devido a estouro (overflow), ±[HUGE_VAL](<#/doc/numeric/math/HUGE_VAL>), `±HUGE_VALF`, ou `±HUGE_VALL` é retornado. 

Se ocorrer um erro de intervalo devido a subfluxo (underflow), o resultado correto (após arredondamento) é retornado. 

### Tratamento de erros

Os erros são relatados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>). 

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559), 

  * A menos que ocorra um erro de intervalo, [FE_INEXACT](<#/doc/numeric/fenv/FE_exceptions>) nunca é levantado (o resultado é exato). 
  * A menos que ocorra um erro de intervalo, o [modo de arredondamento atual](<#/doc/numeric/fenv/FE_round>) é ignorado. 
  * Se arg for ±0, ele é retornado, sem modificação. 
  * Se arg for ±∞, ele é retornado, sem modificação. 
  * Se [exp](<#/doc/numeric/math/exp>) for 0, então `arg` é retornado, sem modificação. 
  * Se arg for NaN, NaN é retornado. 

### Notas

Em sistemas binários (onde [FLT_RADIX](<#/doc/types/limits>) é `2`), `scalbn` é equivalente a [ldexp](<#/doc/numeric/math/ldexp>). 

Embora `scalbn` e `scalbln` sejam especificadas para realizar a operação eficientemente, em muitas implementações elas são menos eficientes do que a multiplicação ou divisão por uma potência de dois usando operadores aritméticos. 

A função `scalbln` é fornecida porque o fator necessário para escalar do menor valor de ponto flutuante positivo para o maior valor finito pode ser maior que 32767, o [INT_MAX](<#/doc/types/limits>) garantido pelo padrão. Em particular, para o long double de 80 bits, o fator é 32828. 

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
        printf("scalbn(7, -4) = %f\n", scalbn(7, -4));
        printf("scalbn(1, -1074) = %g (minimum positive subnormal double)\n",
                scalbn(1, -1074));
        printf("scalbn(nextafter(1,0), 1024) = %g (largest finite double)\n",
                scalbn(nextafter(1,0), 1024));
    
        // special values
        printf("scalbn(-0, 10) = %f\n", scalbn(-0.0, 10));
        printf("scalbn(-Inf, -1) = %f\n", scalbn(-INFINITY, -1));
    
        // error handling
        errno = 0; feclearexcept(FE_ALL_EXCEPT);
        printf("scalbn(1, 1024) = %f\n", scalbn(1, 1024));
        if (errno == ERANGE)
            perror("    errno == ERANGE");
        if (fetestexcept(FE_OVERFLOW))
            puts("    FE_OVERFLOW raised");
    }
```

Saída possível: 
```
    scalbn(7, -4) = 0.437500
    scalbn(1, -1074) = 4.94066e-324 (minimum positive subnormal double)
    scalbn(nextafter(1,0), 1024) = 1.79769e+308 (largest finite double)
    scalbn(-0, 10) = -0.000000
    scalbn(-Inf, -1) = -inf
    scalbn(1, 1024) = inf
        errno == ERANGE: Numerical result out of range
        FE_OVERFLOW raised
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.12.6.13 As funções scalbn (p: TBD) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: TBD) 

    

  * F.10.3.13 As funções scalbn (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.12.6.13 As funções scalbn (p: TBD) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: TBD) 

    

  * F.10.3.13 As funções scalbn (p: TBD) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.12.6.13 As funções scalbn (p: 247) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375) 

    

  * F.10.3.13 As funções scalbn (p: 523) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.12.6.13 As funções scalbn (p: 228) 

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337) 

    

  * F.9.3.13 As funções scalbn (p: 460) 

### Veja também

[ frexpfrexpffrexpl](<#/doc/numeric/math/frexp>)(C99)(C99) |  divide um número em significando e uma potência de 2   
(função)  
[ ldexpldexpfldexpl](<#/doc/numeric/math/ldexp>)(C99)(C99) |  multiplica um número por 2 elevado a uma potência   
(função)  
[Documentação C++](<#/>) para scalbn