# free

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
void free( void *ptr );
```

Desaloca o espaço previamente alocado por [malloc()](<#/doc/memory/malloc>), [calloc()](<#/doc/memory/calloc>), aligned_alloc(),(desde C11) ou [realloc()](<#/doc/memory/realloc>).

Se `ptr` for um ponteiro nulo, a função não faz nada.

O comportamento é indefinido se o valor de `ptr` não for igual a um valor retornado anteriormente por [malloc()](<#/doc/memory/malloc>), [calloc()](<#/doc/memory/calloc>), [realloc()](<#/doc/memory/realloc>), ou aligned_alloc()(desde C11).

O comportamento é indefinido se a área de memória referenciada por `ptr` já tiver sido desalocada, ou seja, se `free()`, free_sized(), free_aligned_sized()(desde C23), ou [realloc()](<#/doc/memory/realloc>) já tiver sido chamada com `ptr` como argumento e nenhuma chamada para [malloc()](<#/doc/memory/malloc>), [calloc()](<#/doc/memory/calloc>), [realloc()](<#/doc/memory/realloc>), ou aligned_alloc()(desde C11) resultou em um ponteiro igual a `ptr` posteriormente.

O comportamento é indefinido se, após `free()` retornar, um acesso for feito através do ponteiro `ptr` (a menos que outra função de alocação tenha resultado em um valor de ponteiro igual a `ptr`).

`free` é thread-safe: ela se comporta como se acessasse apenas os locais de memória visíveis através de seu argumento, e não qualquer armazenamento estático. Uma chamada a `free` que desaloca uma região de memória _sincroniza-se com_ uma chamada a qualquer função de alocação subsequente que aloque a mesma ou parte da mesma região de memória. Essa sincronização ocorre após qualquer acesso à memória pela função de desalocação e antes de qualquer acesso à memória pela função de alocação. Existe uma única ordem total de todas as funções de alocação e desalocação operando em cada região de memória particular. | (desde C11)

### Parâmetros

- **ptr** — ponteiro para a memória a ser desalocada

### Valor de retorno

(nenhum)

### Observações

A função aceita (e não faz nada com) o ponteiro nulo para reduzir a quantidade de casos especiais. Independentemente de a alocação ser bem-sucedida ou não, o ponteiro retornado por uma função de alocação pode ser passado para `free()`.

### Exemplo

Execute este código
```c
    #include <stdlib.h>
    
    int main(void)
    {
        int *p1 = malloc(10*sizeof *p1);
        free(p1); // todo ponteiro alocado deve ser liberado
    
        int *p2 = calloc(10, sizeof *p2);
        int *p3 = realloc(p2, 1000*sizeof *p3);
        if(p3) // p3 não nulo significa que p2 foi liberado por realloc
           free(p3);
        else // p3 nulo significa que p2 não foi liberado
           free(p2);
    }
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 
    
      * 7.24.3.3 A função free (p: 365) 

  * Padrão C17 (ISO/IEC 9899:2018): 
    
      * 7.22.3.3 A função free (p: 254) 

  * Padrão C11 (ISO/IEC 9899:2011): 
    
      * 7.22.3.3 A função free (p: 348) 

  * Padrão C99 (ISO/IEC 9899:1999): 
    
      * 7.20.3.2 A função free (p: 313) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 
    
      * 4.10.3.2 A função free 

### Veja também

[ malloc](<#/doc/memory/malloc>) | aloca memória
(função)
[ free_sized](<#/doc/memory/free_sized>)(C23) | desaloca memória de tamanho especificado previamente alocada
(função)
[ free_aligned_sized](<#/doc/memory/free_aligned_sized>)(C23) | desaloca memória de tamanho e alinhamento especificados previamente alocada
(função)
[Documentação C++](<#/>) para free