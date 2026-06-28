# thrd_exit

Definido no cabeçalho [`<threads.h>`](<#/doc/thread>)

```c
_Noreturn void thrd_exit( int res );  // desde C11
(até C23)  // até C23
[[noreturn]] void thrd_exit( int res );  // desde C23
```

Primeiro, para cada chave de armazenamento específico de thread que foi criada com um destrutor não nulo e para a qual o valor associado não é nulo (veja [tss_create](<#/doc/thread/tss_create>)), `thrd_exit` define o valor associado à chave como [NULL](<#/doc/types/NULL>) e então invoca o destrutor com o valor anterior da chave. A ordem em que os destrutores são invocados é não especificada.

Se, depois disso, ainda restarem chaves com destrutores e valores não nulos (por exemplo, se um destrutor executou [tss_set](<#/doc/thread/tss_set>)), o processo é repetido até [TSS_DTOR_ITERATIONS](<#/doc/thread/TSS_DTOR_ITERATIONS>) vezes.

Finalmente, a função `thrd_exit` encerra a execução da thread chamadora e define seu código de resultado para `res`.

Se a última thread no programa for terminada com `thrd_exit`, o programa inteiro termina como se chamasse [exit](<#/doc/program/exit>) com [EXIT_SUCCESS](<#/doc/program/EXIT_status>) como argumento (assim as funções registradas por [atexit](<#/doc/program/atexit>) são executadas no contexto dessa última thread)

### Parâmetros

- **res** — o valor de resultado a ser retornado

### Valor de retorno

(nenhum)

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.26.5.5 A função thrd_exit (p: 280)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.26.5.5 A função thrd_exit (p: 384)

### Veja também

[ thrd_join](<#/doc/thread/thrd_join>)(C11) | bloqueia até que uma thread termine
(função)
[ thrd_detach](<#/doc/thread/thrd_detach>)(C11) | desanexa uma thread
(função)