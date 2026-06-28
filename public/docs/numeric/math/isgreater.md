# isgreater

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
#define isgreater(x, y) /* implementation defined */  // desde C99
```

Determina se o número de ponto flutuante x é maior que o número de ponto flutuante (y), sem definir exceções de ponto flutuante.

### Parâmetros

- **x** — valor de ponto flutuante
- **y** — valor de ponto flutuante

### Valor de retorno

Valor inteiro não zero se x > y, ​0​ caso contrário.

### Observações

O operador> embutido para números de ponto flutuante pode definir [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) se um ou ambos os argumentos forem NaN. Esta função é uma versão "silenciosa" do operador>.

### Exemplo

Execute este código
```c
    #include <math.h>
    #include <stdio.h>
    
    int main(void)
    {
        printf("isgreater(2.0,1.0)      = %d\n", isgreater(2.0, 1.0));
        printf("isgreater(1.0,2.0)      = %d\n", isgreater(1.0, 2.0));
        printf("isgreater(INFINITY,1.0) = %d\n", isgreater(INFINITY, 1.0));
        printf("isgreater(1.0,NAN)      = %d\n", isgreater(1.0, NAN));
    
        return 0;
    }
```

Saída possível:
```
    isgreater(2.0,1.0)      = 1
    isgreater(1.0,2.0)      = 0
    isgreater(INFINITY,1.0) = 1
    isgreater(1.0,NAN)      = 0
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.12.14.1 A macro isgreater (p: TBD)

    

  * F.10.11 Macros de comparação (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.12.14.1 A macro isgreater (p: 189)

    

  * F.10.11 Macros de comparação (p: 386-387)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.12.14.1 A macro isgreater (p: 259)

    

  * F.10.11 Macros de comparação (p: 531)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.12.14.1 A macro isgreater (p: 240)

### Veja também

[ isless](<#/doc/numeric/math/isless>)(C99) | verifica se o primeiro argumento de ponto flutuante é menor que o segundo
(macro de função)
[Documentação C++](<#/>) para isgreater