# roundeven, roundevenf, roundevenl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float roundevenf( float arg );  // desde C23
double roundeven( double arg );  // desde C23
long double roundevenl( long double arg );  // desde C23
Definido no cabeçalho ``<tgmath.h>``
#define roundeven( arg )  // desde C23
```

1-3) Calcula o valor inteiro mais próximo de arg (em formato de ponto flutuante), arredondando casos de meio-ponto para o inteiro par mais próximo, independentemente do modo de arredondamento atual.

4) Macro genérica de tipo: Se arg tiver o tipo long double, `roundevenl` é chamada. Caso contrário, se arg tiver um tipo inteiro ou o tipo double, `roundeven` é chamada. Caso contrário, `roundevenf` é chamada, respectivamente.

### Parâmetros

- **arg** — valor de ponto flutuante

### Valor de retorno

Se nenhum erro ocorrer, o valor inteiro mais próximo de arg, arredondando casos de meio-ponto para o inteiro par mais próximo, é retornado.

### Tratamento de erros

Esta função não está sujeita a nenhum dos erros especificados em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559):

  * [FE_INEXACT](<#/doc/numeric/fenv/FE_exceptions>) nunca é levantado.
  * Se arg for ±∞, ele é retornado, sem modificação.
  * Se arg for ±0, ele é retornado, sem modificação.
  * Se arg for NaN, NaN é retornado.

### Exemplo

Execute este código
```c
    #include <math.h>
    #include <stdio.h>
    
    int main(void)
    {
        printf("roundeven(+2.4) = %+f\n", roundeven(2.4));
        printf("roundeven(-2.4) = %+f\n", roundeven(-2.4));
        printf("roundeven(+2.5) = %+f\n", roundeven(2.5));
        printf("roundeven(-2.5) = %+f\n", roundeven(-2.5));
        printf("roundeven(+2.6) = %+f\n", roundeven(2.6));
        printf("roundeven(-2.6) = %+f\n", roundeven(-2.6));
        printf("roundeven(+3.5) = %+f\n", roundeven(3.5));
        printf("roundeven(-3.5) = %+f\n", roundeven(-3.5));
        printf("roundeven(-0.0) = %+f\n", roundeven(-0.0));
        printf("roundeven(-Inf) = %+f\n",   roundeven(-INFINITY));
    }
```

Saída possível:
```
    roundeven(+2.4) = +2.000000
    roundeven(-2.4) = -2.000000
    roundeven(+2.5) = +2.000000
    roundeven(-2.5) = -2.000000
    roundeven(+2.6) = +3.000000
    roundeven(-2.6) = -3.000000
    roundeven(+3.5) = +4.000000
    roundeven(-3.5) = -4.000000
    roundeven(-0.0) = -0.000000
    roundeven(-Inf) = -inf
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.12.9.8 As funções roundeven (p: 265-266)

    

  * 7.27 Matemática genérica de tipo <tgmath.h> (p: 386-390)

    

  * F.10.6.8 As funções roundeven (p: 532)

### Veja também

[ rintrintfrintllrintlrintflrintlllrintllrintfllrintl](<#/doc/numeric/math/rint>)(C99)(C99)(C99)(C99)(C99)(C99)(C99)(C99)(C99) | arredonda para um inteiro usando o modo de arredondamento atual com exceção se o resultado for diferente (função)
[ roundroundfroundllroundlroundflroundlllroundllroundfllroundl](<#/doc/numeric/math/round>)(C99)(C99)(C99)(C99)(C99)(C99)(C99)(C99)(C99) | arredonda para o inteiro mais próximo, arredondando para longe de zero em casos de meio-ponto (função)