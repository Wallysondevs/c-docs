# isgreaterequal

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
#define isgreaterequal(x, y) /* implementation defined */  // desde C99
```

  
Determina se o número de ponto flutuante x é maior ou igual ao número de ponto flutuante y, sem definir exceções de ponto flutuante.

### Parâmetros

x  |  \-  |  valor de ponto flutuante   
y  |  \-  |  valor de ponto flutuante   
  
### Valor de retorno

Valor inteiro diferente de zero se x >= y, ​0​ caso contrário.

### Observações

O operador embutido `>=` para números de ponto flutuante pode levantar [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) se um ou ambos os argumentos forem NaN. Esta função é uma versão "silenciosa" do operador `>=`.

### Exemplo

Execute este código
```c
    #include <math.h>
    #include <stdio.h>
     
    int main(void)
    {
        printf("isgreaterequal(2.0,1.0)      = %d\n", isgreaterequal(2.0, 1.0));
        printf("isgreaterequal(1.0,2.0)      = %d\n", isgreaterequal(1.0, 2.0));
        printf("isgreaterequal(1.0,1.0)      = %d\n", isgreaterequal(1.0, 1.0));
        printf("isgreaterequal(INFINITY,1.0) = %d\n", isgreaterequal(INFINITY, 1.0));
        printf("isgreaterequal(1.0,NAN)      = %d\n", isgreaterequal(1.0, NAN));
     
        return 0;
    }
```

Saída possível: 
```
    isgreaterequal(2.0,1.0)      = 1
    isgreaterequal(1.0,2.0)      = 0
    isgreaterequal(1.0,1.0)      = 1
    isgreaterequal(INFINITY,1.0) = 1
    isgreaterequal(1.0,NAN)      = 0
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.12.14.2 A macro isgreaterequal (p: TBD) 

    

  * F.10.11 Macros de comparação (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.12.14.2 A macro isgreaterequal (p: TBD) 

    

  * F.10.11 Macros de comparação (p: TBD) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.12.14.2 A macro isgreaterequal (p: 259-260) 

    

  * F.10.11 Macros de comparação (p: 531) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.12.14.2 A macro isgreaterequal (p: 240-241) 

### Veja também

[ islessequal](<#/doc/numeric/math/islessequal>)(C99) | verifica se o primeiro argumento de ponto flutuante é menor ou igual ao segundo   
(macro de função)  
[documentação C++](<#/>) para isgreaterequal