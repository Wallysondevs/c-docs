# acosh, acoshf, acoshl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float acoshf( float arg );  // desde C99
double acosh( double arg );  // desde C99
long double acoshl( long double arg );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define acosh( arg )  // desde C99
```

1-3) Calcula o cosseno hiperbólico inverso de arg.

4) Macro de tipo genérico: Se o argumento tiver o tipo long double, `acoshl` é chamada. Caso contrário, se o argumento tiver um tipo inteiro ou o tipo double, `acosh` é chamada. Caso contrário, `acoshf` é chamada. Se o argumento for complexo, então a macro invoca a função complexa correspondente ([cacoshf](<#/doc/numeric/complex/cacosh>), [cacosh](<#/doc/numeric/complex/cacosh>), [cacoshl](<#/doc/numeric/complex/cacosh>)).

### Parâmetros

- **arg** — valor de ponto flutuante representando a área de um setor hiperbólico

### Valor de retorno

Se nenhum erro ocorrer, o cosseno hiperbólico inverso de arg (cosh-1
(arg), ou arcosh(arg)) no intervalo [0, +∞], é retornado.

Se ocorrer um erro de domínio, um valor definido pela implementação é retornado (NaN onde suportado).

### Tratamento de erros

Os erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Se o argumento for menor que 1, ocorre um erro de domínio.

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559),

  * Se o argumento for menor que 1, [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado e um NaN é retornado.
  * Se o argumento for 1, +0 é retornado.
  * Se o argumento for +∞, +∞ é retornado.
  * Se o argumento for NaN, NaN é retornado.

### Notas

Embora o padrão C nomeie esta função como "cosseno hiperbólico de arco", as funções inversas das funções hiperbólicas são as funções de área. Seu argumento é a área de um setor hiperbólico, não um arco. O nome correto é "cosseno hiperbólico inverso" (usado por POSIX) ou "cosseno hiperbólico de área".

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
        printf("acosh(1) = %f\nacosh(10) = %f\n", acosh(1), acosh(10));
        printf("acosh(DBL_MAX) = %f\nacosh(Inf) = %f\n", acosh(DBL_MAX), acosh(INFINITY));
     
        // error handling
        errno = 0; feclearexcept(FE_ALL_EXCEPT);
        printf("acosh(0.5) = %f\n", acosh(0.5));
        if (errno == EDOM)
            perror("    errno == EDOM");
        if (fetestexcept(FE_INVALID))
            puts("    FE_INVALID raised");
    }
```

Saída possível:
```
    acosh(1) = 0.000000
    acosh(10) = 2.993223
    acosh(DBL_MAX) = 710.475860
    acosh(Inf) = inf
    acosh(0.5) = -nan
        errno == EDOM: Numerical argument out of domain
        FE_INVALID raised
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.12.5.1 As funções acosh (p: TBD)

    

  * 7.27 Matemática de tipo genérico <tgmath.h> (p: TBD)

    

  * F.10.2.1 As funções acosh (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.12.5.1 As funções acosh (p: 175)

    

  * 7.25 Matemática de tipo genérico <tgmath.h> (p: 272-273)

    

  * F.10.2.1 As funções acosh (p: 379)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.12.5.1 As funções acosh (p: 240)

    

  * 7.25 Matemática de tipo genérico <tgmath.h> (p: 373-375)

    

  * F.10.2.1 As funções acosh (p: 520)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.12.5.1 As funções acosh (p: 221)

    

  * 7.22 Matemática de tipo genérico <tgmath.h> (p: 335-337)

    

  * F.9.2.1 As funções acosh (p: 457)

### Veja também

[ asinhasinhfasinhl](<#/doc/numeric/math/asinh>)(C99)(C99)(C99) | calcula o seno hiperbólico inverso (\\({\small\operatorname{arsinh}{x} }\\)arsinh(x))
(função)
[ atanhatanhfatanhl](<#/doc/numeric/math/atanh>)(C99)(C99)(C99) | calcula a tangente hiperbólica inversa (\\({\small\operatorname{artanh}{x} }\\)artanh(x))
(função)
[ coshcoshfcoshl](<#/doc/numeric/math/cosh>)(C99)(C99) | calcula o cosseno hiperbólico (\\({\small\cosh{x} }\\)cosh(x))
(função)
[ cacoshcacoshfcacoshl](<#/doc/numeric/complex/cacosh>)(C99)(C99)(C99) | calcula o cosseno hiperbólico de arco complexo
(função)
[Documentação C++](<#/>) para acosh

### Links externos

[Weisstein, Eric W. "Cosseno Hiperbólico Inverso."](<https://mathworld.wolfram.com/InverseHyperbolicCosine.html>) De MathWorld — Um Recurso Web da Wolfram.
---