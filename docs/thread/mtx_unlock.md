# mtx_unlock

Definido no cabeçalho [`<threads.h>`](<#/doc/thread>)

```c
int mtx_unlock( mtx_t *mutex );  // desde C11
```

Desbloqueia o mutex apontado por `mutex`.

O comportamento é indefinido se o mutex não estiver bloqueado pela thread chamadora.

Esta função _sincroniza-com_ chamadas subsequentes a [mtx_lock](<#/doc/thread/mtx_lock>), [mtx_trylock](<#/doc/thread/mtx_trylock>), ou [mtx_timedlock](<#/doc/thread/mtx_timedlock>) no mesmo mutex. Todas as operações de bloqueio/desbloqueio em qualquer mutex dado formam uma única ordem total (semelhante à ordem de modificação de um atômico).

### Parâmetros

- **mutex** — ponteiro para o mutex a ser desbloqueado

### Valor de retorno

[thrd_success](<#/doc/thread/thrd_errors>) se bem-sucedido, [thrd_error](<#/doc/thread/thrd_errors>) caso contrário.

### Referências

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.26.4.6 A função mtx_unlock (p: 279)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.26.4.6 A função mtx_unlock (p: 382)

### Veja também

[ mtx_lock](<#/doc/thread/mtx_lock>)(C11) | bloqueia até que um mutex seja bloqueado
(função)
[ mtx_timedlock](<#/doc/thread/mtx_timedlock>)(C11) | bloqueia até que um mutex seja bloqueado ou o tempo expire
(função)
[ mtx_trylock](<#/doc/thread/mtx_trylock>)(C11) | bloqueia um mutex ou retorna sem bloquear se já estiver bloqueado
(função)
[Documentação C++](<#/>) para mutex::unlock
[Documentação C++](<#/>) para timed_mutex::unlock
[Documentação C++](<#/>) para recursive_mutex::unlock
[Documentação C++](<#/>) para recursive_timed_mutex::unlock