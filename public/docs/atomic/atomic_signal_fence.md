# atomic_signal_fence

Definido no cabeçalho [`<stdatomic.h>`](<#/doc/thread>)

```c
void atomic_signal_fence( memory_order order );  // desde C11
```

Estabelece a ordenação de sincronização de memória de acessos não atômicos e atômicos relaxados, conforme instruído por `order`, entre uma thread e um manipulador de sinal executado na mesma thread. Isso é equivalente a [atomic_thread_fence](<#/doc/atomic/atomic_thread_fence>), exceto que nenhuma instrução de CPU para ordenação de memória é emitida. Apenas a reordenação das instruções pelo compilador é suprimida conforme `order` instrui. Por exemplo, uma barreira com semântica de liberação impede que leituras ou escritas sejam movidas para além de escritas subsequentes e uma barreira com semântica de aquisição impede que leituras ou escritas sejam movidas para antes de leituras precedentes.

### Parâmetros

- **order** — a ordenação de memória executada por esta barreira

### Valor de retorno

(nenhum)

### Referências

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.17.4.2 A função atomic_signal_fence (p: 204-205)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.17.4.2 A função atomic_signal_fence (p: 279)

### Veja também

[ atomic_thread_fence](<#/doc/atomic/atomic_thread_fence>)(C11) | primitiva de sincronização de barreira genérica dependente da ordenação de memória
(função)
[Documentação C++](<#/>) para atomic_signal_fence