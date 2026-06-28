# thrd_create

Definido no cabeçalho [`<threads.h>`](<#/doc/thread>)

```c
int thrd_create( thrd_t *thr, thrd_start_t func, void *arg );  // desde C11
```

Cria uma nova thread executando a função `func`. A função é invocada como func(arg).

Se bem-sucedido, o objeto apontado por `thr` é definido como o identificador da nova thread.

A conclusão desta função _sincroniza-se com_ o início da thread.

### Parâmetros

- **thr** — ponteiro para o local de memória onde será colocado o identificador da nova thread
- **func** — função a ser executada
- **arg** — argumento a ser passado para a função

### Valor de retorno

[thrd_success](<#/doc/thread/thrd_errors>) se a criação da nova thread foi bem-sucedida. Caso contrário, retorna [thrd_nomem](<#/doc/thread/thrd_errors>) se não houver memória suficiente ou [thrd_error](<#/doc/thread/thrd_errors>) se outro erro ocorreu.

### Observações

Os identificadores de thread podem ser reutilizados para novas threads assim que a thread tiver terminado e sido "joined" ou "detached".

O tipo [thrd_start_t](<#/doc/thread>) é um typedef de int(*)(void*), o que difere do equivalente POSIX void*(*)(void*)

Todos os valores de armazenamento específicos da thread (veja [tss_create](<#/doc/thread/tss_create>)) são inicializados para [NULL](<#/doc/types/NULL>).

O retorno da função `func` é equivalente a chamar [thrd_exit](<#/doc/thread/thrd_exit>) com o argumento igual ao valor de retorno de `func`.

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.26.5.1 A função thrd_create (p: 279)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.26.5.1 A função thrd_create (p: 383)

### Veja também

[ thrd_detach](<#/doc/thread/thrd_detach>)(C11) | desanexa uma thread
(função)
[ thrd_join](<#/doc/thread/thrd_join>)(C11) | bloqueia até que uma thread termine
(função)
[Documentação C++](<#/>) para thread