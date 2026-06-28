# asinh, asinhf, asinhl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float asinhf( float arg );  // desde C99
double asinh( double arg );  // desde C99
long double asinhl( long double arg );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define asinh( arg )  // desde C99
```

1-3) Calcula o seno hiperbólico inverso de arg.

4) Macro genérica de tipo: Se o argumento tiver o tipo long double, `asinhl` é chamada. Caso contrário, se o argumento tiver um tipo inteiro ou o tipo double, `asinh` é chamada. Caso contrário, `asinhf` é chamada. Se o argumento for complexo, então a macro invoca a função complexa correspondente ([casinhf](<#/doc/numeric/complex/casinh>), [casinh](<#/doc/numeric/complex/casinh>), [casinhl](<#/doc/numeric/complex/casinh>)).

### Parâmetros

- **arg** — valor de ponto flutuante representando a área de um setor hiperbólico

### Valor de retorno

Se nenhum erro ocorrer, o seno hiperbólico inverso de arg (sinh-1
(arg), ou arsinh(arg)), é retornado.

Se ocorrer um erro de faixa devido a underflow, o resultado correto (após arredondamento) é retornado.

### Tratamento de erros

Os erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559),

*   Se o argumento for ±0 ou ±∞, ele é retornado sem modificações.
*   Se o argumento for NaN, NaN é retornado.

### Notas

Embora o padrão C nomeie esta função como "seno hiperbólico de arco", as funções inversas das funções hiperbólicas são as funções de área. Seu argumento é a área de um setor hiperbólico, não um arco. O nome correto é "seno hiperbólico inverso" (usado por POSIX) ou "seno hiperbólico de área".

### Exemplo

Execute este código
```c
    #include <math.h>
    #include <stdio.h>
     
    int main(void)
    {
        printf("asinh(1) = %f\nasinh(-1) = %f\n", asinh(1), asinh(-1));
        // special values
        printf("asinh(+0) = %f\nasinh(-0) = %f\n", asinh(0.0), asinh(-0.0));
    }
```

Saída:
```
    asinh(1) = 0.881374
    asinh(-1) = -0.881374
    asinh(+0) = 0.000000
    asinh(-0) = -0.000000
```

### Referências

*   Padrão C23 (ISO/IEC 9899:2024):

    *   7.12.5.2 As funções asinh (p: 240-241)

    *   7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    *   F.10.2.2 As funções asinh (p: 520)

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.12.5.2 As funções asinh (p: 240-241)

    *   7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    *   F.10.2.2 As funções asinh (p: 520)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.12.5.2 As funções asinh (p: 240-241)

    *   7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    *   F.10.2.2 As funções asinh (p: 520)

*   Padrão C99 (ISO/IEC 9899:1999):

    *   7.12.5.2 As funções asinh (p: 221)

    *   7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337)

    *   F.9.2.2 As funções asinh (p: 457)

### Veja também

[ acoshacoshfacoshl](<#/doc/numeric/math/acosh>)(desde C99)(desde C99)(desde C99) | calcula o cosseno hiperbólico inverso (\\({\small\operatorname{arcosh}{x} }\\)arcosh(x))
(função)
[ atanhatanhfatanhl](<#/doc/numeric/math/atanh>)(desde C99)(desde C99)(desde C99) | calcula a tangente hiperbólica inversa (\\({\small\operatorname{artanh}{x} }\\)artanh(x))
(função)
[ sinhsinhfsinhl](<#/doc/numeric/math/sinh>)(desde C99)(desde C99) | calcula o seno hiperbólico (\\({\small\sinh{x} }\\)sinh(x))
(função)
[ casinhcasinhfcasinhl](<#/doc/numeric/complex/casinh>)(desde C99)(desde C99)(desde C99) | calcula o seno hiperbólico de arco complexo
(função)
[Documentação C++](<#/>) para asinh

### Links externos

[Weisstein, Eric W. "Seno Hiperbólico Inverso."](<https://mathworld.wolfram.com/InverseHyperbolicSine.html>) De MathWorld — Um Recurso Web da Wolfram.
---