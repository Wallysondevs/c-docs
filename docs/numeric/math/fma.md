# fma, fmaf, fmal

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float fmaf( float x, float y, float z );  // desde C99
double fma( double x, double y, double z );  // desde C99
long double fmal( long double x, long double y, long double z );  // desde C99
#define FP_FAST_FMA /* implementation-defined */  // desde C99
#define FP_FAST_FMAF /* implementation-defined */  // desde C99
#define FP_FAST_FMAL /* implementation-defined */  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define fma( x, y, z )  // desde C99
```

1-3) Calcula (x * y) + z como se com precisão infinita e arredondado apenas uma vez para se ajustar ao tipo de resultado.

4-6) Se as constantes de macro `FP_FAST_FMA`, `FP_FAST_FMAF`, ou `FP_FAST_FMAL` forem definidas, a função correspondente `fma`, `fmaf`, ou `fmal` é avaliada mais rapidamente (além de ser mais precisa) do que a expressão x * y + z para argumentos double, float e long double, respectivamente. Se definidas, essas macros avaliam para o inteiro 1.

7) Macro genérica de tipo: Se qualquer argumento tiver o tipo long double, `fmal` é chamada. Caso contrário, se qualquer argumento tiver um tipo inteiro ou o tipo double, `fma` é chamada. Caso contrário, `fmaf` é chamada.

### Parâmetros

- **x, y, z** — valores de ponto flutuante

### Valor de retorno

Em caso de sucesso, retorna o valor de (x * y) + z como se calculado com precisão infinita e arredondado uma vez para se ajustar ao tipo de resultado (ou, alternativamente, calculado como uma única operação ternária de ponto flutuante).

Se ocorrer um erro de intervalo devido a overflow, [±HUGE_VAL](<#/doc/numeric/math/HUGE_VAL>), `±HUGE_VALF`, ou `±HUGE_VALL` é retornado.

Se ocorrer um erro de intervalo devido a underflow, o valor correto (após arredondamento) é retornado.

### Tratamento de erros

Os erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559),

  * Se x for zero e y for infinito ou se x for infinito e y for zero, e
    * se z não for um NaN, então NaN é retornado e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado,
    * se z for um NaN, então NaN é retornado e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) pode ser levantado.
  * Se x * y for um infinito exato e z for um infinito com o sinal oposto, NaN é retornado e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado.
  * Se x ou y forem NaN, NaN é retornado.
  * Se z for NaN, e x * y não for 0 * Inf ou Inf * 0, então NaN é retornado (sem [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>)).

### Notas

Esta operação é comumente implementada em hardware como uma instrução de CPU de [multiplicação-adição fundida](<https://en.wikipedia.org/wiki/Multiply%E2%80%93accumulate_operation> "enwiki:Multiply–accumulate operation"). Se suportado por hardware, espera-se que as macros FP_FAST_FMA* apropriadas sejam definidas, mas muitas implementações utilizam a instrução da CPU mesmo quando as macros não estão definidas.

[POSIX especifica](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/fma.html>) que a situação em que o valor x * y é inválido e z é um NaN é um erro de domínio.

Devido à sua precisão intermediária infinita, `fma` é um bloco de construção comum para outras operações matemáticas corretamente arredondadas, como [sqrt](<#/doc/numeric/math/sqrt>) ou até mesmo a divisão (onde não fornecida pela CPU, por exemplo, [Itanium](<https://en.wikipedia.org/wiki/Itanium> "enwiki:Itanium")).

Assim como em todas as expressões de ponto flutuante, a expressão (x * y) + z pode ser compilada como uma multiplicação-adição fundida, a menos que o [` #pragma`](<#/doc/preprocessor/impl>) STDC FP_CONTRACT esteja desativado.

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
        // demo the difference between fma and built-in operators
        double in = 0.1;
        printf("0.1 double is %.23f (%a)\n", in, in);
        printf("0.1*10 is 1.0000000000000000555112 (0x8.0000000000002p-3),"
               " or 1.0 if rounded to double\n");
        double expr_result = 0.1 * 10 - 1;
        printf("0.1 * 10 - 1 = %g : 1 subtracted after "
               "intermediate rounding to 1.0\n", expr_result);
        double fma_result = fma(0.1, 10, -1);
        printf("fma(0.1, 10, -1) = %g (%a)\n", fma_result, fma_result);
    
        // fma use in double-double arithmetic
        printf("\nin double-double arithmetic, 0.1 * 10 is representable as ");
        double high = 0.1 * 10;
        double low = fma(0.1, 10, -high);
        printf("%g + %g\n\n", high, low);
    
        // error handling
        feclearexcept(FE_ALL_EXCEPT);
        printf("fma(+Inf, 10, -Inf) = %f\n", fma(INFINITY, 10, -INFINITY));
        if (fetestexcept(FE_INVALID))
            puts("    FE_INVALID raised");
    }
```

Saída possível:
```
    0.1 double is 0.10000000000000000555112 (0x1.999999999999ap-4)
    0.1*10 is 1.0000000000000000555112 (0x8.0000000000002p-3), or 1.0 if rounded to double
    0.1 * 10 - 1 = 0 : 1 subtracted after intermediate rounding to 1.0
    fma(0.1, 10, -1) = 5.55112e-17 (0x1p-54)
    
    in double-double arithmetic, 0.1 * 10 is representable as 1 + 5.55112e-17
    
    fma(+Inf, 10, -Inf) = -nan
        FE_INVALID raised
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.12.13.1 As funções fma (p: TBD)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: TBD)

    

  * F.10.10.1 As funções fma (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.12.13.1 As funções fma (p: 188-189)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 272-273)

    

  * F.10.10.1 As funções fma (p: 386)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.12.13.1 As funções fma (p: 258)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    

  * F.10.10.1 As funções fma (p: 530)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.12.13.1 As funções fma (p: 239)

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337)

    

  * F.9.10.1 As funções fma (p: 466)

### Veja também

[ remainderremainderfremainderl](<#/doc/numeric/math/remainder>)(C99)(C99)(C99) | calcula o resto com sinal da operação de divisão de ponto flutuante
(função)
[ remquoremquofremquol](<#/doc/numeric/math/remquo>)(C99)(C99)(C99) | calcula o resto com sinal, bem como os três últimos bits da operação de divisão
(função)
[Documentação C++](<#/>) para fma