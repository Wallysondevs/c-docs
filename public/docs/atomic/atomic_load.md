# atomic_load, atomic_load_explicit

Definido no cabeçalho [`<stdatomic.h>`](<#/doc/thread>)

```c
C atomic_load( const volatile A* obj );  // desde C11
C atomic_load_explicit( const volatile A* obj, memory_order order );  // desde C11
```

  
Carrega atomicamente e retorna o valor atual da variável atômica apontada por `obj`. A operação é uma operação de leitura atômica.

A primeira versão ordena os acessos à memória de acordo com [memory_order_seq_cst](<#/doc/atomic/memory_order>), a segunda versão ordena os acessos à memória de acordo com `order`. `order` deve ser um de [memory_order_relaxed](<#/doc/atomic/memory_order>), [memory_order_consume](<#/doc/atomic/memory_order>), [memory_order_acquire](<#/doc/atomic/memory_order>) ou [memory_order_seq_cst](<#/doc/atomic/memory_order>). Caso contrário, o comportamento é indefinido.

Esta é uma [função genérica](<#/doc/language/generic>) definida para todos os [tipos de objeto atômico](<#/doc/language/atomic>) `A`. O argumento é um ponteiro para um tipo atômico `volatile` para aceitar endereços de objetos atômicos tanto não-`volatile` quanto [volatile](<#/doc/language/volatile>) (por exemplo, I/O mapeada em memória), e a semântica `volatile` é preservada ao aplicar esta operação a objetos atômicos `volatile`. `C` é o tipo não-atômico correspondente a `A`.

Não é especificado se o nome de uma função genérica é uma macro ou um identificador declarado com ligação externa. Se uma definição de macro for suprimida para acessar uma função real (por exemplo, entre parênteses como (atomic_load)(...)), ou um programa definir um identificador externo com o nome de uma função genérica, o comportamento é indefinido.

### Parâmetros

obj  |  \-  |  ponteiro para o objeto atômico a ser acessado   
order  |  \-  |  a ordenação de sincronização de memória para esta operação   
  
### Valor de retorno

O valor atual da variável atômica apontada por `obj`.

### Referências

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.17.7.2 As funções genéricas atomic_load (p: 206) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.17.7.2 As funções genéricas atomic_load (p: 282) 

### Veja também

[ atomic_storeatomic_store_explicit](<#/doc/atomic/atomic_store>)(C11) |  armazena um valor em um objeto atômico   
(função)  
[Documentação C++](<#/>) para atomic_load, atomic_load_explicit