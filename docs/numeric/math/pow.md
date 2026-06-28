# pow, powf, powl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float powf( float base, float exponent );  // desde C99
double pow( double base, double exponent );
long double powl( long double base, long double exponent );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define pow( base, exponent )  // desde C99
```

  
1-3) Calcula o valor de base elevado à potência exponent.

4) Macro genérica de tipo: Se qualquer argumento tiver o tipo long double, `powl` é chamada. Caso contrário, se qualquer argumento tiver um tipo inteiro ou o tipo double, `pow` é chamada. Caso contrário, `powf` é chamada. Se pelo menos um argumento for complexo ou imaginário, então a macro invoca a função complexa correspondente ([cpowf](<#/doc/numeric/complex/cpow>), [cpow](<#/doc/numeric/complex/cpow>), [cpowl](<#/doc/numeric/complex/cpow>)).

### Parâmetros

base  |  \-  |  base como valor de ponto flutuante   
exponent  |  \-  |  exponent como valor de ponto flutuante   
  
### Valor de retorno

Se nenhum erro ocorrer, base elevado à potência de exponent (baseexponent  
) é retornado. 

Se ocorrer um erro de domínio, um valor definido pela implementação é retornado (NaN onde suportado). 

Se ocorrer um erro de polo ou um erro de faixa devido a overflow, ±[HUGE_VAL](<#/doc/numeric/math/HUGE_VAL>), `±HUGE_VALF`, ou `±HUGE_VALL` é retornado. 

Se ocorrer um erro de faixa devido a underflow, o resultado correto (após arredondamento) é retornado. 

### Tratamento de erros

Erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>). 

Se base for finito e negativo e exponent for finito e não inteiro, ocorre um erro de domínio e pode ocorrer um erro de faixa. 

Se base for zero e exponent for zero, pode ocorrer um erro de domínio. 

Se base for zero e exponent for negativo, pode ocorrer um erro de domínio ou um erro de polo. 

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559), 

  * pow(+0, exponent), onde exponent é um inteiro ímpar negativo, retorna `+∞` e levanta [FE_DIVBYZERO](<#/doc/numeric/fenv/FE_exceptions>)
  * pow(-0, exponent), onde exponent é um inteiro ímpar negativo, retorna `-∞` e levanta [FE_DIVBYZERO](<#/doc/numeric/fenv/FE_exceptions>)
  * pow(±0, exponent), onde exponent é negativo, finito, e é um inteiro par ou um não inteiro, retorna +∞ e levanta [FE_DIVBYZERO](<#/doc/numeric/fenv/FE_exceptions>)
  * pow(±0, -∞) retorna +∞ e pode levantar [FE_DIVBYZERO](<#/doc/numeric/fenv/FE_exceptions>)(ate C23)
  * pow(+0, exponent), onde exponent é um inteiro ímpar positivo, retorna +0 
  * pow(-0, exponent), onde exponent é um inteiro ímpar positivo, retorna -0 
  * pow(±0, exponent), onde exponent é um não inteiro positivo ou um inteiro par positivo, retorna +0 
  * pow(-1, ±∞) retorna 1
  * pow(+1, exponent) retorna 1 para qualquer exponent, mesmo quando exponent é `NaN`
  * pow(base, ±0) retorna 1 para qualquer base, mesmo quando base é `NaN`
  * pow(base, exponent) retorna `NaN` e levanta [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) se base for finito e negativo e exponent for finito e não inteiro. 
  * pow(base, -∞) retorna +∞ para qualquer `|base|<1`
  * pow(base, -∞) retorna +0 para qualquer `|base|>1`
  * pow(base, +∞) retorna +0 para qualquer `|base|<1`
  * pow(base, +∞) retorna +∞ para qualquer `|base|>1`
  * pow(-∞, exponent) retorna -0 se exponent for um inteiro ímpar negativo 
  * pow(-∞, exponent) retorna +0 se exponent for um não inteiro negativo ou um inteiro par negativo 
  * pow(-∞, exponent) retorna -∞ se exponent for um inteiro ímpar positivo 
  * pow(-∞, exponent) retorna +∞ se exponent for um não inteiro positivo ou um inteiro par positivo 
  * pow(+∞, exponent) retorna +0 para qualquer exponent negativo
  * pow(+∞, exponent) retorna +∞ para qualquer exponent positivo
  * exceto onde especificado acima, se qualquer argumento for NaN, NaN é retornado. 

### Notas

Embora `pow` não possa ser usado para obter uma raiz de um número negativo, [cbrt](<#/doc/numeric/math/cbrt>) é fornecida para o caso comum onde `exponent` é 1 / 3. 

### Exemplo

Execute este código
```c
    #include <errno.h>
    #include <fenv.h>
    #include <math.h>
    #include <stdio.h>
    // #pragma STDC FENV_ACCESS ON
    
    int main(void)
    {
        // typical usage
        printf("pow(2, 10) = %f\n", pow(2, 10));
        printf("pow(2, 0.5) = %f\n", pow(2, 0.5));
        printf("pow(-2, -3) = %f\n", pow(-2, -3));
    
        // special values
        printf("pow(-1, NAN) = %f\n", pow(-1, NAN));
        printf("pow(+1, NAN) = %f\n", pow(+1, NAN));
        printf("pow(INFINITY, 2) = %f\n", pow(INFINITY, 2));
        printf("pow(INFINITY, -1) = %f\n", pow(INFINITY, -1));
    
        // error handling
        errno = 0; feclearexcept(FE_ALL_EXCEPT);
        printf("pow(-1, 1/3) = %f\n", pow(-1, 1.0 / 3));
        if (errno == EDOM)
            perror("    errno == EDOM");
        if (fetestexcept(FE_INVALID))
            puts("    FE_INVALID raised");
    
        feclearexcept(FE_ALL_EXCEPT);
        printf("pow(-0, -3) = %f\n", pow(-0.0, -3));
        if (fetestexcept(FE_DIVBYZERO))
            puts("    FE_DIVBYZERO raised");
    }
