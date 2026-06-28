# modf, modff, modfl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float modff( float arg, float* iptr );  // desde C99
double modf( double arg, double* iptr );
long double modfl( long double arg, long double* iptr );  // desde C99
```

1-3) Decompõe o valor de ponto flutuante `arg` fornecido em partes integral e fracionária, cada uma com o mesmo tipo e sinal que `arg`. A parte integral (em formato de ponto flutuante) é armazenada no objeto apontado por `iptr`.

### Parâmetros

- **arg** — valor de ponto flutuante
- **iptr** — ponteiro para o valor de ponto flutuante onde a parte integral será armazenada

### Valor de retorno

Se nenhum erro ocorrer, retorna a parte fracionária de `arg` com o mesmo sinal que `arg`. A parte integral é colocada no valor apontado por `iptr`.

A soma do valor retornado e do valor armazenado em `*iptr` resulta em `arg` (considerando arredondamento).

### Tratamento de erros

Esta função não está sujeita a nenhum erro especificado em `[`math_errhandling`](<#/doc/numeric/math/math_errhandling>)`.

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559),

  * Se `arg` for ±0, ±0 é retornado, e ±0 é armazenado em `*iptr`.
  * Se `arg` for ±∞, ±0 é retornado, e ±∞ é armazenado em `*iptr`.
  * Se `arg` for NaN, NaN é retornado, e NaN é armazenado em `*iptr`.
  * O valor retornado é exato, `[`o modo de arredondamento atual`](<#/doc/numeric/fenv/FE_round>)` é ignorado.

### Notas

Esta função se comporta como se fosse implementada da seguinte forma:
```c
    double modf(double value, double *iptr)
    {
    #pragma STDC FENV_ACCESS ON
        int save_round = fegetround();
        fesetround(FE_TOWARDZERO);
        *iptr = std::nearbyint(value);
        fesetround(save_round);
        return copysign(isinf(value) ? 0.0 : value - (*iptr), value);
    }
```

### Exemplo

Execute este código
```c
    #include <float.h>
    #include <math.h>
    #include <stdio.h>
    
    int main(void)
    {
        double f = 123.45;
        printf("Given the number %.2f or %a in hex,\n", f, f);
    
        double f3;
        double f2 = modf(f, &f3);
        printf("modf() makes %.2f + %.2f\n", f3, f2);
    
        int i;
        f2 = frexp(f, &i);
        printf("frexp() makes %f * 2^%d\n", f2, i);
    
        i = ilogb(f);
        printf("logb()/ilogb() make %f * %d^%d\n", f / scalbn(1.0, i), FLT_RADIX, i);
    
        // special values
        f2 = modf(-0.0, &f3);
        printf("modf(-0) makes %.2f + %.2f\n", f3, f2);
        f2 = modf(-INFINITY, &f3);
        printf("modf(-Inf) makes %.2f + %.2f\n", f3, f2);
    }
```

Saída possível:
```
    Given the number 123.45 or 0x1.edccccccccccdp+6 in hex,
    modf() makes 123.00 + 0.45
    frexp() makes 0.964453 * 2^7
    logb()/ilogb() make 1.92891 * 2^6
    modf(-0) makes -0.00 + -0.00
    modf(-Inf) makes -INF + -0.00
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.12.6.12 As funções modf (p: TBD)

    

  * F.10.3.12 As funções modf (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.12.6.12 As funções modf (p: TBD)

    

  * F.10.3.12 As funções modf (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.12.6.12 As funções modf (p: 246-247)

    

  * F.10.3.12 As funções modf (p: 523)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.12.6.12 As funções modf (p: 227)

    

  * F.9.3.12 As funções modf (p: 460)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.5.4.6 A função modf

### Veja também

[`trunctruncftruncl`](<#/doc/numeric/math/trunc>)`(C99)(C99)(C99) | arredonda para o inteiro mais próximo não maior em magnitude que o valor fornecido`
(função)
[`Documentação C++`](<#/>) para modf