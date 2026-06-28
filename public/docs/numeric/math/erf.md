# erf, erff, erfl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float erff( float arg );  // desde C99
double erf( double arg );  // desde C99
long double erfl( long double arg );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define erf( arg )  // desde C99
```

  
1-3) Calcula a [função erro](<https://en.wikipedia.org/wiki/Error_function> "enwiki:Error function") de arg.

4) Macro genérica de tipo: Se arg tiver o tipo long double, `erfl` é chamada. Caso contrário, se arg tiver um tipo inteiro ou o tipo double, `erf` é chamada. Caso contrário, `erff` é chamada.

### Parâmetros

arg  |  \-  |  valor de ponto flutuante   
  
### Valor de retorno

Se nenhum erro ocorrer, o valor da função erro de arg, isto é \\(\frac{2}{\sqrt{\pi} }\int_{0}^{arg}{e^{-{t^2} }\mathsf{d}t}\\)2  
---  
√π  
∫arg  
0 _e_ -t2  
d _t_ , é retornado. Se ocorrer um erro de intervalo devido a underflow, o resultado correto (após arredondamento), isto é \\(\frac{2\cdot arg}{\sqrt{\pi} }\\)2*arg  
---  
√π  
, é retornado. 

### Tratamento de erros

Os erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>). 

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559), 

  * Se o argumento for ±0, ±0 é retornado 
  * Se o argumento for ±∞, ±1 é retornado 
  * Se o argumento for NaN, NaN é retornado 

### Notas

Underflow é garantido se |arg| < [DBL_MIN](<#/doc/types/limits>)*([sqrt](<#/doc/numeric/math/sqrt>)(π)/2). 

\\(\operatorname{erf}(\frac{x}{\sigma \sqrt{2} })\\)erf(x  
---  
σ√2  
) é a probabilidade de que uma medição cujos erros estão sujeitos a uma distribuição normal com desvio padrão \\(\sigma\\)σ esteja a menos de \\(x\\)x de distância do valor médio. 

### Exemplo

Execute este código
```c
    #include <math.h>
    #include <stdio.h>
     
    double phi(double x1, double x2)
    {
        return (erf(x2 / sqrt(2)) - erf(x1 / sqrt(2))) / 2;
    }
     
    int main(void)
    {
        puts("normal variate probabilities:");
        for (int n = -4; n < 4; ++n)
            printf("[%2d:%2d]: %5.2f%%\n", n, n + 1, 100 * phi(n, n + 1));
     
        puts("special values:");
        printf("erf(-0) = %f\n", erf(-0.0));
        printf("erf(Inf) = %f\n", erf(INFINITY));
    }
```

Saída: 
```
    normal variate probabilities:
    [-4:-3]:  0.13%
    [-3:-2]:  2.14%
    [-2:-1]: 13.59%
    [-1: 0]: 34.13%
    [ 0: 1]: 34.13%
    [ 1: 2]: 13.59%
    [ 2: 3]:  2.14%
    [ 3: 4]:  0.13%
    special values:
    erf(-0) = -0.000000
    erf(Inf) = 1.000000
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.12.8.1 As funções erf (p: 249) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375) 

    

  * F.10.5.1 As funções erf (p: 525) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.12.8.1 As funções erf (p: 230) 

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337) 

    

  * F.9.5.1 As funções erf (p: 462) 

### Veja também

[ erfcerfcferfcl](<#/doc/numeric/math/erfc>)(C99)(C99)(C99) | calcula a função erro complementar   
(função)  
[Documentação C++](<#/>) para erf  
  
### Links externos

[Weisstein, Eric W. "Erf."](<https://mathworld.wolfram.com/Erf.html>) De MathWorld — Um Recurso Web da Wolfram.   
---