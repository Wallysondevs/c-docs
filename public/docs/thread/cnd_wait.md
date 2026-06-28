# cnd_wait

Definido no cabeçalho [`<threads.h>`](<#/doc/thread>)

```c
int cnd_wait( cnd_t* cond, mtx_t* mutex );  // desde C11
```

Desbloqueia atomicamente o mutex apontado por `mutex` e bloqueia na variável de condição apontada por `cond` até que a thread seja sinalizada por [cnd_signal](<#/doc/thread/cnd_signal>) ou [cnd_broadcast](<#/doc/thread/cnd_broadcast>), ou até que ocorra um despertar espúrio. O mutex é bloqueado novamente antes que a função retorne.

O comportamento é indefinido se o mutex não estiver previamente bloqueado pela thread chamadora.

### Parâmetros

- **cond** — ponteiro para a variável de condição na qual bloquear
- **mutex** — ponteiro para o mutex a ser desbloqueado durante a duração do bloqueio

### Valor de retorno

[thrd_success](<#/doc/thread/thrd_errors>) se bem-sucedido, [thrd_error](<#/doc/thread/thrd_errors>) caso contrário.

### Referências

* Padrão C17 (ISO/IEC 9899:2018):

  * 7.26.3.6 A função cnd_wait (p: 277)

* Padrão C11 (ISO/IEC 9899:2011):

  * 7.26.3.6 A função cnd_wait (p: 380)

### Veja também

[ cnd_timedwait](<#/doc/thread/cnd_timedwait>)(C11) | bloqueia em uma variável de condição, com um tempo limite
(função)
[Documentação C++](<#/>) para condition_variable::wait
[Documentação C++](<#/>) para condition_variable_any::wait