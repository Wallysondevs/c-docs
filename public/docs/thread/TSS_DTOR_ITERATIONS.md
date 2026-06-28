# TSS_DTOR_ITERATIONS

Definido no cabeçalho [`<threads.h>`](<#/doc/thread>)

```c
#define TSS_DTOR_ITERATIONS /* unspecified */  // desde C11
```

Expande para uma [expressão constante](<#/doc/language/constant_expression>) integral positiva que define o número máximo de vezes que um destrutor para um ponteiro de armazenamento local de thread será chamado por [thrd_exit](<#/doc/thread/thrd_exit>).

Esta constante é equivalente a `PTHREAD_DESTRUCTOR_ITERATIONS` do POSIX.

### Referências

*   Padrão C17 (ISO/IEC 9899:2018):
    *   7.26.1/3 TSS_DTOR_ITERATIONS (p: 274)
*   Padrão C11 (ISO/IEC 9899:2011):
    *   7.26.1/3 TSS_DTOR_ITERATIONS (p: 376)