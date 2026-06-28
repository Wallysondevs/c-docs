# atomic_exchange, atomic_exchange_explicit

Definido no cabeçalho [`<stdatomic.h>`](<#/doc/thread>)

```c
C atomic_exchange( volatile A* obj, C desired );  // desde C11
C atomic_exchange_explicit( volatile A* obj, C desired, memory_order order );  // desde C11
```

  
Substitui atomicamente o valor apontado por `obj` por `desired` e retorna o valor que `obj` continha anteriormente. A operação é uma operação de leitura-modificação-escrita. A primeira versão ordena os acessos à memória de acordo com [memory_order_seq_cst](<#/doc/atomic/memory_order>), a segunda versão ordena os acessos à memória de acordo com `order`. 

Esta é uma [função genérica](<#/doc/language/generic>) definida para todos os [tipos de objeto atômico](<#/doc/language/atomic>) `A`. O argumento é um ponteiro para um tipo atômico volátil para aceitar endereços de objetos atômicos não-voláteis e [voláteis](<#/doc/language/volatile>) (por exemplo, I/O mapeado em memória), e a semântica volátil é preservada ao aplicar esta operação a objetos atômicos voláteis. `C` é o tipo não-atômico correspondente a `A`. 

Não é especificado se o nome de uma função genérica é uma macro ou um identificador declarado com ligação externa. Se uma definição de macro for suprimida para acessar uma função real (por exemplo, entre parênteses como (atomic_exchange)(...)), ou um programa definir um identificador externo com o nome de uma função genérica, o comportamento é indefinido. 

### Parâmetros

obj  |  \-  |  ponteiro para o objeto atômico a ser modificado   
desired  |  \-  |  o valor para substituir o objeto atômico   
order  |  \-  |  a ordem de sincronização de memória para esta operação: todos os valores são permitidos   
  
### Valor de retorno

O valor que o objeto atômico apontado por `obj` continha anteriormente. 

### Referências

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.17.7.3 As funções genéricas atomic_exchange (p: 207) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.17.7.3 As funções genéricas atomic_exchange (p: 283) 

### Veja também

[ atomic_compare_exchange_strongatomic_compare_exchange_strong_explicitatomic_compare_exchange_weakatomic_compare_exchange_weak_explicit](<#/doc/atomic/atomic_compare_exchange>)(C11) |  troca um valor com um objeto atômico se o valor antigo for o esperado, caso contrário lê o valor antigo   
(função)  
[Documentação C++](<#/>) para atomic_exchange, atomic_exchange_explicit