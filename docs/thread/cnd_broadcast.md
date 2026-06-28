# cnd_broadcast

Definido no cabeçalho [`<threads.h>`](<#/doc/thread>)

```c
int cnd_broadcast( cnd_t *cond );  // desde C11
```

Desbloqueia todas as threads que estão bloqueadas na variável de condição `cond` no momento da chamada. Se nenhuma thread estiver bloqueada em `cond`, a função não faz nada e retorna `thrd_success`.

### Parâmetros

- **cond** — ponteiro para uma variável de condição

### Valor de retorno

[thrd_success](<#/doc/thread/thrd_errors>) se bem-sucedido, [thrd_error](<#/doc/thread/thrd_errors>) caso contrário.

### Referências

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.26.3.1 A função cnd_broadcast (p: 275-276)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.26.3.1 A função cnd_broadcast (p: 378)

### Veja também

[ cnd_signal](<#/doc/thread/cnd_signal>)(C11) | desbloqueia uma thread bloqueada em uma variável de condição
(função) |
[Documentação C++](<#/>) para condition_variable::notify_all
[Documentação C++](<#/>) para condition_variable_any::notify_all