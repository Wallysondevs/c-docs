# fmax, fmaxf, fmaxl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float fmaxf( float x, float y );  // desde C99
double fmax( double x, double y );  // desde C99
long double fmaxl( long double x, long double y );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define fmax( x, y )  // desde C99
```

  
1-3) Retorna o maior de dois argumentos de ponto flutuante, tratando NaNs como dados ausentes (entre um NaN e um valor numérico, o valor numérico é escolhido).

4) Macro genérica de tipo: Se qualquer argumento tiver o tipo `long double`, `fmaxl` é chamada. Caso contrário, se qualquer argumento tiver um tipo inteiro ou o tipo `double`, `fmax` é chamada. Caso contrário, `fmaxf` é chamada.

### Parâmetros

x, y  |  \-  |  valores de ponto flutuante   
  
### Valor de retorno

Se bem-sucedida, retorna o maior de dois valores de ponto flutuante. O valor retornado é exato e não depende de nenhum modo de arredondamento. 

### Tratamento de erros

Esta função não está sujeita a nenhuma das condições de erro especificadas em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>). 

Se a implementação suporta aritmética de ponto flutuante IEEE (IEC 60559), 

  * Se um dos dois argumentos for NaN, o valor do outro argumento é retornado. 
  * Somente se ambos os argumentos forem NaN, NaN é retornado. 

### Notas

Esta função não é obrigada a ser sensível ao sinal de zero, embora algumas implementações adicionalmente imponham que, se um argumento for +0 e o outro for -0, então +0 é retornado. 

### Exemplo

Execute este código
```
    #include <math.h>
    #include <stdio.h>
     
    int main(void)
    {
        printf("fmax(2,1)    = %f\n", fmax(2,1));
        printf("fmax(-Inf,0) = %f\n", fmax(-INFINITY,0));
        printf("fmax(NaN,-1) = %f\n", fmax(NAN,-1));
    }
```

Saída: 
```
    fmax(2,1)    = 2.000000
    fmax(-Inf,0) = 0.000000
    fmax(NaN,-1) = -1.000000
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.12.12.2 As funções fmax (p: TBD) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: TBD) 

    

  * F.10.9.2 As funções fmax (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.12.12.2 As funções fmax (p: 188) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 397) 

    

  * F.10.9.2 As funções fmax (p: 386) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.12.12.2 As funções fmax (p: 257-258) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375) 

    

  * F.10.9.2 As funções fmax (p: 530) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.12.12.2 As funções fmax (p: 238-239) 

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337) 

    

  * F.9.9.2 As funções fmax (p: 466) 

### Veja também

[ isgreater](<#/doc/numeric/math/isgreater>)(C99) |  verifica se o primeiro argumento de ponto flutuante é maior que o segundo   
(macro de função)  
[ fminfminffminl](<#/doc/numeric/math/fmin>)(C99)(C99)(C99) |  determina o menor de dois valores de ponto flutuante   
(função)  
[Documentação C++](<#/>) para fmax