# erfc, erfcf, erfcl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float erfcf( float arg );  // desde C99
double erfc( double arg );  // desde C99
long double erfcl( long double arg );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define erfc( arg )  // desde C99
```

1-3) Calcula a [função erro complementar](<https://en.wikipedia.org/wiki/Complementary_error_function> "enwiki:Complementary error function") de arg, ou seja, 1.0 - [erf](<#/doc/numeric/math/erf>)(arg), mas sem perda de precisão para valores grandes de arg.

4) Macro genérica de tipo: Se arg tiver o tipo long double, `erfcl` é chamada. Caso contrário, se arg tiver um tipo inteiro ou o tipo double, `erfc` é chamada. Caso contrário, `erfcf` é chamada.

### Parâmetros

- **arg** — valor de ponto flutuante

### Valor de retorno

Se nenhum erro ocorrer, o valor da função erro complementar de arg, ou seja, \\(\frac{2}{\sqrt{\pi} }\int_{arg}^{\infty}{e^{-{t^2} }\mathsf{d}t}\\)2
---
√π
∫∞
arg _e_ -t2
d _t_ ou \\({\small 1-\operatorname{erf}(arg)}\\)1-erf(arg), é retornado.

Se ocorrer um erro de intervalo devido a underflow, o resultado correto (após arredondamento) é retornado.

### Tratamento de erros

Os erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559),

  * Se o argumento for +∞, +0 é retornado.
  * Se o argumento for -∞, 2 é retornado.
  * Se o argumento for NaN, NaN é retornado.

### Notas

Para o tipo `double` compatível com IEEE, o underflow é garantido se arg > 26.55.

### Exemplo

Execute este código
```c
    #include <math.h>
    #include <stdio.h>
    
    double normalCDF(double x) // Phi(-∞, x) aka N(x)
    {
        return erfc(-x / sqrt(2)) / 2;
    }
    
    int main(void)
    {
        puts("normal cumulative distribution function:");
        for (double n = 0; n < 1; n += 0.1)
            printf("normalCDF(%.2f) %5.2f%%\n", n, 100 * normalCDF(n));
    
        printf("special values:\n"
               "erfc(-Inf) = %f\n"
               "erfc(Inf) = %f\n",
               erfc(-INFINITY),
               erfc(INFINITY));
    }
```

Saída:
```
    normal cumulative distribution function:
    normalCDF(0.00) 50.00%
    normalCDF(0.10) 53.98%
    normalCDF(0.20) 57.93%
    normalCDF(0.30) 61.79%
    normalCDF(0.40) 65.54%
    normalCDF(0.50) 69.15%
    normalCDF(0.60) 72.57%
    normalCDF(0.70) 75.80%
    normalCDF(0.80) 78.81%
    normalCDF(0.90) 81.59%
    normalCDF(1.00) 84.13%
    special values:
    erfc(-Inf) = 2.000000
    erfc(Inf) = 0.000000
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.12.8.2 As funções erfc (p: 249-250)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    

  * F.10.5.2 As funções erfc (p: 525)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.12.8.2 As funções erfc (p: 249-250)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    

  * F.10.5.2 As funções erfc (p: 525)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.12.8.2 As funções erfc (p: 249-250)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    

  * F.10.5.2 As funções erfc (p: 525)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.12.8.2 As funções erfc (p: 230)

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337)

    

  * F.9.5.2 As funções erfc (p: 462)

### Veja também

[ erferfferfl](<#/doc/numeric/math/erf>)(C99)(C99)(C99) | calcula a função erro
(função)
[Documentação C++](<#/>) para erfc

### Links externos

[Weisstein, Eric W. "Erfc."](<https://mathworld.wolfram.com/Erfc.html>) De MathWorld — Um Recurso Web da Wolfram.
---