# cnd_init

Definido no cabeçalho [`<threads.h>`](<#/doc/thread>) | | (desde C11)

```c
int cnd_init( cnd_t* cond );
```

Inicializa uma nova variável de condição. O objeto apontado por `cond` será definido com um valor que identifica a variável de condição.

### Parâmetros

- **cond** — ponteiro para uma variável para armazenar o identificador da variável de condição

### Valor de retorno

[thrd_success](<#/doc/thread/thrd_errors>) se a variável de condição foi criada com sucesso. Caso contrário, retorna [thrd_nomem](<#/doc/thread/thrd_errors>) se não houver memória suficiente ou `thrd_error` se outro erro ocorreu.

### Referências

*   Padrão C17 (ISO/IEC 9899:2018):

*   7.26.3.3 A função cnd_init (p: 276)

*   Padrão C11 (ISO/IEC 9899:2011):

*   7.26.3.3 A função cnd_init (p: 379)

### Veja também

[Documentação C++](<#/>) para condition_variable
---
[Documentação C++](<#/>) para condition_variable_any