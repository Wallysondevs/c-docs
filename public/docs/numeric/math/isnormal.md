# isnormal

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
#define isnormal(arg) /* implementation defined */  // desde C99
```

  
Determina se o número de ponto flutuante `arg` fornecido é normal, ou seja, não é zero, subnormal, infinito, nem `NaN`. A macro retorna um valor inteiro. 

[FLT_EVAL_METHOD](<#/doc/types/limits/FLT_EVAL_METHOD>) é ignorado: mesmo que o argumento seja avaliado com mais faixa e precisão do que seu tipo, ele é primeiro convertido para seu tipo semântico, e a classificação é baseada nisso. 

### Parâmetros

arg  |  \-  |  valor de ponto flutuante   
  
### Valor de retorno

Valor inteiro diferente de zero se `arg` for normal, ​0​ caso contrário. 

### Exemplo

Execute este código
```c
    #include <float.h>
    #include <math.h>
    #include <stdio.h>
     
    int main(void)
    {
        printf("isnormal(NAN)         = %d\n", isnormal(NAN));
        printf("isnormal(INFINITY)    = %d\n", isnormal(INFINITY));
        printf("isnormal(0.0)         = %d\n", isnormal(0.0));
        printf("isnormal(DBL_MIN/2.0) = %d\n", isnormal(DBL_MIN / 2.0));
        printf("isnormal(1.0)         = %d\n", isnormal(1.0));
    }
```

Saída: 
```
    isnormal(NAN)         = 0
    isnormal(INFINITY)    = 0
    isnormal(0.0)         = 0
    isnormal(DBL_MIN/2.0) = 0
    isnormal(1.0)         = 1
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.12.3.5 A macro isnormal (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.12.3.5 A macro isnormal (p: TBD) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.12.3.5 A macro isnormal (p: 237) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.12.3.5 A macro isnormal (p: 217-218) 

### Veja também

[ fpclassify](<#/doc/numeric/math/fpclassify>)(C99) |  classifica o valor de ponto flutuante fornecido   
(macro de função)  
[ isfinite](<#/doc/numeric/math/isfinite>)(C99) |  verifica se o número fornecido tem valor finito   
(macro de função)  
[ isinf](<#/doc/numeric/math/isinf>)(C99) |  verifica se o número fornecido é infinito   
(macro de função)  
[ isnan](<#/doc/numeric/math/isnan>)(C99) |  verifica se o número fornecido é NaN   
(macro de função)  
[Documentação C++](<#/>) para isnormal