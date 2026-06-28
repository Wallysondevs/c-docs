# atomic_flag_test_and_set, atomic_flag_test_and_set_explicit

Definido no cabeçalho [`<stdatomic.h>`](<#/doc/thread>)

```c
_Bool atomic_flag_test_and_set( volatile atomic_flag* obj );  // desde C11
_Bool atomic_flag_test_and_set_explicit( volatile atomic_flag* obj, memory_order order );  // desde C11
```

Altera atomicamente o estado de um `atomic_flag` apontado por `obj` para definido (true) e retorna o valor anterior. A primeira versão ordena os acessos à memória de acordo com [memory_order_seq_cst](<#/doc/atomic/memory_order>), a segunda versão ordena os acessos à memória de acordo com `order`.

O argumento é um ponteiro para um atomic flag volátil para aceitar endereços de atomic flags tanto não-voláteis quanto [voláteis](<#/doc/language/volatile>) (por exemplo, I/O mapeada em memória).

### Parâmetros

- **obj** — ponteiro para o objeto atomic flag a ser modificado
- **order** — a ordenação de sincronização de memória para esta operação: todos os valores são permitidos

### Valor de retorno

O valor anterior mantido pelo atomic flag apontado por `obj`.

### Referências

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.17.8.1 As funções atomic_flag_test_and_set (p: 209)
*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.17.8.1 As funções atomic_flag_test_and_set (p: 285-286)

### Veja também

[ atomic_flag_clearatomic_flag_clear_explicit](<#/doc/atomic/atomic_flag_clear>)(C11) | define um atomic_flag como false
(função)
[Documentação C++](<#/>) para atomic_flag_test_and_set, atomic_flag_test_and_set_explicit