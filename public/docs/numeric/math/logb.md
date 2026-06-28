# logb, logbf, logbl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float logbf( float arg );  // desde C99
double logb( double arg );  // desde C99
long double logbl( long double arg );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define logb( arg )  // desde C99
```

  
1-3) Extrai o valor do expoente imparcial e independente da base do argumento de ponto flutuante `arg`, e o retorna como um valor de ponto flutuante.

4) Macros genéricas de tipo: Se `arg` tiver o tipo `long double`, `logbl` é chamada. Caso contrário, se `arg` tiver um tipo inteiro ou o tipo `double`, `logb` é chamada. Caso contrário, `logbf` é chamada.

Formalmente, o expoente imparcial é a parte integral com sinal de logr|arg| (retornada por esta função como um valor de ponto flutuante), para `arg` diferente de zero, onde `r` é [FLT_RADIX](<#/doc/types/limits>). Se `arg` for subnormal, ele é tratado como se fosse normalizado. 

### Parâmetros

arg  |  \-  |  valor de ponto flutuante   
  
### Valor de retorno

Se nenhum erro ocorrer, o expoente imparcial de `arg` é retornado como um valor de ponto flutuante com sinal. 

Se ocorrer um erro de domínio, um valor definido pela implementação é retornado. 

Se ocorrer um erro de polo, [-HUGE_VAL](<#/doc/numeric/math/HUGE_VAL>), `-HUGE_VALF`, ou `-HUGE_VALL` é retornado. 

### Tratamento de erros

Os erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>). 

Erro de domínio ou de faixa pode ocorrer se `arg` for zero. 

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559), 

  * Se `arg` for ±0, -∞ é retornado e [FE_DIVBYZERO](<#/doc/numeric/fenv/FE_exceptions>) é levantado. 
  * Se `arg` for ±∞, +∞ é retornado. 
  * Se `arg` for NaN, NaN é retornado. 
  * Em todos os outros casos, o resultado é exato ([FE_INEXACT](<#/doc/numeric/fenv/FE_exceptions>) nunca é levantado) e [o modo de arredondamento atual](<#/doc/numeric/fenv/FE_round>) é ignorado. 

### Notas

[POSIX exige](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/logb.html>) que um erro de polo ocorra se `arg` for ±0. 

O valor do expoente retornado por `logb` é sempre 1 a menos que o expoente retornado por [frexp](<#/doc/numeric/math/frexp>) devido aos diferentes requisitos de normalização: para o expoente `e` retornado por `logb`, |arg*r-e  
| está entre 1 e `r` (tipicamente entre 1 e 2), mas para o expoente `e` retornado por [frexp](<#/doc/numeric/math/frexp>), |arg*2-e  
| está entre 0.5 e 1. 

### Exemplo

Compara diferentes funções de decomposição de ponto flutuante.

Execute este código
```c
    #include <fenv.h>
    #include <float.h>
    #include <math.h>
    #include <stdio.h>
    // #pragma STDC FENV_ACCESS ON
     
    int main(void)
    {
        double f = 123.45;
        printf("Given the number %.2f or %a in hex,\n", f, f);
     
        double f3;
        double f2 = modf(f, &f3);
        printf("modf() makes %.0f + %.2f\n", f3, f2);
     
        int i;
        f2 = frexp(f, &i);
        printf("frexp() makes %f * 2^%d\n", f2, i);
     
        i = logb(f);
        printf("logb()/logb() make %f * %d^%d\n", f/scalbn(1.0, i), FLT_RADIX, i);
     
        // error handling
        feclearexcept(FE_ALL_EXCEPT);
        printf("logb(0) = %f\n", logb(0));
        if (fetestexcept(FE_DIVBYZERO))
            puts("    FE_DIVBYZERO raised");
    }
```

Saída possível: 
```
    Given the number 123.45 or 0x1.edccccccccccdp+6 in hex,
    modf() makes 123 + 0.45
    frexp() makes 0.964453 * 2^7
    logb()/logb() make 1.928906 * 2^6
    logb(0) = -Inf
        FE_DIVBYZERO raised
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.12.6.11 As funções logb (p: TBD) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: TBD) 

    

  * F.10.3.11 As funções logb (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.12.6.11 As funções logb (p: 179-180) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375) 

    

  * F.10.3.11 As funções logb (p: 381) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.12.6.11 As funções logb (p: 246) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375) 

    

  * F.10.3.11 As funções logb (p: 522) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.12.6.11 As funções logb (p: 227) 

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337) 

    

  * F.9.3.11 As funções logb (p: 459) 

### Veja também

[ frexpfrexpffrexpl](<#/doc/numeric/math/frexp>)(C99)(C99) |  divide um número em significando e uma potência de 2   
(função)  
[ ilogbilogbfilogbl](<#/doc/numeric/math/ilogb>)(C99)(C99)(C99) |  extrai o expoente do número dado   
(função)  
[ scalbnscalbnfscalbnlscalblnscalblnfscalblnl](<#/doc/numeric/math/scalbn>)(C99)(C99)(C99)(C99)(C99)(C99) |  calcula eficientemente um número vezes [FLT_RADIX](<#/doc/types/limits>) elevado a uma potência   
(função)  
[Documentação C++](<#/>) para logb