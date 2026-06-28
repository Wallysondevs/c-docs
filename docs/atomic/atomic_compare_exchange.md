# atomic_compare_exchange_weak, atomic_compare_exchange_strong, atomic_compare_exchange_weak_explicit, atomic_compare_exchange_strong_explicit

Definido no cabeçalho [`<stdatomic.h>`](<#/doc/thread>)

```c
_Bool atomic_compare_exchange_strong( volatile A* obj,
C* expected, C desired );  // desde C11
_Bool atomic_compare_exchange_weak( volatile A *obj,
C* expected, C desired );  // desde C11
_Bool atomic_compare_exchange_strong_explicit( volatile A* obj,
C* expected, C desired,
memory_order succ,
memory_order fail );  // desde C11
_Bool atomic_compare_exchange_weak_explicit( volatile A *obj,
C* expected, C desired,
memory_order succ,
memory_order fail );  // desde C11
```

Compara atomicamente o conteúdo da memória apontada por `obj` com o conteúdo da memória apontada por `expected`, e se forem bit a bit iguais, substitui o primeiro por `desired` (realiza uma operação de leitura-modificação-escrita). Caso contrário, carrega o conteúdo real da memória apontada por `obj` em `*expected` (realiza uma operação de carregamento).

Os modelos de memória para as operações de leitura-modificação-escrita e carregamento são `succ` e `fail` respectivamente. As versões (1-2) usam [memory_order_seq_cst](<#/doc/atomic/memory_order>) por padrão.

As formas fracas ((2) e (4)) das funções podem falhar de forma espúria, ou seja, agir como se *obj != *expected mesmo que sejam iguais. Quando um compare-and-exchange está em um loop, a versão fraca proporcionará melhor desempenho em algumas plataformas. Quando um compare-and-exchange fraco exigiria um loop e um forte não, o forte é preferível.

Esta é uma [função genérica](<#/doc/language/generic>) definida para todos os [tipos de objeto atômico](<#/doc/language/atomic>) `A`. O argumento é um ponteiro para um tipo atômico volátil para aceitar endereços de objetos atômicos tanto não-voláteis quanto [voláteis](<#/doc/language/volatile>) (por exemplo, I/O mapeado em memória), e a semântica volátil é preservada ao aplicar esta operação a objetos atômicos voláteis. `C` é o tipo não-atômico correspondente a `A`.

É não especificado se o nome de uma função genérica é uma macro ou um identificador declarado com ligação externa. Se uma definição de macro for suprimida para acessar uma função real (por exemplo, entre parênteses como (atomic_compare_exchange)(...)), ou um programa definir um identificador externo com o nome de uma função genérica, o comportamento é indefinido.

### Parâmetros

- **obj** — ponteiro para o objeto atômico a ser testado e modificado
- **expected** — ponteiro para o valor esperado a ser encontrado no objeto atômico
- **desired** — o valor a ser armazenado no objeto atômico se ele for como esperado
- **succ** — a ordenação de sincronização de memória para a operação de leitura-modificação-escrita se a comparação for bem-sucedida. Todos os valores são permitidos.
- **fail** — a ordenação de sincronização de memória para a operação de carregamento se a comparação falhar. Não pode ser [memory_order_release](<#/doc/atomic/memory_order>) ou [memory_order_acq_rel](<#/doc/atomic/memory_order>) e não pode especificar uma ordenação mais forte que `succ`

### Valor de retorno

O resultado da comparação: true se `*obj` era igual a `*exp`, false caso contrário.

### Observações

O comportamento da família `atomic_compare_exchange_*` é como se o seguinte fosse executado atomicamente:
```c
    if (memcmp(obj, expected, sizeof *obj) == 0) {
        memcpy(obj, &desired, sizeof *obj);
        return true;
    } else {
        memcpy(expected, obj, sizeof *obj);
        return false;
    }
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.17.7.4 As funções genéricas atomic_compare_exchange (p: 207)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.17.7.4 As funções genéricas atomic_compare_exchange (p: 283-284)

### Veja também

[ atomic_exchangeatomic_exchange_explicit](<#/doc/atomic/atomic_exchange>)(C11) | troca um valor com o valor de um objeto atômico
(função)
[Documentação C++](<#/>) para atomic_compare_exchange_weak, atomic_compare_exchange_strong, atomic_compare_exchange_weak_explicit, atomic_compare_exchange_strong_explicit