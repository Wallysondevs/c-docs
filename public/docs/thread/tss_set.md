# tss_set

Definido no cabeçalho [`<threads.h>`](<#/doc/thread>)

```c
int tss_set( tss_t tss_id, void *val );  // desde C11
```

Define o valor do armazenamento específico de thread identificado por `tss_id` para a thread atual como `val`. Diferentes threads podem definir valores distintos para a mesma chave.

O destrutor, se disponível, não é invocado.

### Parâmetros

- **tss_id** — chave de armazenamento específico de thread, obtida de [tss_create](<#/doc/thread/tss_create>) e não excluída por [tss_delete](<#/doc/thread/tss_delete>)
- **val** — valor a ser definido para o armazenamento específico de thread

### Valor de retorno

[thrd_success](<#/doc/thread/thrd_errors>) se bem-sucedido, [thrd_error](<#/doc/thread/thrd_errors>) caso contrário.

### Observações

O equivalente POSIX desta função é `[`pthread_setspecific`](<http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_setspecific.html>)`.

Tipicamente, TSS é usado para armazenar ponteiros para blocos de memória alocada dinamicamente que foram reservados para uso pela thread chamadora.

`tss_set` pode ser chamado no destrutor TSS. Se o destrutor sair com um valor não-NULL no armazenamento TSS, ele será tentado novamente por [thrd_exit](<#/doc/thread/thrd_exit>) até [TSS_DTOR_ITERATIONS](<#/doc/thread/TSS_DTOR_ITERATIONS>) vezes, após o que o armazenamento será perdido.

### Exemplo

| Esta seção está incompleta
Razão: melhorar, talvez procurar exemplos POSIX para inspiração
```
    int thread_func(void *arg) {
        tss_t key;
        if (thrd_success == tss_create(&key, free)) {
            tss_set(key, malloc(4)); // armazena um ponteiro no TSS
            // ...
        }
    } // chama free() para o ponteiro armazenado no TSS
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.26.6.4 A função tss_set (p: 282-283)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.26.6.4 A função tss_set (p: 387)

### Veja também

[ tss_get](<#/doc/thread/tss_get>)(C11) | lê do armazenamento específico de thread
(função)