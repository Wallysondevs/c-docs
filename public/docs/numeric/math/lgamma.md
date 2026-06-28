# lgamma, lgammaf, lgammal

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float lgammaf( float arg );  // desde C99
double lgamma( double arg );  // desde C99
long double lgammal( long double arg );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define lgamma( arg )  // desde C99
```

  
1-3) Calcula o logaritmo natural do valor absoluto da [função gama](<https://en.wikipedia.org/wiki/Gamma_function> "enwiki:Gamma function") de arg.

4) Macro genérica de tipo: Se arg tiver o tipo long double, `lgammal` é chamada. Caso contrário, se arg tiver um tipo inteiro ou o tipo double, `lgamma` é chamada. Caso contrário, `lgammaf` é chamada.

### Parâmetros

arg  |  \-  |  valor de ponto flutuante   
  
### Valor de retorno

Se nenhum erro ocorrer, o valor do logaritmo da função gama de arg, ou seja \\(\log_{e}|{\int_0^\infty t^{arg-1} e^{-t} \mathsf{d}t}|\\)loge|∫∞  
0 _t_ arg-1  
_e_ -t d _t_ |, é retornado. 

Se ocorrer um erro de polo, [+HUGE_VAL](<#/doc/numeric/math/HUGE_VAL>), `+HUGE_VALF`, ou `+HUGE_VALL` é retornado. 

Se ocorrer um erro de intervalo devido a estouro, [±HUGE_VAL](<#/doc/numeric/math/HUGE_VAL>), `±HUGE_VALF`, ou `±HUGE_VALL` é retornado. 

### Tratamento de erros

Os erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>). 

Se arg for zero ou um inteiro menor que zero, um erro de polo pode ocorrer. 

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559), 

  * Se o argumento for 1, +0 é retornado. 
  * Se o argumento for 2, +0 é retornado. 
  * Se o argumento for ±0, +∞ é retornado e [FE_DIVBYZERO](<#/doc/numeric/fenv/FE_exceptions>) é levantado. 
  * Se o argumento for um inteiro negativo, +∞ é retornado e [FE_DIVBYZERO](<#/doc/numeric/fenv/FE_exceptions>) é levantado. 
  * Se o argumento for ±∞, +∞ é retornado. 
  * Se o argumento for NaN, NaN é retornado. 

### Notas

Se arg for um número natural, lgamma(arg) é o logaritmo do fatorial de arg - 1. 

A [versão POSIX de `lgamma`](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/lgamma.html>) não é thread-safe: cada execução da função armazena o sinal da função gama de arg na variável externa estática `signgam`. Algumas implementações fornecem `lgamma_r`, que recebe um ponteiro para armazenamento fornecido pelo usuário para singgam como o segundo parâmetro, e é thread-safe. 

Existe uma função não padronizada chamada `gamma` em várias implementações, mas sua definição é inconsistente. Por exemplo, a versão glibc e 4.2BSD de `gamma` executa `lgamma`, mas a versão 4.4BSD de `gamma` executa `tgamma`. 

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
        printf("lgamma(10) = %f, log(9!) = %f\n", lgamma(10),
                                                  log(2 * 3 * 4 * 5 * 6 * 7 * 8 * 9));
        const double pi = acos(-1);
        printf("lgamma(0.5) = %f, log(sqrt(pi)) = %f\n", log(sqrt(pi)), lgamma(0.5));
        // special values
        printf("lgamma(1) = %f\n", lgamma(1));
        printf("lgamma(+Inf) = %f\n", lgamma(INFINITY));
     
        // error handling
        errno = 0; feclearexcept(FE_ALL_EXCEPT);
        printf("lgamma(0) = %f\n", lgamma(0));
        if (errno == ERANGE)
            perror("    errno == ERANGE");
        if (fetestexcept(FE_DIVBYZERO))
            puts("    FE_DIVBYZERO raised");
    }
```

Saída possível: 
```
    lgamma(10) = 12.801827, log(9!) = 12.801827
    lgamma(0.5) = 0.572365, log(sqrt(pi)) = 0.572365
    lgamma(1) = 0.000000
    lgamma(+Inf) = inf
    lgamma(0) = inf
        errno == ERANGE: Numerical result out of range
        FE_DIVBYZERO raised
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.12.8.3 As funções lgamma (p: TBD) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: TBD) 

    

  * F.10.5.3 As funções lgamma (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.12.8.3 As funções lgamma (p: 182) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 272-273) 

    

  * F.10.5.3 As funções lgamma (p: 383) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.12.8.3 As funções lgamma (p: 250) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375) 

    

  * F.10.5.3 As funções lgamma (p: 525) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.12.8.3 As funções lgamma (p: 231) 

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337) 

    

  * F.9.5.3 As funções lgamma (p: 462) 

### Veja também

[ tgammatgammaftgammal](<#/doc/numeric/math/tgamma>)(C99)(C99)(C99) |  calcula a função gama   
(função)  
[Documentação C++](<#/>) para lgamma  
  
### Links externos

[Weisstein, Eric W. "Log Gamma Function."](<https://mathworld.wolfram.com/LogGammaFunction.html>) De MathWorld — Um Recurso Web da Wolfram.   
---