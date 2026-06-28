# Enumerações

Um _tipo enumerado_ é um [tipo](<#/doc/language/compatible_type>) distinto cujo valor é um valor do seu _tipo subjacente_ (veja abaixo), que inclui os valores de constantes explicitamente nomeadas (_constantes de enumeração_).

### Sintaxe

O tipo enumerado é declarado usando o seguinte _especificador de enumeração_ como o especificador de tipo na [gramática de declaração](<#/doc/language/declarations>):

---
`enum` attr-spec-seq ﻿(optional) identifier ﻿(optional) `{` enumerator-list `}` | (1) |
`enum` attr-spec-seq ﻿(optional) identifier ﻿(optional) `:` type `{` enumerator-list `}` | (2) | (desde C23)

1) Declara uma enumeração sem um tipo subjacente fixo.

2) Declara uma enumeração de tipo subjacente fixo `type`.

onde `enumerator-list` é uma lista de enumeradores separada por vírgulas (com vírgula final permitida) (desde C99), cada um dos quais tem a forma:

---
enumeration-constant attr-spec-seq ﻿(optional) | (1) |
enumeration-constant attr-spec-seq ﻿(optional) `=` constant-expression | (2) |

onde

- **identifier, enumeration-constant** — identificadores que são introduzidos por esta declaração
- **constant-expression** — [expressão constante inteira](<#/doc/language/constant_expression>) cujo valor é representável como um valor do tipo int (até C23). Se a enumeração tiver um tipo subjacente fixo, representável como um valor do tipo (desde C23)
- **attr-spec-seq** — (C23)lista opcional de [atributos](<#/doc/language/attributes>),

* aplicada a toda a enumeração se aparecer após `enum`,
* aplicada ao enumerador se aparecer após `enumeration-constant`

Assim como com [struct](<#/doc/language/struct>) ou [union](<#/doc/language/union>), uma declaração que introduz um tipo enumerado e uma ou mais constantes de enumeração também pode declarar um ou mais objetos desse tipo ou de um tipo derivado dele.
```c
    enum color { RED, GREEN, BLUE } c = RED, *cp = &c;
    // introduz o tipo enum color
    // as constantes inteiras RED, GREEN, BLUE
    // o objeto c do tipo enum color
    // o objeto cp do tipo ponteiro para enum color
```

### Explicação

Cada `enumeration-constant` que aparece no corpo de um especificador de enumeração torna-se uma [constante inteira](<#/doc/language/constant_expression>) do tipo int (até C23) no escopo envolvente e pode ser usada sempre que constantes inteiras forem necessárias (por exemplo, como um rótulo `case` ou como um tamanho de array não-VLA).

Durante o processamento de cada constante de enumeração na lista de enumeradores, o tipo da constante de enumeração deve ser:

* o tipo previamente declarado, se for uma redeclaração da mesma constante de enumeração; ou,
* o tipo enumerado, para uma enumeração com tipo subjacente fixo; ou,
* int, se não houver constantes de enumeração anteriores na lista de enumeradores e nenhum `=` explícito com uma expressão constante inteira definidora; ou,
* int, se dado explicitamente com `=` e o valor da expressão constante inteira for representável por um int; ou,
* o tipo da expressão constante inteira, se dado explicitamente com `=` e se o valor da expressão constante inteira não for representável por int; ou,
* o tipo do valor da última constante de enumeração com 1 adicionado a ele. Se tal expressão constante inteira causaria um estouro (overflow) ou uma quebra (wraparound) do valor da constante de enumeração anterior a partir da adição de 1, o tipo assume um dos seguintes:
    * um tipo inteiro assinado de tamanho adequado (excluindo os tipos inteiros assinados de precisão de bit) capaz de representar o valor da constante de enumeração anterior mais 1; ou,
    * um tipo inteiro não assinado de tamanho adequado (excluindo os tipos inteiros não assinados de precisão de bit) capaz de representar o valor da constante de enumeração anterior mais 1.

Um tipo inteiro assinado é escolhido se a constante de enumeração anterior à qual está sendo adicionado for do tipo inteiro assinado. Um tipo inteiro não assinado é escolhido se a constante de enumeração anterior for do tipo inteiro não assinado. Se não houver um tipo inteiro de tamanho adequado descrito anteriormente que possa representar o novo valor, então a enumeração não tem um tipo capaz de representar todos os seus valores. | (desde C23)
```c
    enum color { RED, GREEN, BLUE } r = RED;
    switch(r)
    {
    case RED:
        puts("red");
        break;
    case GREEN:
        puts("green");
        break;
    case BLUE:
        puts("blue");
        break;
    }
```

Se `enumeration-constant` for seguido por `=` `constant-expression`, seu valor é o valor dessa expressão constante. Se `enumeration-constant` não for seguido por `=` `constant-expression`, seu valor é o valor um maior que o valor do enumerador anterior na mesma enumeração. O valor do primeiro enumerador (se não usar `=` `constant-expression`) é zero.
```c
    enum Foo { A, B, C = 10, D, E = 1, F, G = F + C };
    // A=0, B=1, C=10, D=11, E=1, F=2, G=12
```

O próprio identificador, se usado, torna-se o nome do tipo enumerado no [espaço de nomes](<#/doc/language/name_space>) de tags e requer o uso da palavra-chave `enum` (a menos que seja `typedef`'d para o espaço de nomes comum).
```c
    enum color { RED, GREEN, BLUE };
    enum color r = RED; // OK
    // color x = GREEN; // Erro: color não está no espaço de nomes comum
    typedef enum color color_t;
    color_t x = GREEN; // OK
```

Cada tipo enumerado sem um tipo subjacente fixo (desde C23) é [compatível](<#/doc/language/compatible_type>) com um dos seguintes: `char`, um tipo inteiro assinado ou um tipo inteiro não assinado (excluindo `bool` e os tipos inteiros de precisão de bit) (desde C23). É definido pela implementação qual tipo é compatível com qualquer tipo enumerado dado, mas seja qual for, ele deve ser capaz de representar todos os valores enumeradores dessa enumeração. Para todas as enumerações com um tipo subjacente fixo, o tipo enumerado é compatível com o tipo subjacente da enumeração. (desde C23)

O tipo de membro da enumeração para um tipo enumerado sem tipo subjacente fixo após a conclusão é:

* int se todos os valores da enumeração forem representáveis como um int; ou,
* o tipo enumerado.

| (desde C23)
Todas as enumerações têm um tipo subjacente. O tipo subjacente pode ser explicitamente especificado usando um `enum-type-specifier` e é seu tipo subjacente fixo. Se não for explicitamente especificado, o tipo subjacente é o tipo compatível da enumeração, que é um tipo inteiro assinado ou não assinado, ou `char`. | (desde C23)

Tipos enumerados são tipos inteiros e, como tal, podem ser usados em qualquer lugar onde outros tipos inteiros podem ser usados, incluindo em [conversões implícitas](<#/doc/language/conversion>) e [operadores aritméticos](<#/doc/language/operator_arithmetic>).
```c
    enum { ONE = 1, TWO } e;
    long n = ONE; // promoção
    double d = ONE; // conversão
    e = 1.2; // conversão, e agora é ONE
    e = e + 1; // e agora é TWO
```

### Notas

Ao contrário de [struct](<#/doc/language/struct>) ou [union](<#/doc/language/union>), não existem enums forward-declarados em C:
```c
    enum Color; // Erro: não há forward-declarations para enums em C
    enum Color { RED, GREEN, BLUE };
```

Enumerações permitem a declaração de constantes nomeadas de uma forma mais conveniente e estruturada do que o `#define`; elas são visíveis no depurador, obedecem às regras de escopo e participam do sistema de tipos.
```c
    #define TEN 10
    struct S { int x : TEN; }; // OK
```

ou
```c
    enum { TEN = 10 };
    struct S { int x : TEN; }; // também OK
```

Desde C23, [constexpr](<#/doc/language/constexpr>) pode ser usado para o mesmo propósito:
```c
    constexpr int TEN = 10;
    struct S { int x : TEN; }; // também OK
```

Além disso, como uma [struct](<#/doc/language/struct>) ou [union](<#/doc/language/union>) não estabelece seu escopo em C, um tipo de enumeração e suas constantes de enumeração podem ser introduzidos na especificação de membro da primeira, e seu escopo é o mesmo da primeira, posteriormente.
```c
    struct Element
    {
        int z;
        enum State { SOLID, LIQUID, GAS, PLASMA } state;
    } oxygen = { 8, GAS };
    
    // o tipo enum State e suas constantes de enumeração permanecem visíveis aqui, por exemplo.
    void foo(void)
    {
        enum State e = LIQUID; // OK
        printf("%d %d %d ", e, oxygen.state, PLASMA); // imprime 1 2 3
    }
```

### Exemplo

Execute este código
```c
    #include <stdio.h>
    
    int main(void)
    {
        enum TV { FOX = 11, CNN = 25, ESPN = 15, HBO = 22, MAX = 30, NBC = 32 };
    
        printf("List of cable stations:\n");
        printf(" FOX: \t%2d\n", FOX);
        printf(" HBO: \t%2d\n", HBO);
        printf(" MAX: \t%2d\n", MAX);
    }
```

Saída:
```
    List of cable stations:
     FOX:   11
     HBO:   22
     MAX:   30
```

### Referências

* Padrão C23 (ISO/IEC 9899:2024):

* 6.2.5/21 Tipos (p: 39)

* 6.7.2.2 Especificadores de enumeração (p: 107-112)

* Padrão C17 (ISO/IEC 9899:2018):

* 6.2.5/16 Tipos (p: 32)

* 6.7.2.2 Especificadores de enumeração (p: 84-85)

* Padrão C11 (ISO/IEC 9899:2011):

* 6.2.5/16 Tipos (p: 41)

* 6.7.2.2 Especificadores de enumeração (p: 117-118)

* Padrão C99 (ISO/IEC 9899:1999):

* 6.2.5/16 Tipos (p: 35)

* 6.7.2.2 Especificadores de enumeração (p: 105-106)

* Padrão C89/C90 (ISO/IEC 9899:1990):

* 3.1.2.5 Tipos

* 3.5.2.2 Especificadores de enumeração

### Palavras-chave

[`enum`](<#/doc/keyword/enum>)

### Veja também

[Documentação C++](<#/>) para declaração de enumeração