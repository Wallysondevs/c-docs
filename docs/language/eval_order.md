# Ordem de avaliação

A ordem de avaliação dos operandos de qualquer operador C, incluindo a ordem de avaliação dos argumentos de função em uma expressão de chamada de função, e a ordem de avaliação das subexpressões dentro de qualquer expressão é não especificada (exceto onde indicado abaixo). O compilador irá avaliá-los em qualquer ordem, e pode escolher outra ordem quando a mesma expressão for avaliada novamente.

Não existe o conceito de avaliação da esquerda para a direita ou da direita para a esquerda em C, o que não deve ser confundido com a associatividade da esquerda para a direita e da direita para a esquerda dos operadores: a expressão `f1() + f2() + f3()` é analisada como `(f1() + f2()) + f3()` devido à associatividade da esquerda para a direita do operador+, mas a chamada de função para `f3` pode ser avaliada primeiro, por último, ou entre `f1()` ou `f2()` em tempo de execução.

### Definições

#### Avaliações

Existem dois tipos de avaliações realizadas pelo compilador para cada expressão ou subexpressão (ambas opcionais):

*   _cálculo de valor_ : cálculo do valor retornado pela expressão. Isso pode envolver a determinação da identidade do objeto ([avaliação de lvalue](<#/doc/language/value_category>)) ou a leitura do valor previamente atribuído a um objeto (avaliação de rvalue)
*   _efeito colateral_ : acesso (leitura ou escrita) a um objeto designado por um lvalue [volatile](<#/doc/language/volatile>), modificação (escrita) a um objeto, sincronização atômica (desde C11), modificação de um arquivo, modificação do ambiente de ponto flutuante (se suportado), ou chamada de uma função que realiza qualquer uma dessas operações.

Se nenhum efeito colateral for produzido por uma expressão e o compilador puder determinar que o valor não é usado, a expressão [pode não ser avaliada](<#/doc/language/as_if>).

#### Ordenação

"sequenced-before" (sequenciado-antes) é uma relação assimétrica, transitiva e par-a-par entre avaliações dentro da mesma thread (pode se estender por threads se tipos atômicos e barreiras de memória estiverem envolvidos).

*   Se um [_ponto de sequência_](<https://en.wikipedia.org/wiki/Sequence_point> "enwiki:Sequence point") estiver presente entre as subexpressões E1 e E2, então tanto o cálculo de valor quanto os efeitos colaterais de E1 são _sequenced-before_ (sequenciados-antes) de cada cálculo de valor e efeito colateral de E2
*   Se a avaliação A é sequenciada antes da avaliação B, então a avaliação de A estará completa antes que a avaliação de B comece.
*   Se A não é sequenciada antes de B e B é sequenciada antes de A, então a avaliação de B estará completa antes que a avaliação de A comece.
*   Se A não é sequenciada antes de B e B não é sequenciada antes de A, então existem duas possibilidades:
    *   as avaliações de A e B são não sequenciadas: elas podem ser realizadas em qualquer ordem e podem se sobrepor (dentro de uma única thread de execução, o compilador pode intercalar as instruções da CPU que compõem A e B)
    *   as avaliações de A e B são sequenciadas de forma indeterminada: elas podem ser realizadas em qualquer ordem, mas não podem se sobrepor: ou A estará completa antes de B, ou B estará completa antes de A. A ordem pode ser a oposta na próxima vez que a mesma expressão for avaliada.

| (desde C11) |
| :---------- |

### Regras

1) Existe um ponto de sequência após a avaliação de todos os argumentos da função e do designador da função, e antes da chamada de função real.

2) Existe um ponto de sequência após a avaliação do primeiro (esquerdo) operando e antes da avaliação do segundo (direito) operando dos seguintes operadores binários: `&&` (AND lógico), `||` (OR lógico), e `,` (vírgula).

3) Existe um ponto de sequência após a avaliação do primeiro (esquerdo) operando e antes da avaliação do segundo ou terceiro operando (o que for avaliado) do operador condicional `?:`

4) Existe um ponto de sequência após a avaliação de uma expressão completa (uma expressão que não é uma subexpressão: tipicamente algo que termina com um ponto e vírgula ou uma [instrução de controle](<#/doc/language/statements>) de `if`/`switch`/`while`/`do`) e antes da próxima expressão completa.

5) Existe um ponto de sequência no final de um declarador completo.
6) Existe um ponto de sequência imediatamente antes do retorno de uma função de biblioteca.
7) Existe um ponto de sequência após a ação associada a cada especificador de conversão em E/S formatada (em particular, é bem formado para [scanf](<#/doc/io/fscanf>) escrever diferentes campos na mesma variável e para [printf](<#/doc/io/fprintf>) ler e modificar ou modificar a mesma variável mais de uma vez usando %n)
8) Existem pontos de sequência antes e imediatamente após cada chamada a uma função de comparação feita pelas funções de biblioteca [qsort](<#/doc/algorithm/qsort>) e [bsearch](<#/doc/algorithm/bsearch>), bem como entre qualquer chamada à função de comparação e o movimento dos objetos associados feito por [qsort](<#/doc/algorithm/qsort>) | (desde C99)
9) Os cálculos de valor (mas não os efeitos colaterais) dos operandos de qualquer operador são sequenciados antes do cálculo de valor do resultado do operador (mas não seus efeitos colaterais).
10) O efeito colateral (modificação do argumento esquerdo) do operador de atribuição direta e de todos os operadores de atribuição composta é sequenciado após o cálculo de valor (mas não os efeitos colaterais) de ambos os argumentos esquerdo e direito.
11) O cálculo de valor dos operadores de pós-incremento e pós-decremento é sequenciado antes de seu efeito colateral.
12) Uma chamada de função que não é sequenciada antes ou sequenciada depois de outra chamada de função é sequenciada de forma indeterminada (instruções da CPU que constituem diferentes chamadas de função não podem ser intercaladas, mesmo que as funções sejam inlined)
13) Em expressões de lista de [inicialização](<#/doc/language/initialization>), todas as avaliações são sequenciadas de forma indeterminada
14) Em relação a uma chamada de função sequenciada de forma indeterminada, a operação dos operadores de atribuição composta, e ambas as formas prefixada e postfixada dos operadores de incremento e decremento são avaliações únicas. | (desde C11)

### Comportamento indefinido

1) Se um efeito colateral em um objeto escalar não é sequenciado em relação a outro efeito colateral no mesmo objeto escalar, o [comportamento é indefinido](<#/doc/language/behavior>).
```c
    i = ++i + i++; // undefined behavior
    i = i++ + 1; // undefined behavior
    f(++i, ++i); // undefined behavior
    f(i = -1, i = -1); // undefined behavior
```

2) Se um efeito colateral em um objeto escalar não é sequenciado em relação a um cálculo de valor usando o valor do mesmo objeto escalar, o comportamento é indefinido.
```c
    f(i, i++); // undefined behavior
    a[i] = i++; // undefined bevahior
```

3) As regras acima se aplicam desde que pelo menos uma ordenação permitida de subexpressões permita tal efeito colateral não sequenciado.

### Veja também

[Precedência de operadores](<#/doc/language/operator_precedence>) que define como as expressões são construídas a partir de sua representação no código fonte.

[Documentação C++](<#/>) para Ordem de avaliação