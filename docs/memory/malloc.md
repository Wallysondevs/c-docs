# malloc

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
void *malloc( size_t size );
```

Aloca `size` bytes de armazenamento não inicializado.

Se a alocação for bem-sucedida, retorna um ponteiro que está adequadamente alinhado para qualquer tipo de objeto com [alinhamento fundamental](<#/doc/language/object>).

Se `size` for zero, o comportamento de `malloc` é definido pela implementação. Por exemplo, um ponteiro nulo pode ser retornado. Alternativamente, um ponteiro não nulo pode ser retornado; mas tal ponteiro não deve ser [desreferenciado](<#/doc/language/operator_member_access>), e deve ser passado para [free](<#/doc/memory/free>) para evitar vazamentos de memória.

`malloc` é thread-safe: ele se comporta como se acessasse apenas os locais de memória visíveis através de seu argumento, e não qualquer armazenamento estático. Uma chamada anterior a [free](<#/doc/memory/free>), free_sized, e free_aligned_sized(desde C23) ou [realloc](<#/doc/memory/realloc>) que desaloca uma região de memória _sincroniza-se com_ uma chamada a `malloc` que aloca a mesma ou parte da mesma região de memória. Esta sincronização ocorre após qualquer acesso à memória pela função de desalocação e antes de qualquer acesso à memória por `malloc`. Existe uma única ordem total de todas as funções de alocação e desalocação operando em cada região de memória particular. | (desde C11)

### Parâmetros

- **size** — número de bytes a alocar

### Valor de retorno

Em caso de sucesso, retorna o ponteiro para o início da memória recém-alocada. Para evitar um vazamento de memória, o ponteiro retornado deve ser desalocado com [free()](<#/doc/memory/free>) ou [realloc()](<#/doc/memory/realloc>).

Em caso de falha, retorna um ponteiro nulo.

### Exemplo

Execute este código
```
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(void)
    {
        int *p1 = malloc(4*sizeof(int));  // allocates enough for an array of 4 int
        int *p2 = malloc(sizeof(int[4])); // same, naming the type directly
        int *p3 = malloc(4*sizeof *p3);   // same, without repeating the type name
    
        if(p1) {
            for(int n=0; n<4; ++n) // populate the array
                p1[n] = n*n;
            for(int n=0; n<4; ++n) // print it back out
                printf("p1[%d] == %d\n", n, p1[n]);
        }
    
        free(p1);
        free(p2);
        free(p3);
    }
```

Saída:
```
    p1[0] == 0
    p1[1] == 1
    p1[2] == 4
    p1[3] == 9
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.22.3.4 A função malloc (p: 254)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.22.3.4 A função malloc (p: 349)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.20.3.3 A função malloc (p: 314)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.10.3.3 A função malloc

### Veja também

[ free](<#/doc/memory/free>) | desaloca memória previamente alocada
(função)
[Documentação C++](<#/>) para malloc