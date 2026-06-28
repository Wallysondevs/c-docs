# float_t, double_t

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
typedef /* definido pela implementação */ float_t  // desde C99
typedef /* definido pela implementação */ double_t  // desde C99
```

Os tipos float_t e double_t são tipos de ponto flutuante pelo menos tão largos quanto float e double, respectivamente, e tais que double_t é pelo menos tão largo quanto float_t. O valor de [FLT_EVAL_METHOD](<#/doc/types/limits/FLT_EVAL_METHOD>) determina os tipos de float_t e double_t.

`FLT_EVAL_METHOD` | Explicação
​0​ | float_t e double_t são equivalentes a float e double, respectivamente
1 | ambos float_t e double_t são equivalentes a double
2 | ambos float_t e double_t são equivalentes a long double
outro | ambos float_t e double_t são definidos pela implementação

### Exemplo

Execute este código
```c
    #include <float.h>
    #include <math.h>
    #include <stdio.h>
    
    #define SHOW(expr) printf("%s = %d\n", #expr, (int)(expr))
    
    int main()
    {
        SHOW(FLT_EVAL_METHOD);
        SHOW(sizeof(float));
        SHOW(sizeof(float_t));
        SHOW(sizeof(double));
        SHOW(sizeof(double_t));
    }
```

Saída possível:
```
    FLT_EVAL_METHOD = 1
    sizeof(float) = 4
    sizeof(float_t) = 8
    sizeof(double) = 8
    sizeof(double_t) = 8
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.12 Matemática <math.h> (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.12 Matemática <math.h> (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.12 Matemática <math.h> (p: 231)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.12 Matemática <math.h> (p: 212)

### Veja também

[ FLT_EVAL_METHOD](<#/doc/types/limits/FLT_EVAL_METHOD>)(C99) | especifica em qual precisão todas as operações aritméticas são realizadas
(constante de macro)