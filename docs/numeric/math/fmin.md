# fmin, fminf, fminl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float fminf( float x, float y );  // desde C99
double fmin( double x, double y );  // desde C99
long double fminl( long double x, long double y );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define fmin( x, y )  // desde C99
```

1-3) Retorna o menor de dois argumentos de ponto flutuante, tratando NaNs como dados ausentes (entre um NaN e um valor numérico, o valor numérico é escolhido).

4) Macro de tipo genérico: Se qualquer argumento tiver o tipo long double, `fminl` é chamada. Caso contrário, se qualquer argumento tiver um tipo inteiro ou o tipo double, `fmin` é chamada. Caso contrário, `fminf` é chamada.

### Parâmetros

- **x, y** — valores de ponto flutuante

### Valor de retorno

Se bem-sucedida, retorna o menor de dois valores de ponto flutuante. O valor retornado é exato e não depende de nenhum modo de arredondamento.

### Tratamento de erros

Esta função não está sujeita a nenhuma das condições de erro especificadas em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Se a implementação suporta aritmética de ponto flutuante IEEE (IEC 60559),

  * Se um dos dois argumentos for NaN, o valor do outro argumento é retornado
  * Somente se ambos os argumentos forem NaN, NaN é retornado

### Observações

Esta função não é obrigada a ser sensível ao sinal de zero, embora algumas implementações adicionalmente imponham que se um argumento for +0 e o outro for -0, então -0 é retornado.

### Exemplo

Execute este código
```c
    #include <math.h>
    #include <stdio.h>
    
    int main(void)
    {
        printf("fmin(2,1)    = %f\n", fmin(2, 1));
        printf("fmin(-Inf,0) = %f\n", fmin(-INFINITY, 0));
        printf("fmin(NaN,-1) = %f\n", fmin(NAN, -1));
    }
```

Saída possível:
```
    fmin(2,1)    = 1.000000
    fmin(-Inf,0) = -inf
    fmin(NaN,-1) = -1.000000
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.12.12.3 As funções fmin (p: TBD)

    

  * 7.25 Matemática de tipo genérico <tgmath.h> (p: TBD)

    

  * F.10.9.3 As funções fmin (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.12.12.3 As funções fmin (p: TBD)

    

  * 7.25 Matemática de tipo genérico <tgmath.h> (p: TBD)

    

  * F.10.9.3 As funções fmin (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.12.12.3 As funções fmin (p: 258)

    

  * 7.25 Matemática de tipo genérico <tgmath.h> (p: 373-375)

    

  * F.10.9.3 As funções fmin (p: 530)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.12.12.3 As funções fmin (p: 239)

    

  * 7.22 Matemática de tipo genérico <tgmath.h> (p: 335-337)

    

  * F.9.9.3 As funções fmin (p: 466)

### Veja também

[`isless`](<#/doc/numeric/math/isless>)(C99) | verifica se o primeiro argumento de ponto flutuante é menor que o segundo
(macro de função)
[`fmaxfmaxffmaxl`](<#/doc/numeric/math/fmax>)(C99)(C99)(C99) | determina o maior de dois valores de ponto flutuante
(função)
[documentação C++](<#/>) para fmin