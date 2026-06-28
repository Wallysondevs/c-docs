# cosh, coshf, coshl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float coshf( float arg );  // desde C99
double cosh( double arg );
long double coshl( long double arg );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define cosh( arg )  // desde C99
```

1-3) Calcula o cosseno hiperbólico de `arg`.

4) Macro de tipo genérico: Se o argumento tiver o tipo long double, `coshl` é chamado. Caso contrário, se o argumento tiver um tipo inteiro ou o tipo double, `cosh` é chamado. Caso contrário, `coshf` é chamado. Se o argumento for complexo, a macro invoca a função complexa correspondente ([ccoshf](<#/doc/numeric/complex/ccosh>), [ccosh](<#/doc/numeric/complex/ccosh>), [ccoshl](<#/doc/numeric/complex/ccosh>)).

### Parâmetros

- **arg** — valor de ponto flutuante representando um ângulo hiperbólico

### Valor de retorno

Se nenhum erro ocorrer, o cosseno hiperbólico de `arg` (cosh(arg), ou earg
+e-arg

---
2
) é retornado.

Se ocorrer um erro de faixa devido a estouro (overflow), [+HUGE_VAL](<#/doc/numeric/math/HUGE_VAL>), `+HUGE_VALF`, ou `+HUGE_VALL` é retornado.

### Tratamento de erros

Erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559),

  * se o argumento for ±0, 1 é retornado
  * Se o argumento for ±∞, +∞ é retornado
  * se o argumento for NaN, NaN é retornado

### Notas

Para o tipo double compatível com IEEE, se |arg| > 710.5, então `cosh(arg)` estoura (overflows).

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
        printf("cosh(1) = %f\ncosh(-1)= %f\n", cosh(1), cosh(-1));
        printf("log(sinh(1) + cosh(1))=%f\n", log(sinh(1) + cosh(1)));
        // special values
        printf("cosh(+0) = %f\ncosh(-0) = %f\n", cosh(0.0), cosh(-0.0));
        // error handling
        errno = 0;
        feclearexcept(FE_ALL_EXCEPT);
        printf("cosh(710.5) = %f\n", cosh(710.5));
        if (errno == ERANGE)
            perror("    errno == ERANGE");
        if (fetestexcept(FE_OVERFLOW))
            puts("    FE_OVERFLOW raised");
    }
```

Saída possível:
```
    cosh(1) = 1.543081
    cosh(-1)= 1.543081
    log(sinh(1) + cosh(1))=1.000000
    cosh(+0) = 1.000000
    cosh(-0) = 1.000000
    cosh(710.5) = inf
        errno == ERANGE: Numerical result out of range
        FE_OVERFLOW raised
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.12.5.4 As funções cosh (p: TBD)

    

  * 7.25 Matemática de tipo genérico <tgmath.h> (p: TBD)

    

  * F.10.2.4 As funções cosh (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.12.5.4 As funções cosh (p: 176)

    

  * 7.25 Matemática de tipo genérico <tgmath.h> (p: 272-273)

    

  * F.10.2.4 As funções cosh (p: 379)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.12.5.4 As funções cosh (p: 241)

    

  * 7.25 Matemática de tipo genérico <tgmath.h> (p: 373-375)

    

  * F.10.2.4 As funções cosh (p: 520)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.12.5.4 As funções cosh (p: 222)

    

  * 7.22 Matemática de tipo genérico <tgmath.h> (p: 335-337)

    

  * F.9.2.4 As funções cosh (p: 457)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.5.3.1 A função cosh

### Veja também

[ sinhsinhfsinhl](<#/doc/numeric/math/sinh>)(C99)(C99) | calcula o seno hiperbólico (\\({\small\sinh{x} }\\)sinh(x))
(função)
[ tanhtanhftanhl](<#/doc/numeric/math/tanh>)(C99)(C99) | calcula a tangente hiperbólica (\\({\small\tanh{x} }\\)tanh(x))
(função)
[ acoshacoshfacoshl](<#/doc/numeric/math/acosh>)(C99)(C99)(C99) | calcula o cosseno hiperbólico inverso (\\({\small\operatorname{arcosh}{x} }\\)arcosh(x))
(função)
[ ccoshccoshfccoshl](<#/doc/numeric/complex/ccosh>)(C99)(C99)(C99) | calcula o cosseno hiperbólico complexo
(função)
[Documentação C++](<#/>) para cosh