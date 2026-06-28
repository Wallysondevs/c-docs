# cnd_destroy

Definido no cabeçalho [`<threads.h>`](<#/doc/thread>)

```c
void cnd_destroy( cnd_t* cond );  // desde C11
```

Destrói a variável de condição apontada por `cond`.

Se houver threads esperando em `cond`, o comportamento é indefinido.

### Parâmetros

- **cond** — ponteiro para a variável de condição a ser destruída

### Valor de retorno

(nenhum)

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.26.3.2 A função cnd_destroy (p: 276)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.26.3.2 A função cnd_destroy (p: 378-379)

### Veja também

[Documentação C++](<#/>) para ~condition_variable
---
[Documentação C++](<#/>) para ~condition_variable_any