# cnd_timedwait

Definido no cabeçalho [`<threads.h>`](<#/doc/thread>)

```c
int cnd_timedwait( cnd_t* restrict cond, mtx_t* restrict mutex, const struct timespec* restrict time_point );  // desde C11
```

Desbloqueia atomicamente o mutex apontado por `mutex` e bloqueia na variável de condição apontada por `cond` até que a thread seja sinalizada por [cnd_signal](<#/doc/thread/cnd_signal>) ou [cnd_broadcast](<#/doc/thread/cnd_broadcast>), ou até que o ponto no tempo baseado em TIME_UTC apontado por `time_point` tenha sido atingido, ou até que ocorra um despertar espúrio. O mutex é bloqueado novamente antes que a função retorne.

O comportamento é indefinido se o mutex não estiver previamente bloqueado pela thread chamadora.

### Parâmetros

- **cond** — ponteiro para a variável de condição na qual bloquear
- **mutex** — ponteiro para o mutex a ser desbloqueado durante a duração do bloqueio
- **time_point** — ponteiro para um objeto que especifica o tempo limite para esperar

### Valor de retorno

[thrd_success](<#/doc/thread/thrd_errors>) se bem-sucedido, thrd_timedout se o tempo limite tiver sido atingido antes que o mutex seja bloqueado, ou [thrd_error](<#/doc/thread/thrd_errors>) se um erro ocorreu.

### Referências

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.26.3.5 A função cnd_timedwait (p: 276-277)
*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.26.3.5 A função cnd_timedwait (p: 379-380)

### Veja também

[ cnd_wait](<#/doc/thread/cnd_wait>)(C11) | bloqueia em uma variável de condição
(função)
[Documentação C++](<#/>) para condition_variable::wait_until
[Documentação C++](<#/>) para condition_variable_any::wait_until