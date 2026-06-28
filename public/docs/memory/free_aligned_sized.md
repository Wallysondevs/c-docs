# free_aligned_sized

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
void free_aligned_sized( void* ptr, size_t alignment, size_t size );  // desde C23
```

Se ptr for um ponteiro nulo ou o resultado obtido de uma chamada para aligned_alloc, onde alignment é igual ao alinhamento de alocação solicitado e size é igual ao tamanho de alocação solicitado, esta função é equivalente a [free](<#/doc/memory/free>)(ptr). Caso contrário, o comportamento é indefinido.

O resultado de uma chamada [malloc](<#/doc/memory/malloc>), [calloc](<#/doc/memory/calloc>) ou [realloc](<#/doc/memory/realloc>) não deve ser passado para `free_aligned_sized`.

`free_aligned_sized` é thread-safe: ela se comporta como se acessasse apenas os locais de memória visíveis através de seu argumento, e não qualquer armazenamento estático.

Uma chamada para `free_aligned_sized` que desaloca uma região de memória _sincroniza-com_ uma chamada para qualquer função de alocação subsequente que aloque a mesma ou parte da mesma região de memória. Esta sincronização ocorre após qualquer acesso à memória pela função de desalocação e antes de qualquer acesso à memória pela função de alocação. Existe uma única ordem total de todas as funções de alocação e desalocação operando em cada região de memória particular.

### Parâmetros

- **ptr** — ponteiro para a memória a ser desalocada
- **alignment** — alinhamento da memória a ser desalocada
- **size** — tamanho da memória a ser desalocada

### Valor de retorno

(nenhum)

### Exemplo

| Esta seção está incompleta
Razão: nenhum exemplo

### Referências

* Padrão C23 (ISO/IEC 9899:2024):

* 7.24.3.5 A função free_sized (p: 366)

### Veja também

[ aligned_alloc](<#/doc/memory/aligned_alloc>)(C11) | aloca memória alinhada
(função)
[ free](<#/doc/memory/free>) | desaloca memória previamente alocada
(função)
[ free_sized](<#/doc/memory/free_sized>)(C23) | desaloca memória previamente alocada com tamanho
(função)
[ malloc](<#/doc/memory/malloc>) | aloca memória
(função)