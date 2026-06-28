# sinh, sinhf, sinhl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float sinhf( float arg );  // desde C99
double sinh( double arg );
long double sinhl( long double arg );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define sinh( arg )  // desde C99
```

1-3) Calcula o seno hiperbólico de arg.

4) Macro genérica de tipo: Se o argumento tiver o tipo long double, `sinhl` é chamada. Caso contrário, se o argumento tiver um tipo inteiro ou o tipo double, `sinh` é chamada. Caso contrário, `sinhf` é chamada. Se o argumento for complexo, então a macro invoca a função complexa correspondente ([csinhf](<#/doc/numeric/complex/csinh>), [csinh](<#/doc/numeric/complex/csinh>), [csinhl](<#/doc/numeric/complex/csinh>)).

### Parâmetros

- **arg** — valor de ponto flutuante representando um ângulo hiperbólico

### Valor de retorno

Se nenhum erro ocorrer, o seno hiperbólico de arg (sinh(arg), ou earg
-e-arg

---
2
) é retornado.

Se ocorrer um erro de intervalo devido a estouro (overflow), [±HUGE_VAL](<#/doc/numeric/math/HUGE_VAL>), `±HUGE_VALF`, ou `±HUGE_VALL` é retornado.

Se ocorrer um erro de intervalo devido a subfluxo (underflow), o resultado correto (após arredondamento) é retornado.

### Tratamento de erros

Os erros são relatados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559),

*   se o argumento for ±0 ou ±∞, ele é retornado sem modificação,
*   se o argumento for NaN, NaN é retornado.

### Notas

[POSIX especifica](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/sinh.html>) que, em caso de subfluxo (underflow), arg é retornado sem modificação, e se isso não for suportado, um valor definido pela implementação não maior que [DBL_MIN](<#/doc/types/limits>), [FLT_MIN](<#/doc/types/limits>), e [LDBL_MIN](<#/doc/types/limits>) é retornado.

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
        printf("sinh(1) = %f\nsinh(-1)=%f\n", sinh(1), sinh(-1));
        printf("log(sinh(1) + cosh(1))=%f\n", log(sinh(1) + cosh(1)));
     
        // special values
        printf("sinh(+0) = %f\nsinh(-0)=%f\n", sinh(0.0), sinh(-0.0));
     
        // error handling
        errno = 0; feclearexcept(FE_ALL_EXCEPT);
        printf("sinh(710.5) = %f\n", sinh(710.5));
        if (errno == ERANGE)
            perror("    errno == ERANGE");
        if (fetestexcept(FE_OVERFLOW))
            puts("    FE_OVERFLOW raised");
    }
```

Saída possível:
```
    sinh(1) = 1.175201
    sinh(-1)=-1.175201
    log(sinh(1) + cosh(1))=1.000000
    sinh(+0) = 0.000000
    sinh(-0)=-0.000000
    sinh(710.5) = inf
        errno == ERANGE: Numerical result out of range
        FE_OVERFLOW raised
```

### Referências

*   Padrão C23 (ISO/IEC 9899:2024):

    *   7.12.5.5 As funções sinh (p: TBD)

    *   7.25 Matemática genérica de tipo <tgmath.h> (p: TBD)

    *   F.10.2.5 As funções sinh (p: TBD)

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.12.5.5 As funções sinh (p: 176)

    *   7.25 Matemática genérica de tipo <tgmath.h> (p: 272-273)

    *   F.10.2.5 As funções sinh (p: 379)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.12.5.5 As funções sinh (p: 241-242)

    *   7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    *   F.10.2.5 As funções sinh (p: 520)

*   Padrão C99 (ISO/IEC 9899:1999):

    *   7.12.5.5 As funções sinh (p: 222)

    *   7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337)

    *   F.9.2.5 As funções sinh (p: 457)

*   Padrão C89/C90 (ISO/IEC 9899:1990):

    *   4.5.3.2 A função sinh

### Ver também

[ coshcoshfcoshl](<#/doc/numeric/math/cosh>)(C99)(C99) | calcula o cosseno hiperbólico (\\({\small\cosh{x} }\\)cosh(x))
(função)
[ tanhtanhftanhl](<#/doc/numeric/math/tanh>)(C99)(C99) | calcula a tangente hiperbólica (\\({\small\tanh{x} }\\)tanh(x))
(função)
[ asinhasinhfasinhl](<#/doc/numeric/math/asinh>)(C99)(C99)(C99) | calcula o seno hiperbólico inverso (\\({\small\operatorname{arsinh}{x} }\\)arsinh(x))
(função)
[ csinhcsinhfcsinhl](<#/doc/numeric/complex/csinh>)(C99)(C99)(C99) | calcula o seno hiperbólico complexo
(função)
[Documentação C++](<#/>) para sinh