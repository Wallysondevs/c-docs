# atomic_flag_clear, atomic_flag_clear_explicit

Definido no cabeçalho [`<stdatomic.h>`](<#/doc/thread>)

```c
void atomic_flag_clear( volatile atomic_flag* obj );  // desde C11
void atomic_flag_clear_explicit( volatile atomic_flag* obj, memory_order order );  // desde C11
```

  
Altera atomicamente o estado de um `atomic_flag` apontado por `obj` para limpo (false). A primeira versão ordena os acessos à memória de acordo com [memory_order_seq_cst](<#/doc/atomic/memory_order>), a segunda versão ordena os acessos à memória de acordo com `order`.

O argumento é um ponteiro para uma atomic flag volátil para aceitar endereços de atomic flags tanto não-voláteis quanto [voláteis](<#/doc/language/volatile>) (por exemplo, I/O mapeado em memória).

### Parâmetros

obj  |  \-  |  ponteiro para o objeto atomic flag a ser modificado   
order  |  \-  |  a ordenação de sincronização de memória para esta operação: todos os valores são permitidos   
  
### Valor de retorno

(nenhum) 

### Referências

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.17.8.2 As funções atomic_flag_clear (p: 209) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.17.8.2 As funções atomic_flag_clear (p: 286) 

### Veja também

[ atomic_flag_test_and_setatomic_flag_test_and_set_explicit](<#/doc/atomic/atomic_flag_test_and_set>)(C11) |  define uma atomic_flag como true e retorna o valor antigo   
(função)  
[Documentação C++](<#/>) para atomic_flag_clear, atomic_flag_clear_explicit