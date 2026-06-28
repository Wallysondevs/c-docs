# Tipos Atômicos

### Sintaxe

---
`_Atomic` `(` type-name `)` | (1) | (desde C11)
`_Atomic` type-name | (2) | (desde C11)

1) Usado como um especificador de tipo; isso designa um novo tipo atômico

2) Usado como um qualificador de tipo; isso designa a versão atômica de type-name. Nesta função, pode ser misturado com [`const`](<#/doc/language/const>), [`volatile`](<#/doc/language/volatile>) e [`restrict`](<#/doc/language/restrict>), embora, ao contrário de outros qualificadores, a versão atômica de type-name possa ter um tamanho, alinhamento e representação de objeto diferentes.

- **type-name** — qualquer tipo que não seja array ou função. Para (1), type-name também não pode ser atômico ou cvr-qualificado

O cabeçalho [`<stdatomic.h>`](<#/doc/thread>) define [muitos aliases de tipo de conveniência](<#/doc/thread>), de [`atomic_bool`](<#/doc/thread>) a [`atomic_uintmax_t`](<#/doc/thread>), que simplificam o uso desta palavra-chave com tipos embutidos e de biblioteca.
```c
    _Atomic const int* p1;  // p é um ponteiro para um int const atômico
    const atomic_int* p2;   // o mesmo
    const _Atomic(int)* p3; // o mesmo
```

Se a constante de macro `__STDC_NO_ATOMICS__` for definida pelo compilador, a palavra-chave `_Atomic` não é fornecida.

### Explicação

Objetos de tipos atômicos são os únicos objetos que estão livres de [condições de corrida de dados](<#/doc/language/memory_model>); ou seja, eles podem ser modificados por duas threads concorrentemente ou modificados por uma e lidos por outra.

Cada objeto atômico tem sua própria _ordem de modificação_ associada, que é uma ordem total das modificações feitas a esse objeto. Se, do ponto de vista de alguma thread, a modificação `A` de algum atômico `M` [acontece-antes](<#/doc/atomic/memory_order>) da modificação `B` do mesmo atômico `M`, então na ordem de modificação de `M`, `A` ocorre antes de `B`.

Note que, embora cada objeto atômico tenha sua própria ordem de modificação, não existe uma única ordem total; diferentes threads podem observar modificações em diferentes objetos atômicos em ordens distintas.

Existem quatro tipos de coerência que são garantidos para todas as operações atômicas:

*   **coerência escrita-escrita**: Se uma operação `A` que modifica um objeto atômico `M` _acontece-antes_ de uma operação `B` que modifica `M`, então `A` aparece antes de `B` na ordem de modificação de `M`.
*   **coerência leitura-leitura**: Se um cálculo de valor `A` de um objeto atômico `M` acontece antes de um cálculo de valor `B` de `M`, e `A` obtém seu valor de um efeito colateral `X` em `M`, então o valor calculado por `B` é o valor armazenado por `X` ou é o valor armazenado por um efeito colateral `Y` em `M`, onde `Y` aparece depois de `X` na ordem de modificação de `M`.
*   **coerência leitura-escrita**: Se um cálculo de valor `A` de um objeto atômico `M` _acontece-antes_ de uma operação `B` em `M`, então `A` obtém seu valor de um efeito colateral `X` em `M`, onde `X` aparece antes de `B` na ordem de modificação de `M`.
*   **coerência escrita-leitura**: Se um efeito colateral `X` em um objeto atômico `M` _acontece-antes_ de um cálculo de valor `B` de `M`, então a avaliação `B` obtém seu valor de `X` ou de um efeito colateral `Y` que aparece depois de `X` na ordem de modificação de `M`.

Algumas operações atômicas também são operações de sincronização; elas podem ter semânticas de liberação (release semantics), semânticas de aquisição (acquire semantics) ou semânticas sequencialmente consistentes (sequentially-consistent semantics) adicionais. Veja [memory_order](<#/doc/atomic/memory_order>).

Os [operadores de incremento e decremento](<#/doc/language/operator_incdec>) embutidos e a [atribuição composta](<#/doc/language/operator_assignment>) são operações atômicas de leitura-modificação-escrita com ordenação sequencialmente consistente total (como se estivessem usando [memory_order_seq_cst](<#/doc/atomic/memory_order>)). Se semânticas de sincronização menos rigorosas forem desejadas, as [funções da biblioteca padrão](<#/doc/thread>) podem ser usadas em vez disso.

Propriedades atômicas são significativas apenas para [expressões lvalue](<#/doc/language/value_category>). A conversão de lvalue para rvalue (que modela uma leitura de memória de um local atômico para um registrador da CPU) remove a atomicidade juntamente com outros qualificadores.

| Esta seção está incompleta
Motivo: mais, revisar interação com memory_order e páginas da biblioteca atômica

### Notas

Acessar um membro de uma struct/union atômica é [comportamento indefinido](<#/>).

O tipo de biblioteca [sig_atomic_t](<#/doc/program/sig_atomic_t>) não fornece sincronização entre threads ou ordenação de memória, apenas atomicidade.

Os tipos [`volatile`](<#/doc/language/volatile>) não fornecem sincronização entre threads, ordenação de memória ou atomicidade.

Recomenda-se que as implementações garantam que a representação de `_Atomic(T)` em C seja a mesma que a de `std::atomic<T>` em C++ para cada tipo `T` possível. Os mecanismos usados para garantir atomicidade e ordenação de memória devem ser compatíveis.

### Palavras-chave

[`_Atomic`](<#/doc/keyword/_Atomic>)

### Exemplo

Execute este código
```c
    #include <stdatomic.h>
    #include <stdio.h>
    #include <threads.h>
    
    atomic_int acnt;
    int cnt;
    
    int f(void* thr_data)
    {
        for (int n = 0; n < 1000; ++n)
        {
            ++cnt;
            ++acnt;
            // para este exemplo, a ordem de memória relaxada é suficiente, ex:
            // atomic_fetch_add_explicit(&acnt, 1, memory_order_relaxed);
        }
        return 0;
    }
    
    int main(void)
    {
        thrd_t thr[10];
        for (int n = 0; n < 10; ++n)
            thrd_create(&thr[n], f, NULL);
        for (int n = 0; n < 10; ++n)
            thrd_join(thr[n], NULL);
    
        printf("The atomic counter is %u\n", acnt);
        printf("The non-atomic counter is %u\n", cnt);
    }
```

Saída possível:
```
    The atomic counter is 10000
    The non-atomic counter is 8644
```

### Referências

*   Padrão C23 (ISO/IEC 9899:2024):

    *   6.7.2.4 Especificadores de tipo atômico (p: TBD)

    *   7.17 Atômicos <stdatomic.h> (p: TBD)

*   Padrão C17 (ISO/IEC 9899:2018):

    *   6.7.2.4 Especificadores de tipo atômico (p: 87)

    *   7.17 Atômicos <stdatomic.h> (p: 200-209)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   6.7.2.4 Especificadores de tipo atômico (p: 121)

    *   7.17 Atômicos <stdatomic.h> (p: 273-286)

### Veja também

**[Biblioteca de suporte à concorrência](<#/doc/thread>)**
---
[Documentação C++](<#/>) para atomic