```

Saída possível: 
```
    pow(2, 10) = 1024.000000
    pow(2, 0.5) = 1.414214
    pow(-2, -3) = -0.125000
    pow(-1, NAN) = nan
    pow(+1, NAN) = 1.000000
    pow(INFINITY, 2) = inf
    pow(INFINITY, -1) = 0.000000
    pow(-1, 1/3) = -nan
        errno == EDOM: Numerical argument out of domain
        FE_INVALID raised
    pow(-0, -3) = -inf
        FE_DIVBYZERO raised
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.12.7.5 As funções pow 

    

  * 7.27 Matemática genérica de tipo <tgmath.h>

    

  * F.10.4.5 As funções pow (p: 524-525) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.12.7.4 As funções pow (p: 248-249) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375) 

    

  * F.10.4.4 As funções pow (p: 524-525) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.12.7.4 As funções pow (p: 248-249) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375) 

    

  * F.10.4.4 As funções pow (p: 524-525) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.12.7.4 As funções pow (p: 229) 

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337) 

    

  * F.9.4.4 As funções pow (p: 461) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.5.5.1 A função pow 

### Veja também

[ sqrtsqrtfsqrtl](<#/doc/numeric/math/sqrt>)(C99)(C99) |  calcula a raiz quadrada (\\(\small{\sqrt{x} }\\)√x)   
(função)  
[ cbrtcbrtfcbrtl](<#/doc/numeric/math/cbrt>)(C99)(C99)(C99) |  calcula a raiz cúbica (\\(\small{\sqrt[3]{x} }\\)3√x)   
(função)  
[ hypothypotfhypotl](<#/doc/numeric/math/hypot>)(C99)(C99)(C99) |  calcula a raiz quadrada da soma dos quadrados de dois números dados (\\(\scriptsize{\sqrt{x^2+y^2} }\\)√x2  
+y2  
)   
(função)  
[ cpowcpowfcpowl](<#/doc/numeric/complex/cpow>)(C99)(C99)(C99) |  calcula a função de potência complexa   
(função)  
[Documentação C++](<#/>) para pow