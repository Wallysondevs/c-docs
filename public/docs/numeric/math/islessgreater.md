# islessgreater

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)`

```c
#define islessgreater(x, y) /* implementation defined */  // desde C99
```

  
Determina se o número de ponto flutuante x é menor ou maior que o número de ponto flutuante y, sem definir exceções de ponto flutuante.

### Parâmetros

x  |  \-  |  valor de ponto flutuante   
y  |  \-  |  valor de ponto flutuante   
  
### Valor de retorno

Valor inteiro diferente de zero se x < y || x > y, ​0​ caso contrário.

### Observações

Os operadores embutidos < e > para números de ponto flutuante podem levantar [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) se um ou ambos os argumentos forem NaN. Esta função é uma versão "silenciosa" da expressão x < y || x > y. A macro não avalia x e y duas vezes.

### Exemplo

Execute este código
```c
    #include <math.h>
    #include <stdio.h>
     
    int main(void)
    {
        printf("islessgreater(2.0,1.0)      = %d\n", islessgreater(2.0, 1.0));
        printf("islessgreater(1.0,2.0)      = %d\n", islessgreater(1.0, 2.0));
        printf("islessgreater(1.0,1.0)      = %d\n", islessgreater(1.0, 1.0));
        printf("islessgreater(INFINITY,1.0) = %d\n", islessgreater(INFINITY, 1.0));
        printf("islessgreater(1.0,NAN)      = %d\n", islessgreater(1.0, NAN));
     
        return 0;
    }
```

Saída possível:
```
    islessgreater(2.0,1.0)      = 1
    islessgreater(1.0,2.0)      = 1
    islessgreater(1.0,1.0)      = 0
    islessgreater(INFINITY,1.0) = 1
    islessgreater(1.0,NAN)      = 0
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.12.14.5 A macro islessgreater (p: TBD) 

    

  * F.10.11 Macros de comparação (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.12.14.5 A macro islessgreater (p: TBD) 

    

  * F.10.11 Macros de comparação (p: TBD) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.12.14.5 A macro islessgreater (p: 261) 

    

  * F.10.11 Macros de comparação (p: 531) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.12.14.5 A macro islessgreater (p: 241-242) 

### Veja também

[ isless](<#/doc/numeric/math/isless>)(C99) | verifica se o primeiro argumento de ponto flutuante é menor que o segundo   
(macro de função)  
[ isgreater](<#/doc/numeric/math/isgreater>)(C99) | verifica se o primeiro argumento de ponto flutuante é maior que o segundo   
(macro de função)  
[Documentação C++](<#/>) para islessgreater