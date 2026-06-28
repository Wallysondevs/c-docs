# mtx_init

Definido no cabeçalho [`<threads.h>`](<#/doc/thread>)

```c
int mtx_init( mtx_t* mutex, int type );  // desde C11
```

Cria um novo objeto mutex com `type`. O objeto apontado por `mutex` é definido como um identificador do mutex recém-criado.

`type` deve ter um dos seguintes valores:

  * [mtx_plain](<#/doc/thread/mtx_types>) - um mutex simples e não recursivo é criado.
  * [mtx_timed](<#/doc/thread/mtx_types>) - um mutex não recursivo, que suporta timeout, é criado.
  * [mtx_plain](<#/doc/thread/mtx_types>) | [mtx_recursive](<#/doc/thread/mtx_types>) - um mutex recursivo é criado.
  * [mtx_timed](<#/doc/thread/mtx_types>) | [mtx_recursive](<#/doc/thread/mtx_types>) - um mutex recursivo, que suporta timeout, é criado.

### Parâmetros

- **mutex** — ponteiro para o mutex a ser inicializado
- **type** — o tipo do mutex

### Valor de retorno

[thrd_success](<#/doc/thread/thrd_errors>) se bem-sucedido, [thrd_error](<#/doc/thread/thrd_errors>) caso contrário.

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.26.4.2 A função mtx_init (p: 277-278)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.26.4.2 A função mtx_init (p: 381)

### Veja também

[Documentação C++](<#/>) para mutex
---
[Documentação C++](<#/>) para timed_mutex
[Documentação C++](<#/>) para recursive_mutex
[Documentação C++](<#/>) para recursive_timed_mutex