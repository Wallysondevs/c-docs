# atomic_thread_fence

Definido no cabeçalho [`<stdatomic.h>`](<#/doc/thread>)

```c
void atomic_thread_fence( memory_order order );  // desde C11
```

  
Estabelece a ordenação de sincronização de memória de acessos não atômicos e atômicos relaxados, conforme instruído por `order`, sem uma operação atômica associada. Por exemplo, todos os *stores* não atômicos e atômicos relaxados que ocorrem antes de uma *fence* [memory_order_release](<#/doc/atomic/memory_order>) na *thread* A serão sincronizados com os *loads* não atômicos e atômicos relaxados dos mesmos locais feitos na *thread* B após uma *fence* [memory_order_acquire](<#/doc/atomic/memory_order>).

### Parâmetros

order  |  \-  |  a ordenação de memória executada por esta *fence*   
  
### Valor de retorno

(nenhum) 

### Referências

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.17.4.1 A função atomic_thread_fence (p: 204) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.17.4.1 A função atomic_thread_fence (p: 278-279) 

### Ver também

[ atomic_signal_fence](<#/doc/atomic/atomic_signal_fence>)(C11) |  *fence* entre uma *thread* e um *signal handler* executado na mesma *thread*   
(função)  
[Documentação C++](<#/>) para atomic_thread_fence