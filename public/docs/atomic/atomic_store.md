# atomic_store, atomic_store_explicit

Definido no cabeçalho [`<stdatomic.h>`](<#/>)

```c
void atomic_store( volatile A* obj , C desired );  // desde C11
void atomic_store_explicit( volatile A* obj, C desired, memory_order order );  // desde C11
```

Substitui atomicamente o valor da variável atômica apontada por `obj` com `desired`. A operação é uma operação de escrita atômica.

A primeira versão ordena os acessos à memória de acordo com [memory_order_seq_cst](<#/doc/atomic/memory_order>), a segunda versão ordena os acessos à memória de acordo com `order`. `order` deve ser um de [memory_order_relaxed](<#/doc/atomic/memory_order>), [memory_order_release](<#/doc/atomic/memory_order>) ou [memory_order_seq_cst](<#/doc/atomic/memory_order>). Caso contrário, o comportamento é indefinido.

Esta é uma [função genérica](<#/doc/language/generic>) definida para todos os [tipos de objeto atômico](<#/doc/language/atomic>) `A`. O argumento é um ponteiro para um tipo atômico volátil para aceitar endereços de objetos atômicos tanto não-voláteis quanto [voláteis](<#/doc/language/volatile>) (por exemplo, I/O mapeado em memória), e a semântica volátil é preservada ao aplicar esta operação a objetos atômicos voláteis. `C` é o tipo não-atômico correspondente a `A`.

Não é especificado se o nome de uma função genérica é uma macro ou um identificador declarado com ligação externa. Se uma definição de macro for suprimida para acessar uma função real (por exemplo, entre parênteses como (atomic_store)(...)), ou um programa definir um identificador externo com o nome de uma função genérica, o comportamento é indefinido.

### Parâmetros

- **obj** — ponteiro para o objeto atômico a ser modificado
- **order** — a ordenação de sincronização de memória para esta operação

### Valor de retorno

(nenhum)

### Referências

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.17.7.1 As funções genéricas atomic_store (p: 206)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.17.7.1 As funções genéricas atomic_store (p: 282)

### Veja também

[ atomic_loadatomic_load_explicit](<#/doc/atomic/atomic_load>)(C11) | lê um valor de um objeto atômico
(função)
[Documentação C++](<#/>) para atomic_store, atomic_store_explicit