# thrd_success, thrd_timedout, thrd_busy, thrd_nomem, thrd_error

Definido no cabeçalho [`<threads.h>`](<#/doc/thread>)

```c
enum {
thrd_success = /* unspecified */,
thrd_nomem = /* unspecified */,
thrd_timedout = /* unspecified */,
thrd_busy = /* unspecified */,
thrd_error = /* unspecified */
};  // desde C11
```

Identificadores para estados e erros de thread.

Constante | Explicação
`thrd_success` | indica valor de retorno bem-sucedido
`thrd_nomem` | indica valor de retorno malsucedido devido a condição de falta de memória
`thrd_timedout` | indica valor de retorno por tempo esgotado
`thrd_busy` | indica valor de retorno malsucedido devido a recurso temporariamente indisponível
`thrd_error` | indica valor de retorno malsucedido

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.26.1/5 thrd_success, thrd_timedout, ... (p: 275)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.26.1/5 thrd_success, thrd_timedout, ... (p: 377)