# thread_local

Definido no cabeçalho [`<threads.h>`](<#/doc/thread>)

```c
#define thread_local _Thread_local  // desde C11
(removido em C23)
```

  
Macro de conveniência que pode ser usada para especificar que um objeto possui [duração de armazenamento thread-local](<#/doc/language/storage_duration>). 

### Notas

Desde C23, `thread_local` é em si uma palavra-chave, que também pode ser uma macro predefinida, então `<threads.h>` não a fornece mais. 

### Referências

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.26.1/3 thread_local (p: 274) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.26.1/3 thread_local (p: 376) 

### Veja também

[documentação C++](<#/>) para thread_local  
---