# sqrt, sqrtf, sqrtl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float sqrtf( float arg );  // desde C99
double sqrt( double arg );
long double sqrtl( long double arg );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define sqrt( arg )  // desde C99
```

1-3) Calcula a raiz quadrada de arg.

4) Macro genérica de tipo: Se arg tiver o tipo long double, `sqrtl` é chamada. Caso contrário, se arg tiver um tipo inteiro ou o tipo double, `sqrt` é chamada. Caso contrário, `sqrtf` é chamada. Se arg for complexo ou imaginário, então a macro invoca a função complexa correspondente ([csqrtf](<#/doc/numeric/complex/csqrt>), [csqrt](<#/doc/numeric/complex/csqrt>), [csqrtl](<#/doc/numeric/complex/csqrt>)).

### Parâmetros

- **arg** — valor de ponto flutuante

### Valor de retorno

Se nenhum erro ocorrer, a raiz quadrada de arg (\\({\small \sqrt{arg} }\\)√arg) é retornada.

Se ocorrer um erro de domínio, um valor definido pela implementação é retornado (NaN onde suportado).

Se ocorrer um erro de faixa devido a underflow, o resultado correto (após arredondamento) é retornado.

### Tratamento de erros

Os erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Ocorre um erro de domínio se arg for menor que zero.

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559),

*   Se o argumento for menor que -0, [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado e NaN é retornado.
*   Se o argumento for +∞ ou ±0, ele é retornado, sem modificação.
*   Se o argumento for NaN, NaN é retornado.

### Notas

`sqrt` é exigido pelo padrão IEEE para ser corretamente arredondado a partir do resultado infinitamente preciso. Em particular, o resultado exato é produzido se puder ser representado no tipo de ponto flutuante. As únicas outras operações que exigem isso são os [operadores aritméticos](<#/doc/language/operator_arithmetic>) e a função [fma](<#/doc/numeric/math/fma>). Outras funções, incluindo [pow](<#/doc/numeric/math/pow>), não são tão restritas.

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
        // normal use
        printf("sqrt(100) = %f\n", sqrt(100));
        printf("sqrt(2) = %f\n", sqrt(2));
        printf("golden ratio = %f\n", (1 + sqrt(5)) / 2);
    
        // special values
        printf("sqrt(-0) = %f\n", sqrt(-0.0));
    
        // error handling
        errno = 0; feclearexcept(FE_ALL_EXCEPT);
        printf("sqrt(-1.0) = %f\n", sqrt(-1));
        if (errno == EDOM)
            perror("    errno == EDOM");
        if (fetestexcept(FE_INVALID))
            puts("    FE_INVALID was raised");
    }
```

Saída possível:
```
    sqrt(100) = 10.000000
    sqrt(2) = 1.414214
    golden ratio = 1.618034
    sqrt(-0) = -0.000000
    sqrt(-1.0) = -nan
        errno = EDOM: Numerical argument out of domain
        FE_INVALID was raised
```

### Referências

*   Padrão C23 (ISO/IEC 9899:2024):

    *   7.12.7.5 As funções sqrt (p: TBD)

    *   7.25 Matemática genérica de tipo <tgmath.h> (p: TBD)

    *   F.10.4.5 As funções sqrt (p: TBD)

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.12.7.5 As funções sqrt (p: TBD)

    *   7.25 Matemática genérica de tipo <tgmath.h> (p: TBD)

    *   F.10.4.5 As funções sqrt (p: TBD)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.12.7.5 As funções sqrt (p: 249)

    *   7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    *   F.10.4.5 As funções sqrt (p: 525)

*   Padrão C99 (ISO/IEC 9899:1999):

    *   7.12.7.5 As funções sqrt (p: 229-230)

    *   7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337)

    *   F.9.4.5 As funções sqrt (p: 462)

*   Padrão C89/C90 (ISO/IEC 9899:1990):

    *   4.5.5.2 A função sqrt

### Veja também

[powpowfpowl](<#/doc/numeric/math/pow>)(C99)(C99) | calcula um número elevado a uma dada potência (\\(\small{x^y}\\)xy)
(função)
[cbrtcbrtfcbrtl](<#/doc/numeric/math/cbrt>)(C99)(C99)(C99) | calcula a raiz cúbica (\\(\small{\sqrt[3]{x} }\\)3√x)
(função)
[hypothypotfhypotl](<#/doc/numeric/math/hypot>)(C99)(C99)(C99) | calcula a raiz quadrada da soma dos quadrados de dois números dados (\\(\scriptsize{\sqrt{x^2+y^2} }\\)√x2
+y2
)
(função)
[csqrtcsqrtfcsqrtl](<#/doc/numeric/complex/csqrt>)(C99)(C99)(C99) | calcula a raiz quadrada complexa
(função)
[Documentação C++](<#/>) para sqrt