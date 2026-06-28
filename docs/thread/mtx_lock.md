# mtx_lock

Definido no cabeçalho [`<threads.h>`](<#/doc/thread>)

```c
int mtx_lock( mtx_t* mutex );  // desde C11
```

Bloqueia a thread atual até que o mutex apontado por `mutex` seja travado.

O comportamento é indefinido se a thread atual já travou o mutex e o mutex não é recursivo.

Chamadas anteriores a [mtx_unlock](<#/doc/thread/mtx_unlock>) no mesmo mutex _sincronizam-com_ esta operação, e todas as operações de travamento/destravamento em qualquer mutex dado formam uma única ordem total (similar à ordem de modificação de um atômico)

### Parâmetros

- **mutex** — ponteiro para o mutex a ser travado

### Valor de retorno

[thrd_success](<#/doc/thread/thrd_errors>) se bem-sucedido, [thrd_error](<#/doc/thread/thrd_errors>) caso contrário.

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.26.4.3 A função mtx_lock (p: 278)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.26.4.3 A função mtx_lock (p: 381)

### Veja também

[ mtx_timedlock](<#/doc/thread/mtx_timedlock>)(C11) | bloqueia até travar um mutex ou expirar o tempo
(função)
[ mtx_trylock](<#/doc/thread/mtx_trylock>)(C11) | trava um mutex ou retorna sem bloquear se já estiver travado
(função)
[ mtx_unlock](<#/doc/thread/mtx_unlock>)(C11) | destrava um mutex
(função)
[Documentação C++](<#/>) para mutex::lock
[Documentação C++](<#/>) para timed_mutex::lock
[Documentação C++](<#/>) para recursive_mutex::lock
[Documentação C++](<#/>) para recursive_timed_mutex::lock