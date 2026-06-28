# thrd_join

Definido no cabeçalho [`<threads.h>`](<#/doc/thread>)

```c
int thrd_join( thrd_t thr, int *res );  // desde C11
```

Bloqueia a thread atual até que a thread identificada por `thr` finalize sua execução.

Se `res` não for um ponteiro nulo, o código de resultado da thread é colocado no local apontado por `res`.

A terminação da thread _sincroniza-se com_ a conclusão desta função.

O comportamento é indefinido se a thread foi previamente desanexada (detached) ou aguardada (joined) por outra thread.

### Parâmetros

- **thr** — identificador da thread a ser aguardada (joined)
- **res** — local para colocar o código de resultado

### Valor de retorno

[thrd_success](<#/doc/thread/thrd_errors>) se bem-sucedido, [thrd_error](<#/doc/thread/thrd_errors>) caso contrário.

### Referências

* Padrão C17 (ISO/IEC 9899:2018):

  

* 7.26.5.6 A função thrd_join (p: 280-281)

* Padrão C11 (ISO/IEC 9899:2011):

  

* 7.26.5.6 A função thrd_join (p: 384-385)

### Veja também

[ thrd_detach](<#/doc/thread/thrd_detach>)(C11) | desanexa uma thread
(função)
[ thrd_exit](<#/doc/thread/thrd_exit>)(C11) | termina a thread chamadora
(função)
[Documentação C++](<#/>) para join