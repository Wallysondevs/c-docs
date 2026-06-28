# mtx_trylock

Definido no cabeçalho [`<threads.h>`](<#/doc/thread>)

```c
int mtx_trylock( mtx_t *mutex );  // desde C11
```

Tenta bloquear o mutex apontado por `mutex` sem bloquear. Retorna imediatamente se o mutex já estiver bloqueado.

Chamadas anteriores a [mtx_unlock](<#/doc/thread/mtx_unlock>) no mesmo mutex _sincronizam-com_ esta operação (se esta operação for bem-sucedida), e todas as operações de bloqueio/desbloqueio em qualquer mutex formam uma única ordem total (semelhante à ordem de modificação de um atômico)

### Parâmetros

- **mutex** — ponteiro para o mutex a ser bloqueado

### Valor de retorno

[thrd_success](<#/doc/thread/thrd_errors>) se bem-sucedido, [thrd_busy](<#/doc/thread/thrd_errors>) se o mutex já estiver bloqueado ou devido a uma falha espúria ao adquirir um mutex disponível, [thrd_error](<#/doc/thread/thrd_errors>) se ocorrer um erro.

### Relatórios de Defeito

Os seguintes relatórios de defeito que alteram o comportamento foram aplicados retroativamente a padrões C publicados anteriormente.

DR | Aplicado a | Comportamento conforme publicado | Comportamento correto
[DR 470](<https://www.open-std.org/jtc1/sc22/wg14/www/docs/n2396.htm#dr_470>) | C11 | Não era permitido que `mtx_trylock` falhasse espuriamente | permitido

### Referências

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.26.4.5 A função mtx_trylock (p: 278-279)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.26.4.5 A função mtx_trylock (p: 382)

### Veja também

[ mtx_lock](<#/doc/thread/mtx_lock>)(C11) | bloqueia até bloquear um mutex
(função)
[ mtx_timedlock](<#/doc/thread/mtx_timedlock>)(C11) | bloqueia até bloquear um mutex ou expirar o tempo
(função)
[ mtx_unlock](<#/doc/thread/mtx_unlock>)(C11) | desbloqueia um mutex
(função)
[Documentação C++](<#/>) para mutex::try_lock
[Documentação C++](<#/>) para timed_mutex::try_lock
[Documentação C++](<#/>) para recursive_mutex::try_lock
[Documentação C++](<#/>) para recursive_timed_mutex::try_lock