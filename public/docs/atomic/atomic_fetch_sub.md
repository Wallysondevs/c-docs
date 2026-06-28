# atomic_fetch_sub, atomic_fetch_sub_explicit

Definido no cabeçalho [`<stdatomic.h>`](<#/doc/thread>)

```c
C atomic_fetch_sub( volatile A* obj, M arg );  // desde C11
C atomic_fetch_sub_explicit( volatile A* obj, M arg, memory_order order );  // desde C11
```

Substitui atomicamente o valor apontado por `obj` pelo resultado da subtração de `arg` do valor antigo de `obj`, e retorna o valor que `obj` continha anteriormente. A operação é uma operação de leitura-modificação-escrita. A primeira versão ordena os acessos à memória de acordo com [memory_order_seq_cst](<#/doc/atomic/memory_order>), a segunda versão ordena os acessos à memória de acordo com `order`.

Esta é uma [função genérica](<#/doc/language/generic>) definida para todos os [tipos de objeto atômico](<#/doc/language/atomic>) `A`. O argumento é um ponteiro para um tipo atômico volátil para aceitar endereços de objetos atômicos tanto não-voláteis quanto [voláteis](<#/doc/language/volatile>) (ex: I/O mapeado em memória), e a semântica volátil é preservada ao aplicar esta operação a objetos atômicos voláteis. `M` é o tipo não-atômico correspondente a `A` se `A` for um tipo inteiro atômico, ou [ptrdiff_t](<#/doc/types/ptrdiff_t>) se `A` for um tipo ponteiro atômico.

Não é especificado se o nome de uma função genérica é uma macro ou um identificador declarado com ligação externa. Se uma definição de macro for suprimida para acessar uma função real (ex: entre parênteses como (atomic_fetch_sub)(...)), ou um programa definir um identificador externo com o nome de uma função genérica, o comportamento é indefinido.

Para tipos inteiros com sinal, a aritmética é definida para usar a representação de complemento de dois. Não há resultados indefinidos. Para tipos ponteiro, o resultado pode ser um endereço indefinido, mas as operações, de outra forma, não têm comportamento indefinido.

### Parâmetros

- **obj** — ponteiro para o objeto atômico a ser modificado
- **arg** — o valor a ser subtraído do valor armazenado no objeto atômico
- **order** — a ordem de sincronização de memória para esta operação: todos os valores são permitidos

### Valor de retorno

O valor contido anteriormente pelo objeto atômico apontado por `obj`.

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.17.7.5 As funções genéricas atomic_fetch e modify (p: 208)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.17.7.5 As funções genéricas atomic_fetch e modify (p: 284-285)

### Veja também

[ atomic_fetch_addatomic_fetch_add_explicit](<#/doc/atomic/atomic_fetch_add>)(C11) | adição atômica
(função)
[Documentação C++](<#/>) para atomic_fetch_sub, atomic_fetch_sub_explicit