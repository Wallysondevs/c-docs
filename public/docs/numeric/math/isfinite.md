# isfinite

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
#define isfinite(arg) /* implementation defined */  // desde C99
```

  
Determina se o número de ponto flutuante `arg` possui um valor finito, ou seja, se é normal, subnormal ou zero, mas não infinito ou NaN. A macro retorna um valor inteiro. 

[FLT_EVAL_METHOD](<#/doc/types/limits/FLT_EVAL_METHOD>) é ignorado: mesmo que o argumento seja avaliado com mais faixa e precisão do que seu tipo, ele é primeiro convertido para seu tipo semântico, e a classificação é baseada nisso. 

### Parâmetros

arg  |  \-  |  valor de ponto flutuante   
  
### Valor de retorno

Valor inteiro diferente de zero se `arg` tiver valor finito, ​0​ caso contrário. 

### Exemplo

Execute este código
```c
    #include <float.h>
    #include <math.h>
    #include <stdio.h>
     
    int main(void)
    {
        printf("isfinite(NAN)         = %d\n", isfinite(NAN));
        printf("isfinite(INFINITY)    = %d\n", isfinite(INFINITY));
        printf("isfinite(0.0)         = %d\n", isfinite(0.0));
        printf("isfinite(DBL_MIN/2.0) = %d\n", isfinite(DBL_MIN / 2.0));
        printf("isfinite(1.0)         = %d\n", isfinite(1.0));
        printf("isfinite(exp(800))    = %d\n", isfinite(exp(800)));
    }
```

Saída possível: 
```
    isfinite(NAN)         = 0
    isfinite(INFINITY)    = 0
    isfinite(0.0)         = 1
    isfinite(DBL_MIN/2.0) = 1
    isfinite(1.0)         = 1
    isfinite(exp(800))    = 0
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.12.3.2 A macro isfinite (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.12.3.2 A macro isfinite (p: TBD) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.12.3.2 A macro isfinite (p: 236) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.12.3.2 A macro isfinite (p: 216-217) 

### Veja também

[ fpclassify](<#/doc/numeric/math/fpclassify>)(C99) |  classifica o valor de ponto flutuante fornecido   
(macro de função)  
[ isinf](<#/doc/numeric/math/isinf>)(C99) |  verifica se o número fornecido é infinito   
(macro de função)  
[ isnan](<#/doc/numeric/math/isnan>)(C99) |  verifica se o número fornecido é NaN   
(macro de função)  
[ isnormal](<#/doc/numeric/math/isnormal>)(C99) |  verifica se o número fornecido é normal   
(macro de função)  
[Documentação C++](<#/>) para isfinite