# mtx_plain, mtx_recursive, mtx_timed

Definido no cabeçalho [`<threads.h>`](<#/doc/thread>)

```c
enum {
mtx_plain = /* unspecified */,
mtx_recursive = /* unspecified */,
mtx_timed = /* unspecified */
};  // desde C11
```

Quando passado para [mtx_init](<#/doc/thread/mtx_init>), identifica o tipo de um mutex a ser criado.

Constante | Explicação
`mtx_plain` | mutex simples
`mtx_recursive` | mutex recursivo
`mtx_timed` | mutex com tempo limite

### Referências

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.26.1/5 mtx_plain, mtx_recursive, mtx_timed (p: 274-275)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.26.1/5 mtx_plain, mtx_recursive, mtx_timed (p: 377)

### Veja também

[ mtx_init](<#/doc/thread/mtx_init>)(C11) | cria um mutex
(função)