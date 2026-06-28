# tss_create

Definido no cabeçalho [`<threads.h>`](<#/doc/thread>)

```c
int tss_create( tss_t* tss_key, tss_dtor_t destructor );  // desde C11
```

  
Cria uma nova chave de armazenamento específico de thread e a armazena no objeto apontado por `tss_key`. Embora o mesmo valor de chave possa ser usado por diferentes threads, os valores vinculados à chave por [tss_set](<#/doc/thread/tss_set>) são mantidos por thread e persistem durante a vida útil da thread chamadora.

O valor [NULL](<#/doc/types/NULL>) é associado à chave recém-criada em todas as threads existentes e, após a criação de uma thread, os valores associados a todas as chaves TSS são inicializados para [NULL](<#/doc/types/NULL>).

Se `destructor` não for um ponteiro nulo, então também associa o destrutor que é chamado quando o armazenamento é liberado por [thrd_exit](<#/doc/thread/thrd_exit>) (mas não por [tss_delete](<#/doc/thread/tss_delete>) e não na terminação do programa por [exit](<#/doc/program/exit>)).

Uma chamada para `tss_create` de dentro de um destrutor de armazenamento específico de thread resulta em comportamento indefinido.

### Parâmetros

tss_key  |  \-  |  ponteiro para o local de memória para armazenar a nova chave de armazenamento específico de thread   
destructor  |  \-  |  ponteiro para uma função a ser chamada na saída da thread   
  
### Notas

O equivalente POSIX desta função é [`pthread_key_create`](<http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_key_create.html>)`.`

### Valor de retorno

[thrd_success](<#/doc/thread/thrd_errors>) se bem-sucedido, [thrd_error](<#/doc/thread/thrd_errors>) caso contrário.

### Exemplo

| Esta seção está incompleta  
Razão: melhorar, talvez procurar exemplos POSIX para inspiração   
```
    int thread_func(void *arg) {
        tss_t key;
        if (thrd_success == tss_create(&key, free)) {
            tss_set(key, malloc(4)); // stores a pointer on TSS
            // ...
        }
    } // chama free() para o ponteiro armazenado em TSS
```
  
### Referências

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.26.6.1 A função tss_create (p: 281-282) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.26.6.1 A função tss_create (p: 386)