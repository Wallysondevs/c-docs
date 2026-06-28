# free_sized

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
void free_sized( void* ptr, size_t size );  // desde C23
```

Desaloca o espaço previamente alocado por [malloc()](<#/doc/memory/malloc>), [calloc()](<#/doc/memory/calloc>), ou [realloc()](<#/doc/memory/realloc>) (mas não por aligned_alloc()).

| Esta seção está incompleta
Razão: compartilhar a redação entre a família `free_*`

`free_sized` é thread-safe: ela se comporta como se acessasse apenas os locais de memória visíveis através de seu argumento, e não qualquer armazenamento estático.

Uma chamada a `free_sized` que desaloca uma região de memória _sincroniza-se com_ uma chamada a qualquer função de alocação subsequente que aloque a mesma ou parte da mesma região de memória. Essa sincronização ocorre após qualquer acesso à memória pela função de desalocação e antes de qualquer acesso à memória pela função de alocação. Existe uma única ordem total de todas as funções de alocação e desalocação operando em cada região particular de memória.

### Parâmetros

- **ptr** — ponteiro para a memória a ser desalocada
- **size** — tamanho da memória previamente passada para uma função de alocação

### Valor de retorno

(nenhum)

### Notas

| Esta seção está incompleta

### Implementação possível
```c
    void free_sized(void* ptr, size_t /*size*/)
    {
        free(ptr);
    }
```

### Exemplo

Execute este código
```c
    #include <stddef.h>
    #include <stdio.h>
    #include <stdlib.h>
     
    typedef struct
    {
        size_t size;     // current number of elements
        size_t capacity; // reserved number of elements
        void** data;
    } PtrVector;
     
    PtrVector vector_create(size_t initial_capacity)
    {
        PtrVector ret =
        {
            .capacity = initial_capacity,
            .data = (void**) malloc(initial_capacity * sizeof(void*))
        };
        return ret;
    }
     
    void vector_delete(PtrVector* self)
    {
        free_sized(self->data, self->capacity * sizeof(void*));
    }
     
    void vector_push_back(PtrVector* self, void* value)
    {
        if (self->size == self->capacity)
        {
            self->capacity *= 2;
            self->data = (void**) realloc(self->data, self->capacity * sizeof(void*));
        }
        self->data[self->size++] = value;
    }
     
    int main()
    {
        int data = 42;
        float pi = 3.141592f;
        PtrVector v = vector_create(8);
        vector_push_back(&v, &data);
        vector_push_back(&v, &pi);
        printf("data[0] = %i\n", *(int*)v.data[0]);
        printf("data[1] = %f\n", *(float*)v.data[1]);
        vector_delete(&v);
    }
```

Saída:
```
    data[0] = 42
    data[1] = 3.141592
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.24.3.4 A função free_sized (p: 365-366)

### Veja também

[ free](<#/doc/memory/free>) | desaloca memória previamente alocada
(função)
[ free_aligned_sized](<#/doc/memory/free_aligned_sized>)(C23) | desaloca memória alocada previamente com tamanho e alinhamento específicos
(função)
[ malloc](<#/doc/memory/malloc>) | aloca memória
(função)