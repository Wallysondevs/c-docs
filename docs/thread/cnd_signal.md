# cnd_signal

Definido no cabeçalho [`<threads.h>`](<#/doc/thread>)

```c
int cnd_signal( cnd_t *cond );  // desde C11
```

Desbloqueia uma thread que atualmente aguarda na variável de condição apontada por `cond`. Se nenhuma thread estiver bloqueada, não faz nada e retorna `thrd_success`.

### Parâmetros

- **cond** — ponteiro para uma variável de condição

### Valor de retorno

[thrd_success](<#/doc/thread/thrd_errors>) se bem-sucedido, [thrd_error](<#/doc/thread/thrd_errors>) caso contrário.

### Referências

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.26.3.4 A função cnd_signal (p: 276)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.26.3.4 A função cnd_signal (p: 379)

### Veja também

[ cnd_broadcast](<#/doc/thread/cnd_broadcast>)(C11) | desbloqueia todas as threads bloqueadas em uma variável de condição
(função)
[Documentação C++](<#/>) para condition_variable::notify_one
[Documentação C++](<#/>) para condition_variable_any::notify_one