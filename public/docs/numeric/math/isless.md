# isless

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
#define isless(x, y) /* implementation defined */  // desde C99
```

  
Determina se o número de ponto flutuante x é menor que o número de ponto flutuante y, sem definir exceções de ponto flutuante.

### Parâmetros

x  |  \-  |  valor de ponto flutuante   
y  |  \-  |  valor de ponto flutuante   
  
### Valor de retorno

Valor inteiro diferente de zero se x < y, ​0​ caso contrário.

### Observações

O operador< embutido para números de ponto flutuante pode levantar [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) se um ou ambos os argumentos forem NaN. Esta função é uma versão "silenciosa" do operador<.

### Exemplo

Execute este código
```c
    #include <math.h>
    #include <stdio.h>
    
    int main(void)
    {
        printf("isless(2.0,1.0)      = %d\n", isless(2.0, 1.0));
        printf("isless(1.0,2.0)      = %d\n", isless(1.0, 2.0));
        printf("isless(INFINITY,1.0) = %d\n", isless(INFINITY, 1.0));
        printf("isless(1.0,NAN)      = %d\n", isless(1.0, NAN));
    
        return 0;
    }
```

Saída possível: 
```
    isless(2.0,1.0)      = 0
    isless(1.0,2.0)      = 1
    isless(INFINITY,1.0) = 0
    isless(1.0,NAN)      = 0
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.12.14.3 A macro isless (p: TBD) 

    

  * F.10.11 Macros de comparação (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.12.14.3 A macro isless (p: TBD) 

    

  * F.10.11 Macros de comparação (p: TBD) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.12.14.3 A macro isless (p: 260) 

    

  * F.10.11 Macros de comparação (p: 531) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.12.14.3 A macro isless (p: 241) 

### Veja também

[ isgreater](<#/doc/numeric/math/isgreater>)(C99) | verifica se o primeiro argumento de ponto flutuante é maior que o segundo   
(macro de função)  
[documentação C++](<#/>) para isless