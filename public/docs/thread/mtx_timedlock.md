# mtx_timedlock

Definido no cabeçalho [`<threads.h>`](<#/doc/thread>)

```c
int mtx_timedlock( mtx_t *restrict mutex,
const struct timespec *restrict time_point );  // desde C11
```

Bloqueia a thread atual até que o mutex apontado por `mutex` seja travado ou até que o ponto de tempo de calendário absoluto baseado em TIME_UTC apontado por `time_point` seja atingido.

Como esta função recebe um tempo absoluto, se uma duração for necessária, o ponto de tempo de calendário deve ser calculado manualmente.

O comportamento é indefinido se a thread atual já travou o mutex e o mutex não é recursivo.

O comportamento é indefinido se o mutex não suporta timeout.

Chamadas anteriores a [mtx_unlock](<#/doc/thread/mtx_unlock>) no mesmo mutex _sincronizam-se com_ esta operação (se esta operação for bem-sucedida), e todas as operações de travamento/destravamento em qualquer mutex dado formam uma única ordem total (semelhante à ordem de modificação de um atômico)

### Parâmetros

- **mutex** — ponteiro para o mutex a ser travado
- **time_point** — ponteiro para o tempo de calendário absoluto até o qual esperar pelo timeout

### Valor de retorno

[thrd_success](<#/doc/thread/thrd_errors>) se bem-sucedido, thrd_timedout se o tempo de timeout foi atingido antes que o mutex fosse travado, [thrd_error](<#/doc/thread/thrd_errors>) se ocorrer um erro.

### Referências

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.26.4.4 A função mtx_timedlock (p: 278)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.26.4.4 A função mtx_timedlock (p: 381-382)

### Veja também

[ timespec](<#/doc/chrono/timespec>)(C11) | tempo em segundos e nanossegundos
(estrutura)
[ mtx_lock](<#/doc/thread/mtx_lock>)(C11) | bloqueia até travar um mutex
(função)
[ mtx_trylock](<#/doc/thread/mtx_trylock>)(C11) | trava um mutex ou retorna sem bloquear se já estiver travado
(função)
[ mtx_unlock](<#/doc/thread/mtx_unlock>)(C11) | destrava um mutex
(função)
[documentação C++](<#/>) para timed_mutex::try_lock_until
[documentação C++](<#/>) para recursive_timed_mutex::try_lock_until

### Links externos

[Manual GNU GCC Libc: ISO-C-Mutexes](<https://www.gnu.org/software/libc/manual/html_node/ISO-C-Mutexes.html>)
---