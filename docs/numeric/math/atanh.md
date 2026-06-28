# atanh, atanhf, atanhl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float atanhf( float arg );  // desde C99
double atanh( double arg );  // desde C99
long double atanhl( long double arg );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define atanh( arg )  // desde C99
```

1-3) Calcula a tangente hiperbólica inversa de arg.

4) Macro genérica de tipo: Se o argumento tiver o tipo long double, `atanhl` é chamada. Caso contrário, se o argumento tiver um tipo inteiro ou o tipo double, `atanh` é chamada. Caso contrário, `atanhf` é chamada. Se o argumento for complexo, a macro invoca a função complexa correspondente ([catanhf](<#/doc/numeric/complex/catanh>), [catanh](<#/doc/numeric/complex/catanh>), [catanhl](<#/doc/numeric/complex/catanh>)).

### Parâmetros

- **arg** — valor de ponto flutuante representando a área de um setor hiperbólico

### Valor de retorno

Se nenhum erro ocorrer, a tangente hiperbólica inversa de arg (tanh-1
(arg), ou artanh(arg)), é retornada.

Se ocorrer um erro de domínio, um valor definido pela implementação é retornado (NaN onde suportado).

Se ocorrer um erro de polo, ±[HUGE_VAL](<#/doc/numeric/math/HUGE_VAL>), `±HUGE_VALF`, ou `±HUGE_VALL` é retornado (com o sinal correto).

Se ocorrer um erro de intervalo devido a underflow, o resultado correto (após arredondamento) é retornado.

### Tratamento de erros

Os erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Se o argumento não estiver no intervalo `[`-1`, `+1`]`, ocorre um erro de intervalo.

Se o argumento for ±1, ocorre um erro de polo.

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559),

  * Se o argumento for ±0, ele é retornado sem modificações.
  * Se o argumento for ±1, ±∞ é retornado e [FE_DIVBYZERO](<#/doc/numeric/fenv/FE_exceptions>) é levantado.
  * Se |arg|>1, NaN é retornado e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado.
  * Se o argumento for NaN, NaN é retornado.

### Notas

Embora o padrão C nomeie esta função como "tangente hiperbólica de arco", as funções inversas das funções hiperbólicas são as funções de área. Seu argumento é a área de um setor hiperbólico, não um arco. O nome correto é "tangente hiperbólica inversa" (usado por POSIX) ou "tangente hiperbólica de área".

[POSIX especifica](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/atanh.html>) que, em caso de underflow, arg é retornado sem modificações, e se isso não for suportado, um valor definido pela implementação não maior que [DBL_MIN](<#/doc/types/limits>), [FLT_MIN](<#/doc/types/limits>), e [LDBL_MIN](<#/doc/types/limits>) é retornado.

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
        printf("atanh(0) = %f\natanh(-0) = %f\n", atanh(0), atanh(-0.0));
        printf("atanh(0.9) = %f\n", atanh(0.9));
     
        // error handling
        errno = 0; feclearexcept(FE_ALL_EXCEPT);
        printf("atanh(-1) = %f\n", atanh(-1));
        if (errno == ERANGE)
            perror("    errno == ERANGE");
        if (fetestexcept(FE_DIVBYZERO))
            puts("    FE_DIVBYZERO raised");
    }
```

Saída possível:
```
    atanh(0) = 0.000000
    atanh(-0) = -0.000000
    atanh(0.9) = 1.472219
    atanh(-1) = -inf
        errno == ERANGE: Numerical result out of range
        FE_DIVBYZERO raised
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.12.5.3 As funções atanh (p: 241)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    

  * F.10.2.3 As funções atanh (p: 520)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.12.5.3 As funções atanh (p: TBD)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: TBD)

    

  * F.10.2.3 As funções atanh (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.12.5.3 As funções atanh (p: 241)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    

  * F.10.2.3 As funções atanh (p: 520)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.12.5.3 As funções atanh (p: 221-222)

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337)

    

  * F.9.2.3 As funções atanh (p: 457)

### Veja também

[asinh asinhf asinhl](<#/doc/numeric/math/asinh>)(C99)(C99)(C99) | calcula o seno hiperbólico inverso (\\({\small\operatorname{arsinh}{x} }\\)arsinh(x))
(função)
[acosh acoshf acoshl](<#/doc/numeric/math/acosh>)(C99)(C99)(C99) | calcula o cosseno hiperbólico inverso (\\({\small\operatorname{arcosh}{x} }\\)arcosh(x))
(função)
[tanh tanhf tanhl](<#/doc/numeric/math/tanh>)(C99)(C99) | calcula a tangente hiperbólica (\\({\small\tanh{x} }\\)tanh(x))
(função)
[catanh catanhf catanhl](<#/doc/numeric/complex/catanh>)(C99)(C99)(C99) | calcula a tangente hiperbólica de arco complexa
(função)
[Documentação C++](<#/>) para atanh

### Links externos

[Weisstein, Eric W. "Inverse Hyperbolic Tangent."](<https://mathworld.wolfram.com/InverseHyperbolicTangent.html>) De MathWorld — Um Recurso Web da Wolfram.
---