# ilogb, ilogbf, ilogbl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
int ilogbf( float arg );  // desde C99
int ilogb( double arg );  // desde C99
int ilogbl( long double arg );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define ilogb( arg )  // desde C99
Definido no cabeçalho ``<math.h>``
#define FP_ILOGB0 /* definido pela implementação */  // desde C99
#define FP_ILOGBNAN /* definido pela implementação */  // desde C99
```

  
1-3) Extrai o valor do expoente não viciado do argumento de ponto flutuante `arg`, e o retorna como um valor inteiro com sinal.

4) Macros genéricas de tipo: Se `arg` tiver o tipo `long double`, `ilogbl` é chamada. Caso contrário, se `arg` tiver um tipo inteiro ou o tipo `double`, `ilogb` é chamada. Caso contrário, `ilogbf` é chamada.

5) Expande para uma expressão constante inteira cujo valor é `INT_MIN` ou `-INT_MAX`.

6) Expande para uma expressão constante inteira cujo valor é `INT_MIN` ou `+INT_MAX`.

Formalmente, o expoente não viciado é a parte integral de logr|arg| como um valor inteiro com sinal, para `arg` não nulo, onde `r` é `FLT_RADIX`.

### Parâmetros

arg  |  \-  |  valor de ponto flutuante   
  
### Valor de retorno

Se nenhum erro ocorrer, o expoente não viciado de `arg` é retornado como um valor `int` com sinal.

Se `arg` for zero, `FP_ILOGB0` é retornado.

Se `arg` for infinito, `INT_MAX` é retornado.

Se `arg` for um NaN, `FP_ILOGBNAN` é retornado.

Se o resultado correto for maior que `INT_MAX` ou menor que `INT_MIN`, o valor de retorno é não especificado e um erro de domínio ou erro de faixa pode ocorrer.

### Tratamento de erros

Erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Um erro de domínio ou erro de faixa pode ocorrer se `arg` for zero, infinito ou NaN.

Se o resultado correto for maior que `INT_MAX` ou menor que `INT_MIN`, um erro de domínio ou um erro de faixa pode ocorrer.

Se a implementação suporta aritmética de ponto flutuante IEEE (IEC 60559),

  * Se o resultado correto for maior que `INT_MAX` ou menor que `INT_MIN`, `FE_INVALID` é levantado.
  * Se `arg` for ±0, ±∞, ou NaN, `FE_INVALID` é levantado.
  * Em todos os outros casos, o resultado é exato (`FE_INEXACT` nunca é levantado) e [o modo de arredondamento atual](<#/doc/numeric/fenv/FE_round>) é ignorado.

### Notas

Se `arg` não for zero, infinito ou NaN, o valor retornado é exatamente equivalente a `(int)logb(arg)`.

[POSIX exige](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/ilogb.html>) que um erro de domínio ocorra se `arg` for zero, infinito, NaN, ou se o resultado correto estiver fora da faixa de `int`.

POSIX também exige que, em sistemas conformes com XSI, o valor retornado quando o resultado correto é maior que `INT_MAX` seja `INT_MAX` e o valor retornado quando o resultado correto é menor que `INT_MIN` seja `INT_MIN`.

O resultado correto pode ser representado como `int` em todas as implementações conhecidas. Para que ocorra estouro, `INT_MAX` deve ser menor que `LDBL_MAX_EXP * log2(FLT_RADIX)` ou `INT_MIN` deve ser maior que `LDBL_MIN_EXP - LDBL_MANT_DIG) * log2(FLT_RADIX)`.

O valor do expoente retornado por `ilogb` é sempre 1 a menos que o expoente retornado por `frexp` devido aos diferentes requisitos de normalização: para o expoente `e` retornado por `ilogb`, `|arg*r-e |` está entre 1 e `r` (tipicamente entre 1 e 2), mas para o expoente `e` retornado por `frexp`, `|arg*2-e |` está entre 0.5 e 1.

### Exemplo

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
        printf("Given the number %.2f or %a in hex,\n", f, f);
    
        double f3;
        double f2 = modf(f, &f3);
        printf("modf() makes %.0f + %.2f\n", f3, f2);
    
        int i;
        f2 = frexp(f, &i);
        printf("frexp() makes %f * 2^%d\n", f2, i);
    
        i = ilogb(f);
        printf("logb()/ilogb() make %f * %d^%d\n", f/scalbn(1.0, i), FLT_RADIX, i);
    
        // error handling
        feclearexcept(FE_ALL_EXCEPT);
        printf("ilogb(0) = %d\n", ilogb(0));
        if (fetestexcept(FE_INVALID))
            puts("    FE_INVALID raised");
    }
```

Saída possível:
```
    Given the number 123.45 or 0x1.edccccccccccdp+6 in hex,
    modf() makes 123 + 0.45
    frexp() makes 0.964453 * 2^7
    logb()/ilogb() make 1.92891 * 2^6
    ilogb(0) = -2147483648
        FE_INVALID raised
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.12/8 Matemática <math.h> (p: TBD)

    

  * 7.12.6.5 As funções ilogb (p: TBD)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: TBD)

    

  * F.10.3.5 As funções ilogb (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.12/8 Matemática <math.h> (p: TBD)

    

  * 7.12.6.5 As funções ilogb (p: TBD)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: TBD)

    

  * F.10.3.5 As funções ilogb (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.12/8 Matemática <math.h> (p: 232)

    

  * 7.12.6.5 As funções ilogb (p: 244)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    

  * F.10.3.5 As funções ilogb (p: 521)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.12/8 Matemática <math.h> (p: 213)

    

  * 7.12.6.5 As funções ilogb (p: 224-225)

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337)

    

  * F.9.3.5 As funções ilogb (p: 458)

### Veja também

[ frexpfrexpffrexpl](<#/doc/numeric/math/frexp>)(C99)(C99) |  divide um número em significando e uma potência de 2   
(função)  
[ logblogbflogbl](<#/doc/numeric/math/logb>)(C99)(C99)(C99) |  extrai o expoente do número dado   
(função)  
[ scalbnscalbnfscalbnlscalblnscalblnfscalblnl](<#/doc/numeric/math/scalbn>)(C99)(C99)(C99)(C99)(C99)(C99) |  calcula eficientemente um número vezes `FLT_RADIX` elevado a uma potência   
(função)  
[Documentação C++](<#/>) para ilogb