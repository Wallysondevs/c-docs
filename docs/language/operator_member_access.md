# Operadores de acesso a membros

Os operadores de acesso a membros permitem o acesso aos membros de seus operandos.

Operador | Nome do operador | Exemplo | Descrição
[] | subscrito de array | a[b] | acessa o **b**-ésimo elemento do array **a**
* | desreferência de ponteiro | *a | desreferencia o ponteiro **a** para acessar o objeto ou função ao qual ele se refere
& | endereço de | &a | cria um ponteiro que se refere ao objeto ou função **a**
. | acesso a membro | a.b | acessa o membro **b** da [struct](<#/doc/language/struct>) ou [union](<#/doc/language/union>) **a**
-> | acesso a membro via ponteiro | a->b | acessa o membro **b** da [struct](<#/doc/language/struct>) ou [union](<#/doc/language/union>) apontada por **a**

### Subscrito

A expressão de subscrito de array tem a forma

---
pointer-expression `[` integer-expression `]` | (1) |
integer-expression `[` pointer-expression `]` | (2) |

onde

- **pointer-expression** — uma [expressão](<#/doc/language/expressions>) do tipo ponteiro para objeto completo
- **integer-expression** — uma [expressão](<#/doc/language/expressions>) de tipo inteiro

A expressão do operador de subscrito é uma [expressão lvalue](<#/doc/language/value_category>) cujo tipo é o tipo do objeto apontado pela expressão-ponteiro.

Por definição, o operador de subscrito E1[E2] é exatamente idêntico a *((E1)+(E2)). Se a expressão-ponteiro for uma expressão de array, ela passa por [conversão de lvalue para rvalue](<#/doc/language/conversion>) e se torna um ponteiro para o primeiro elemento do array.

Devido à definição da [adição entre um ponteiro e um inteiro](<#/doc/language/operator_arithmetic>), o resultado é o elemento do array com o índice igual ao resultado da expressão-inteira (ou, se a expressão-ponteiro estava apontando para o i-ésimo elemento de algum array, o índice do resultado é i mais o resultado da expressão-inteira)

Nota: veja [array](<#/doc/language/array>) para detalhes sobre arrays multidimensionais.

Execute este código
```c
    #include <stdio.h>
    int main(void)
    {
        int a[3] = {1,2,3};
        printf("%d %d\n", a[2],  // n == 3
                          2[a]); // same, n == 3
        a[2] = 7; // subscripts are lvalues
    
        int n[2][3] = {{1,2,3},{4,5,6}};
        int (*p)[3] = &n[1]; // elements of n are arrays
        printf("%d %d %d\n", (*p)[0], p[0][1], p[0][2]); // access n[1][] via p
        int x = n[1][2]; // applying [] again to the array n[1]
        printf("%d\n", x);
    
        printf("%c %c\n", "abc"[2], 2["abc"]); // string literals are arrays too
    }
```

Saída:
```
    3 3
    4 5 6
    6
    c c
```

### Desreferência

A expressão de _desreferência_ ou _indireção_ tem a forma

---
`*` pointer-expression

onde

- **pointer-expression** — uma [expressão](<#/doc/language/expressions>) de qualquer tipo de ponteiro

Se a expressão-ponteiro for um ponteiro para função, o resultado do operador de desreferência é um designador de função para essa função.

Se a expressão-ponteiro for um ponteiro para objeto, o resultado é uma [expressão lvalue](<#/doc/language/value_category>) que designa o objeto apontado.

Desreferenciar um ponteiro nulo, um ponteiro para um objeto fora de sua vida útil (um ponteiro pendente), um ponteiro desalinhado ou um ponteiro com valor indeterminado é [comportamento indefinido](<#/>), exceto quando o operador de desreferência é anulado pela aplicação do operador de endereço ao seu resultado, como em &*E.

Execute este código
```c
    #include <stdio.h>
    int main(void)
    {
        int n = 1;
        int* p = &n;
        printf("*p = %d\n", *p); // the value of *p is what's stored in n
        *p = 7; // *p is lvalue
        printf("*p = %d\n", *p);
    }
```

Saída:
```
    *p = 1
    *p = 7
```

### Endereço de

A expressão de endereço tem a forma

---
`&` function | (1) |
`&` lvalue-expression | (2) |
`&` `*` expression | (3) |
`&` expression `[` expression `]` | (4) |

1) endereço de uma função

2) endereço de um objeto

3) caso especial: `&` e `*` se cancelam, nenhum é avaliado

4) caso especial: `&` e o `*` implícito em `[]` se cancelam, apenas a adição implícita em `[]` é avaliada.

onde

- **lvalue-expression** — uma [expressão lvalue](<#/doc/language/value_category>) de qualquer tipo que não seja um [bit-field](<#/doc/language/bit_field>) e não tenha classe de armazenamento [register](<#/doc/language/storage_duration>)

O operador de endereço produz o endereço [não-lvalue](<#/doc/language/value_category>) de seu operando, adequado para inicializar um ponteiro para o tipo do operando. Se o operando for um designador de função (1), o resultado é um ponteiro para função. Se o operando for um objeto (2), o resultado é um ponteiro para objeto.

Se o operando for o operador de desreferência, nenhuma ação é tomada (portanto, é aceitável aplicar &* a um ponteiro nulo), exceto que o resultado não é um lvalue.

Se o operando for uma expressão de índice de array, nenhuma ação é tomada além da conversão de array para ponteiro e da adição, então &a[N] é válido para um array de tamanho N (obter um ponteiro um após o final é aceitável, desreferenciá-lo não é, mas a desreferência se cancela nesta expressão).

Execute este código
```c
    int f(char c) { return c;}
    int main(void)
    {
       int n = 1;
       int *p = &n; // address of object n
       int (*fp)(char) = &f; // address of function f
       int a[3] = {1,2,3};
       int *beg=a, *end=&a[3]; // same as end = a+3
    }
```

### Acesso a membro

A expressão de acesso a membro tem a forma

---
expression `.` member-name

onde

- **expression** — uma expressão do tipo [struct](<#/doc/language/struct>) ou [union](<#/doc/language/union>)
- **member-name** — um [identificador](<#/doc/language/identifier>) que nomeia um membro da struct ou union designada pela expressão

A expressão de acesso a membro designa o membro nomeado da [struct](<#/doc/language/struct>) ou [union](<#/doc/language/union>) designada por seu operando esquerdo. Ela tem a mesma [categoria de valor](<#/doc/language/value_category>) que seu operando esquerdo.

Se o operando esquerdo for qualificado como [const](<#/doc/language/const>) ou [volatile](<#/doc/language/volatile>), o resultado também é qualificado. Se o operando esquerdo for [atomic](<#/doc/language/atomic>), o comportamento é indefinido.

Nota: além de identificadores que nomeiam objetos do tipo struct ou union, as seguintes expressões podem ter tipos struct ou union: [atribuição](<#/doc/language/operator_assignment>), [chamada de função](<#/doc/language/operator_other>), [operador vírgula](<#/doc/language/operator_other>), [operador condicional](<#/doc/language/operator_other>) e [literal composto](<#/doc/language/compound_literal>).

Execute este código
```c
    #include <stdio.h>
    struct s {int x;};
    struct s f(void) { return (struct s){1}; }
    int main(void)
    {
        struct s s;
        s.x = 1; // ok, changes the member of s
        int n = f().x; // f() is an expression of type struct s
    //  f().x = 1; // Error: this member access expression is not an lvalue
    
        const struct s sc;
    //  sc.x = 3;  // Error: sc.x is const, can't be assigned
    
        union { int x; double d; } u = {1};
        u.d = 0.1; // changes the active member of the union
    }
```

### Acesso a membro via ponteiro

A expressão de acesso a membro tem a forma

---
expression `- >` member-name

onde

- **expression** — uma expressão do tipo [ponteiro](<#/doc/language/pointer>) para [struct](<#/doc/language/struct>) ou [union](<#/doc/language/union>)
- **member-name** — um [identificador](<#/doc/language/identifier>) que nomeia um membro da struct ou union apontada pela expressão

A expressão de acesso a membro via ponteiro designa o membro nomeado da [struct](<#/doc/language/struct>) ou [union](<#/doc/language/union>) apontada por seu operando esquerdo. Sua categoria de valor é sempre [lvalue](<#/doc/language/value_category>)

Se o tipo apontado pelo operando esquerdo for qualificado como [const](<#/doc/language/const>) ou [volatile](<#/doc/language/volatile>), o resultado também é qualificado. Se o tipo apontado pelo operando esquerdo for [atomic](<#/doc/language/atomic>), o comportamento é indefinido.

Execute este código
```c
    #include <stdio.h>
    struct s {int x;};
    int main(void)
    {
        struct s s={1}, *p = &s;
        p->x = 7; // changes the value of s.x through the pointer
        printf("%d\n", p->x); // prints 7
    }
```

### Relatórios de defeito

Os seguintes relatórios de defeito que alteram o comportamento foram aplicados retroativamente a padrões C publicados anteriormente.

DR | Aplicado a | Comportamento conforme publicado | Comportamento correto
[DR 076](<https://www.open-std.org/jtc1/sc22/wg14/www/docs/dr_076.html>) | C89 | indireção desnecessária não podia ser cancelada por `&` | tornou-se cancelável

### Referências

*   Padrão C17 (ISO/IEC 9899:2018):
    *   6.5.2.1 Subscrito de array (p: 57-58)
    *   6.5.2.3 Membros de struct e union (p: 58-59)
    *   6.5.3.2 Operadores de endereço e indireção (p: 59-61)
*   Padrão C11 (ISO/IEC 9899:2011):
    *   6.5.2.1 Subscrito de array (p: 80)
    *   6.5.2.3 Membros de struct e union (p: 82-84)
    *   6.5.3.2 Operadores de endereço e indireção (p: 88-89)
*   Padrão C99 (ISO/IEC 9899:1999):
    *   6.5.2.1 Subscrito de array (p: 70)
    *   6.5.2.3 Membros de struct e union (p: 72-74)
    *   6.5.3.2 Operadores de endereço e indireção (p: 78-79)
*   Padrão C89/C90 (ISO/IEC 9899:1990):
    *   3.3.2.1 Subscrito de array
    *   3.3.2.3 Membros de struct e union
    *   3.3.3.2 Operadores de endereço e indireção

### Veja também

*   [Precedência de operadores](<#/doc/language/operator_precedence>)

Operadores comuns
---
[atribuição](<#/doc/language/operator_assignment>) | [incremento
decremento](<#/doc/language/operator_incdec>) | [aritméticos](<#/doc/language/operator_arithmetic>) | [lógicos](<#/doc/language/operator_logical>) | [comparação](<#/doc/language/operator_comparison>) | **acesso a
membro** | [outros](<#/doc/language/operator_other>)
a = b
a += b
a -= b
a *= b
a /= b
a %= b
a &= b
a |= b
a ^= b
a <<= b
a >>= b | ++a
--a
a++
a-- | +a
-a
a + b
a - b
a * b
a / b
a % b
~a
a & b
a | b
a ^ b
a << b
a >> b | !a
a && b
a || b | a == b
a != b
a < b
a > b
a <= b
a >= b | a[b]
*a
&a
a->b
a.b | a(...)
a, b
(type) a
a ? b : c
sizeof

_Alignof
(desde C11)
(até C23)

alignof
(desde C23)
[Documentação C++](<#/>) para operadores de acesso a membros