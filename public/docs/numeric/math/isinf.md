# isinf

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
#define isinf(arg) /* implementation defined */  // desde C99
```

Determina se o número de ponto flutuante `arg` fornecido é infinito positivo ou negativo. A macro retorna um valor inteiro.

[FLT_EVAL_METHOD](<#/doc/types/limits/FLT_EVAL_METHOD>) é ignorado: mesmo que o argumento seja avaliado com mais faixa e precisão do que seu tipo, ele é primeiro convertido para seu tipo semântico, e a classificação é baseada nisso.

### Parâmetros

- **arg** — valor de ponto flutuante

### Valor de retorno

Valor inteiro diferente de zero se `arg` tiver um valor infinito, ​0​ caso contrário.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <math.h>
    #include <float.h>
     
    int main(void)
    {
        printf("isinf(NAN)         = %d\n", isinf(NAN));
        printf("isinf(INFINITY)    = %d\n", isinf(INFINITY));
        printf("isinf(0.0)         = %d\n", isinf(0.0));
        printf("isinf(DBL_MIN/2.0) = %d\n", isinf(DBL_MIN/2.0));
        printf("isinf(1.0)         = %d\n", isinf(1.0));
        printf("isinf(exp(800))    = %d\n", isinf(exp(800)));
    }
```

Saída possível:
```
    isinf(NAN)         = 0
    isinf(INFINITY)    = 1
    isinf(0.0)         = 0
    isinf(DBL_MIN/2.0) = 0
    isinf(1.0)         = 0
    isinf(exp(800))    = 1
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.12.3.3 A macro isinf (p: 172)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.12.3.3 A macro isinf (p: 236)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.12.3.3 A macro isinf (p: 217)

### Veja também

[ fpclassify](<#/doc/numeric/math/fpclassify>)(C99) | classifica o valor de ponto flutuante fornecido
(macro de função)
[ isfinite](<#/doc/numeric/math/isfinite>)(C99) | verifica se o número fornecido tem valor finito
(macro de função)
[ isnan](<#/doc/numeric/math/isnan>)(C99) | verifica se o número fornecido é NaN
(macro de função)
[ isnormal](<#/doc/numeric/math/isnormal>)(C99) | verifica se o número fornecido é normal
(macro de função)
[Documentação C++](<#/>) para isinf