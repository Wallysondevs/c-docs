# mtx_destroy

Definido no cabeçalho [`<threads.h>`](<#/doc/thread>)

```c
void mtx_destroy( mtx_t *mutex );  // desde C11
```

Destrói o mutex apontado por `mutex`.

Se houver threads esperando em `mutex`, o comportamento é indefinido.

### Parâmetros

- **mutex** — ponteiro para o mutex a ser destruído

### Valor de retorno

(nenhum)

### Referências

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.26.4.1 A função mtx_destroy (p: 277)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.26.4.1 A função mtx_destroy (p: 380)

### Veja também

[Documentação C++](<#/>) para ~mutex
---
[Documentação C++](<#/>) para ~timed_mutex
[Documentação C++](<#/>) para ~recursive_mutex
[Documentação C++](<#/>) para ~recursive_timed_mutex