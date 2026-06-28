# kill_dependency

Definido no cabeçalho [`<stdatomic.h>`](<#/doc/thread>)

```c
A kill_dependency( A y );  // desde C11
```

Informa ao compilador que a árvore de dependência iniciada por uma operação de carregamento atômico [memory_order_consume](<#/doc/atomic/memory_order>) não se estende além do valor de retorno de `kill_dependency`; ou seja, o argumento não carrega uma dependência para o valor de retorno.

A função é implementada como uma macro. `A` é o tipo de y.

### Parâmetros

- **y** — a expressão cujo valor de retorno deve ser removido de uma árvore de dependência

### Valor de retorno

Retorna y, não sendo mais parte de uma árvore de dependência.

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.17.3.1 A macro kill_dependency (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.17.3.1 A macro kill_dependency (p: 203-204)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.17.3.1 A macro kill_dependency (p: 278)

### Veja também

[Documentação C++](<#/>) para kill_dependency
---