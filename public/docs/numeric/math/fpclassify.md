# fpclassify

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
#define fpclassify(arg) /* implementation defined */  // desde C99
```

  
Categoriza o valor de ponto flutuante arg nas seguintes categorias: zero, subnormal, normal, infinito, NAN, ou categoria definida pela implementação. A macro retorna um valor inteiro. 

[FLT_EVAL_METHOD](<#/doc/types/limits/FLT_EVAL_METHOD>) é ignorado: mesmo que o argumento seja avaliado com mais faixa e precisão do que seu tipo, ele é primeiro convertido para seu tipo semântico, e a classificação é baseada nisso: um valor normal de long double pode se tornar subnormal quando convertido para double e zero quando convertido para float. 

### Parâmetros

arg  |  \-  |  valor de ponto flutuante   
  
### Valor de retorno

Um de [FP_INFINITE](<#/doc/numeric/math/FP_categories>), [FP_NAN](<#/doc/numeric/math/FP_categories>), [FP_NORMAL](<#/doc/numeric/math/FP_categories>), [FP_SUBNORMAL](<#/doc/numeric/math/FP_categories>), [FP_ZERO](<#/doc/numeric/math/FP_categories>) ou tipo definido pela implementação, especificando a categoria de arg. 

### Exemplo

Execute este código
```
    #include <float.h>
    #include <math.h>
    #include <stdio.h>
     
    const char* show_classification(double x)
    {
        switch(fpclassify(x))
        {
            case FP_INFINITE:  return "Inf";
            case FP_NAN:       return "NaN";
            case FP_NORMAL:    return "normal";
            case FP_SUBNORMAL: return "subnormal";
            case FP_ZERO:      return "zero";
            default:           return "unknown";
        }
    }
     
    int main(void)
    {
        printf("1.0/0.0 is %s\n", show_classification(1 / 0.0));
        printf("0.0/0.0 is %s\n", show_classification(0.0 / 0.0));
        printf("DBL_MIN/2 is %s\n", show_classification(DBL_MIN / 2));
        printf("-0.0 is %s\n", show_classification(-0.0));
        printf("1.0 is %s\n", show_classification(1.0));
    }
```

Saída: 
```
    1.0/0.0 is Inf
    0.0/0.0 is NaN
    DBL_MIN/2 is subnormal
    -0.0 is zero
    1.0 is normal
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.12.3.1 A macro fpclassify (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.12.3.1 A macro fpclassify (p: TBD) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.12.3.1 A macro fpclassify (p: 235) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.12.3.1 A macro fpclassify (p: 216) 

### Veja também

[ isfinite](<#/doc/numeric/math/isfinite>)(C99) |  verifica se o número dado tem valor finito   
(macro de função)  
[ isinf](<#/doc/numeric/math/isinf>)(C99) |  verifica se o número dado é infinito   
(macro de função)  
[ isnan](<#/doc/numeric/math/isnan>)(C99) |  verifica se o número dado é NaN   
(macro de função)  
[ isnormal](<#/doc/numeric/math/isnormal>)(C99) |  verifica se o número dado é normal   
(macro de função)  
[documentação C++](<#/>) para fpclassify