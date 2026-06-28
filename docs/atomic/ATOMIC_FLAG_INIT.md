# ATOMIC_FLAG_INIT

Definido no cabeçalho [`<stdatomic.h>`](<#/doc/thread>)

```c
#define ATOMIC_FLAG_INIT /* unspecified */  // desde C11
```

  
Expande para um inicializador que pode ser usado para inicializar o tipo [atomic_flag](<#/doc/atomic/atomic_flag>) para o estado limpo (clear). O valor de um `atomic_flag` que não é inicializado usando esta macro é indeterminado. 

### Exemplo
```
    #include <stdatomic.h>
     
    atomic_flag flag = ATOMIC_FLAG_INIT;
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.17.1/3 ATOMIC_FLAG_INIT (p: 200) 

    

  * 7.17.8/4 ATOMIC_FLAG_INIT (p: 208) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.17.1/3 ATOMIC_FLAG_INIT (p: 273) 

    

  * 7.17.8/4 ATOMIC_FLAG_INIT (p: 285) 

### Veja também

[ ATOMIC_VAR_INIT](<#/doc/atomic/ATOMIC_VAR_INIT>)(C11)(obsoleto em C17)(removido em C23) | inicializa um novo objeto atômico   
(macro de função)  
[ atomic_flag](<#/doc/atomic/atomic_flag>)(C11) | flag booleana atômica sem bloqueio   
(struct)  
[Documentação C++](<#/>) para ATOMIC_FLAG_INIT