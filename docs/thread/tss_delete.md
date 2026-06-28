# tss_delete

Definido no cabeçalho [`<threads.h>`](<#/doc/thread>)

```c
void tss_delete( tss_t tss_id );  // desde C11
```

Destrói o armazenamento específico de thread identificado por `tss_id`.

O destrutor, se um foi registrado por [tss_create](<#/doc/thread/tss_create>), não é chamado (eles são chamados apenas na saída da thread, seja por [thrd_exit](<#/doc/thread/thrd_exit>) ou pelo retorno da função da thread), é responsabilidade do programador garantir que cada thread que tem conhecimento de `tss_id` tenha realizado toda a limpeza necessária, antes que a chamada para `tss_delete` seja feita.

Se `tss_delete` for chamado enquanto outra thread estiver executando destrutores para `tss_id`, é não especificado se isso altera o número de invocações ao destrutor associado.

Se `tss_delete` for chamado enquanto a thread chamadora estiver executando destrutores, então o destrutor associado a `tss_id` não será executado novamente nesta thread.

### Parâmetros

- **tss_id** — chave de armazenamento específico de thread previamente retornada por [tss_create](<#/doc/thread/tss_create>) e ainda não excluída por **tss_delete**

### Valor de retorno

(nenhum)

### Notas

O equivalente POSIX desta função é [`pthread_key_delete`](<http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_key_delete.html>).

A razão pela qual `tss_delete` nunca chama destrutores é que os destrutores (chamados na saída da thread) são normalmente destinados a serem executados pela mesma thread que originalmente definiu o valor (via [tss_set](<#/doc/thread/tss_set>)) com o qual o destrutor lidará, e podem até depender dos valores desse ou de outros dados específicos de thread, conforme vistos por essa thread. A thread que executa `tss_delete` não tem acesso ao TSS de outras threads. Mesmo que fosse possível chamar o destrutor para o próprio valor de cada thread associado a `tss_id`, `tss_delete` teria que sincronizar com cada thread, nem que fosse apenas para examinar se o valor deste TSS nessa thread é nulo (destrutores são chamados apenas para valores não nulos).

### Exemplo

| Esta seção está incompleta
Razão: nenhum exemplo

### Referências

* Padrão C17 (ISO/IEC 9899:2018):

  * 7.26.6.2 A função tss_delete (p: 282)

* Padrão C11 (ISO/IEC 9899:2011):

  * 7.26.6.2 A função tss_delete (p: 386)