# copysign, copysignf, copysignl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)`

```c
float copysignf( float x, float y );  // desde C99
double copysign( double x, double y );  // desde C99
long double copysignl( long double x, long double y );  // desde C99
Definido no cabeçalho `<tgmath.h>``
#define copysign(x, y)  // desde C99
```

  
1-3) Compõe um valor de ponto flutuante com a magnitude de `x` e o sinal de `y`.

4) Macro genérica de tipo: Se qualquer argumento tiver o tipo long double, `copysignl` é chamada. Caso contrário, se qualquer argumento tiver um tipo inteiro ou o tipo double, `copysign` é chamada. Caso contrário, `copysignf` é chamada.

### Parâmetros

x, y  |  \-  |  valores de ponto flutuante   
  
### Valor de retorno

Se nenhum erro ocorrer, o valor de ponto flutuante com a magnitude de `x` e o sinal de `y` é retornado. 

Se `x` for NaN, então NaN com o sinal de `y` é retornado. 

Se `y` for -0, o resultado é negativo apenas se a implementação suportar o zero com sinal consistentemente em operações aritméticas. 

### Tratamento de erros

Esta função não está sujeita a nenhum erro especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>). 

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559), 

  * O valor retornado é exato ([FE_INEXACT](<#/doc/numeric/fenv/FE_exceptions>) nunca é levantado) e independente do [modo de arredondamento](<#/doc/numeric/fenv/FE_round>) atual. 

### Notas

`copysign` é a única maneira portátil de manipular o sinal de um valor NaN (para examinar o sinal de um NaN, [signbit](<#/doc/numeric/math/signbit>) também pode ser usado). 

### Exemplo

Execute este código
```c
    #include <math.h>
    #include <stdio.h>
    
    int main(void)
    {
        printf("copysign(1.0,+2.0)      = %+1.1f\n", copysign(1.0,+2.0));
        printf("copysign(1.0,-2.0)      = %+1.1f\n", copysign(1.0,-2.0));
        printf("copysign(INFINITY,-2.0) = %f\n",    copysign(INFINITY,-2.0));
        printf("copysign(NAN,-2.0)      = %f\n",    copysign(NAN,-2.0));
    }
```

Saída possível: 
```
    copysign(1.0,+2.0)      = +1.0
    copysign(1.0,-2.0)      = -1.0
    copysign(INFINITY,-2.0) = -inf
    copysign(NAN,-2.0)      = -nan
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.12.11.1 As funções copysign (p: TBD) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: TBD) 

    

  * F.10.8.1 As funções copysign (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.12.11.1 As funções copysign (p: TBD) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: TBD) 

    

  * F.10.8.1 As funções copysign (p: TBD) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.12.11.1 As funções copysign (p: 255) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375) 

    

  * F.10.8.1 As funções copysign (p: 529) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.12.11.1 As funções copysign (p: 236) 

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337) 

    

  * F.9.8.1 As funções copysign (p: 465) 

### Veja também

[ fabsfabsffabsl](<#/doc/numeric/math/fabs>)(C99)(C99) | calcula o valor absoluto de um valor de ponto flutuante (\\(\small{|x|}\\)|x|)   
(função)  
[ signbit](<#/doc/numeric/math/signbit>)(C99) | verifica se o número dado é negativo   
(macro de função)  
[Documentação C++](<#/>) para copysign