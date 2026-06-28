# isunordered

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
#define isunordered(x, y) /* implementation defined */  // desde C99
```

  
Determina se os números de ponto flutuante x e y são não ordenados, ou seja, um ou ambos são NaN e, portanto, não podem ser comparados significativamente entre si.

### Parâmetros

x  |  \-  |  valor de ponto flutuante   
y  |  \-  |  valor de ponto flutuante   
  
### Valor de retorno

Valor inteiro diferente de zero se x ou y for NaN, ​0​ caso contrário.

### Exemplo

Execute este código
```c
    #include <math.h>
    #include <stdio.h>
     
    int main(void)
    {
        printf("isunordered(NAN,1.0) = %d\n", isunordered(NAN, 1.0));
        printf("isunordered(1.0,NAN) = %d\n", isunordered(1.0, NAN));
        printf("isunordered(NAN,NAN) = %d\n", isunordered(NAN, NAN));
        printf("isunordered(1.0,0.0) = %d\n", isunordered(1.0, 0.0));
     
        return 0;
    }
```

Saída possível: 
```
    isunordered(NAN,1.0) = 1
    isunordered(1.0,NAN) = 1
    isunordered(NAN,NAN) = 1
    isunordered(1.0,0.0) = 0
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.12.14.6 A macro isunordered (p: TBD) 

    

  * F.10.11 Macros de comparação (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.12.14.6 A macro isunordered (p: TBD) 

    

  * F.10.11 Macros de comparação (p: TBD) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.12.14.6 A macro isunordered (p: 261) 

    

  * F.10.11 Macros de comparação (p: 531) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.12.14.6 A macro isunordered (p: 242) 

### Veja também

[ fpclassify](<#/doc/numeric/math/fpclassify>)(C99) |  classifica o valor de ponto flutuante fornecido   
(macro de função)  
[ isnan](<#/doc/numeric/math/isnan>)(C99) |  verifica se o número fornecido é NaN   
(macro de função)  
[Documentação C++](<#/>) para isunordered