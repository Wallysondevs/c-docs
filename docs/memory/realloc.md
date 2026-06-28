# realloc

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
void *realloc( void *ptr, size_t new_size );
```

  
Realoca a área de memória fornecida. Se ptr não for NULL, ele deve ter sido previamente alocado por [malloc](<#/doc/memory/malloc>), [calloc](<#/doc/memory/calloc>) ou `realloc` e ainda não liberado com uma chamada para [free](<#/doc/memory/free>) ou `realloc`. Caso contrário, os resultados são comportamento indefinido.

A realocação é feita por:

a) expandindo ou contraindo a área existente apontada por ptr, se possível. O conteúdo da área permanece inalterado até o menor dos tamanhos novo e antigo. Se a área for expandida, o conteúdo da nova parte do array é comportamento indefinido.

b) alocando um novo bloco de memória de tamanho new_size bytes, copiando a área de memória com tamanho igual ao menor dos tamanhos novo e antigo, e liberando o bloco antigo.

Se não houver memória suficiente, o bloco de memória antigo não é liberado e um ponteiro nulo é retornado.

Se ptr for [NULL](<#/doc/types/NULL>), o comportamento é o mesmo que chamar [malloc](<#/doc/memory/malloc>)(new_size).

Caso contrário,

se new_size for zero, o comportamento é definido pela implementação (um ponteiro nulo pode ser retornado (nesse caso, o bloco de memória antigo pode ou não ser liberado), ou algum ponteiro não nulo pode ser retornado que não pode ser usado para acessar o armazenamento). Tal uso é obsoleto (via [C DR 400](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2396.htm#dr_400>)).(desde C17) | (até C23)  
se new_size for zero, o comportamento é indefinido. | (desde C23)  
`realloc` é thread-safe: ele se comporta como se acessasse apenas os locais de memória visíveis através de seu argumento, e não qualquer armazenamento estático. Uma chamada anterior a [free](<#/doc/memory/free>) ou `realloc` que desaloca uma região de memória _sincroniza-se-com_ uma chamada a qualquer função de alocação, incluindo `realloc` que aloca a mesma ou parte da mesma região de memória. Essa sincronização ocorre após qualquer acesso à memória pela função de desalocação e antes de qualquer acesso à memória por `realloc`. Existe uma ordem total única de todas as funções de alocação e desalocação operando em cada região particular de memória. | (desde C11)  
  
### Parâmetros

- **ptr** — ponteiro para a área de memória a ser realocada
- **new_size** — novo tamanho do array em bytes
  
### Valor de retorno

Em caso de sucesso, retorna o ponteiro para o início da memória recém-alocada. Para evitar um vazamento de memória, o ponteiro retornado deve ser desalocado com [free](<#/doc/memory/free>) ou `realloc`. O ponteiro original ptr é invalidado e qualquer acesso a ele é comportamento indefinido (mesmo que a realocação tenha sido no local).

Em caso de falha, retorna um ponteiro nulo. O ponteiro original ptr permanece válido e pode precisar ser desalocado com [free](<#/doc/memory/free>) ou `realloc`.

### Notas

Originalmente (em C89), o suporte para tamanho zero foi adicionado para acomodar código como
```
    OBJ *p = calloc(0, sizeof(OBJ)); // "zero-length" placeholder
    /*...*/
    while (1)
    {
        p = realloc(p, c * sizeof(OBJ)); // reallocations until size settles
        /* code that may change c or break out of loop */
    }
```

### Exemplo

Execute este código
```
    #include <assert.h>
    #include <stdio.h>
    #include <stdlib.h>
    #include <string.h>
     
    void print_storage_info(const int* next, const int* prev, int ints)
    {
        if (next)
            printf("%s location: %p. Size: %d ints (%ld bytes).\n",
                   (next != prev ? "New" : "Old"), (void*)next, ints, ints * sizeof(int));
        else
            printf("Allocation failed.\n");
    }
     
    int main(void)
    {
        const int pattern[] = {1, 2, 3, 4, 5, 6, 7, 8};
        const int pattern_size = sizeof pattern / sizeof(int);
        int *next = NULL, *prev = NULL;
     
        if ((next = (int*)malloc(pattern_size * sizeof *next))) // allocates an array
        {
            memcpy(next, pattern, sizeof pattern); // fills the array
            print_storage_info(next, prev, pattern_size);
        }
        else
            return EXIT_FAILURE;
     
        // Reallocate in cycle using the following values as a new storage size.
        const int realloc_size[] = {10, 12, 512, 32768, 65536, 32768};
     
        for (int i = 0; i != sizeof realloc_size / sizeof(int); ++i)
        {
            if ((next = (int*)realloc(prev = next, realloc_size[i] * sizeof(int))))
            {
                print_storage_info(next, prev, realloc_size[i]);
                assert(!memcmp(next, pattern, sizeof pattern));  // is pattern held
            }
            else // if realloc failed, the original pointer needs to be freed
            {
                free(prev);
                return EXIT_FAILURE;
            }
        }
     
        free(next); // finally, frees the storage
        return EXIT_SUCCESS;
    }
```

Saída possível:
```
    New location: 0x144c010. Size: 8 ints (32 bytes).
    Old location: 0x144c010. Size: 10 ints (40 bytes).
    New location: 0x144c450. Size: 12 ints (48 bytes).
    Old location: 0x144c450. Size: 512 ints (2048 bytes).
    Old location: 0x144c450. Size: 32768 ints (131072 bytes).
    New location: 0x7f490c5bd010. Size: 65536 ints (262144 bytes).
    Old location: 0x7f490c5bd010. Size: 32768 ints (131072 bytes).
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.22.3.5 A função realloc (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.22.3.5 A função realloc (p: 254) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.22.3.5 A função realloc (p: 349) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.20.3.4 A função realloc (p: 314) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.10.3.4 A função realloc 

### Veja também

[Documentação C++](<#/>) para realloc  
---