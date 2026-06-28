# RAND_MAX

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
#define RAND_MAX /*definido pela implementação*/
```

  
Expande para uma expressão constante inteira igual ao valor máximo retornado pela função [rand()](<#/doc/numeric/random/rand>). Este valor é dependente da implementação. É garantido que este valor seja de pelo menos 32767. 

### Exemplo

Execute este código
```
    #include <limits.h>
    #include <stdio.h>
    #include <stdlib.h>
    #include <time.h>
     
    int main(void)
    {
        srand(time(NULL)); // use current time as seed for random generator
        printf("RAND_MAX: %i\n", RAND_MAX);
        printf("INT_MAX: %i\n", INT_MAX);
        printf("Random value on [0,1]: %f\n", (double)rand() / RAND_MAX);
    }
```

Saída possível: 
```
    RAND_MAX: 2147483647
    INT_MAX: 2147483647
    Random value on [0,1]: 0.362509
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.22/3 Utilitários gerais <stdlib.h> (p: 248) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.22/3 Utilitários gerais <stdlib.h> (p: 340) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.20/3 Utilitários gerais <stdlib.h> (p: 306) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.10 UTILITÁRIOS GERAIS <stdlib.h>

### Veja também

[ rand](<#/doc/numeric/random/rand>) |  gera um número pseudoaleatório   
(função)  
[ srand](<#/doc/numeric/random/srand>) |  inicializa o gerador de números pseudoaleatórios   
(função)  
[Documentação C++](<#/>) para RAND_MAX