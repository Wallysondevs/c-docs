# tss_get

Definido no cabeçalho [`<threads.h>`](<#/doc/thread>)

```c
void *tss_get( tss_t tss_key );  // desde C11
```

Retorna o valor armazenado no armazenamento específico de thread para a thread atual, identificado por `tss_key`. Threads diferentes podem obter valores diferentes identificados pela mesma chave.

Na inicialização da thread (veja [thrd_create](<#/doc/thread/thrd_create>)), os valores associados a todas as chaves TSS são NULL. Valores diferentes podem ser colocados no armazenamento específico de thread com [tss_set](<#/doc/thread/tss_set>).

### Parâmetros

- **tss_key** — chave de armazenamento específico de thread, obtida de [tss_create](<#/doc/thread/tss_create>) e não excluída por [tss_delete](<#/doc/thread/tss_delete>)

### Valor de retorno

O valor em caso de sucesso, [NULL](<#/doc/types/NULL>) em caso de falha.

### Observações

O equivalente POSIX para esta função é [`pthread_getspecific`](<http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_getspecific.html>).

### Exemplo

| Esta seção está incompleta
Razão: nenhum exemplo

### Referências

* Padrão C17 (ISO/IEC 9899:2018):

  * 7.26.6.3 A função tss_get (p: 282)

* Padrão C11 (ISO/IEC 9899:2011):

  * 7.26.6.3 A função tss_get (p: 386)

### Veja também

[ tss_set](<#/doc/thread/tss_set>)(C11) | escreve no armazenamento específico de thread
(função)