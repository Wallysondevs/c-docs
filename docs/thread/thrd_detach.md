# thrd_detach

Definido no cabeçalho [`<threads.h>`](<#/doc/thread>)

```c
int thrd_detach( thrd_t thr );  // desde C11
```

  
Desvincula a thread identificada por `thr` do ambiente atual. Os recursos mantidos pela thread serão liberados automaticamente assim que a thread finalizar. 

### Parâmetros

thr  |  \-  |  identificador da thread a ser desvinculada   
  
### Valor de retorno

[thrd_success](<#/doc/thread/thrd_errors>) se bem-sucedido, [thrd_error](<#/doc/thread/thrd_errors>) caso contrário. 

### Referências

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.26.5.3 A função thrd_detach (p: 280) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.26.5.3 A função thrd_detach (p: 383-384) 

### Veja também

[ thrd_join](<#/doc/thread/thrd_join>)(C11) |  bloqueia até que uma thread termine   
(função)  
[Documentação C++](<#/>) para detach