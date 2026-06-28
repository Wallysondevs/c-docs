# FP_NORMAL, FP_SUBNORMAL, FP_ZERO, FP_INFINITE, FP_NAN

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
#define FP_NORMAL /*definido pela implementação*/  // desde C99
#define FP_SUBNORMAL /*definido pela implementação*/  // desde C99
#define FP_ZERO /*definido pela implementação*/  // desde C99
#define FP_INFINITE /*definido pela implementação*/  // desde C99
#define FP_NAN /*definido pela implementação*/  // desde C99
```

As macros `FP_NORMAL`, `FP_SUBNORMAL`, `FP_ZERO`, `FP_INFINITE`, `FP_NAN` representam cada uma uma categoria distinta de números de ponto flutuante. Todas elas se expandem para uma expressão de constante inteira.

Constante | Explicação
`FP_NORMAL` | indica que o valor é _normal_, ou seja, não é um infinito, subnormal, não-é-um-número ou zero
`FP_SUBNORMAL` | indica que o valor é [_subnormal_](<https://en.wikipedia.org/wiki/Subnormal_number> "enwiki:Subnormal number")
`FP_ZERO` | indica que o valor é zero positivo ou negativo
`FP_INFINITE` | indica que o valor não é representável pelo tipo subjacente (infinito positivo ou negativo)
`FP_NAN` | indica que o valor é não-é-um-número (NaN)

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <math.h>
    #include <float.h>
     
    const char *show_classification(double x) {
        switch(fpclassify(x)) {
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
        printf("1.0/0.0 is %s\n", show_classification(1/0.0));
        printf("0.0/0.0 is %s\n", show_classification(0.0/0.0));
        printf("DBL_MIN/2 is %s\n", show_classification(DBL_MIN/2));
        printf("-0.0 is %s\n", show_classification(-0.0));
        printf(" 1.0 is %s\n", show_classification(1.0));
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

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.12/6 FP_NORMAL, ... (p: 169-170)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.12/6 FP_NORMAL, ... (p: 232)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.12/6 FP_NORMAL, ... (p: 213)

### Veja também

[ fpclassify](<#/doc/numeric/math/fpclassify>)(C99) | classifica o valor de ponto flutuante fornecido
(macro de função)
[Documentação C++](<#/>) para FP_categories