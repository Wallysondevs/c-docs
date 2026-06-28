# Declaração de struct

Uma struct é um tipo que consiste em uma sequência de membros cujo armazenamento é alocado em uma sequência ordenada (em oposição a union, que é um tipo que consiste em uma sequência de membros cujo armazenamento se sobrepõe).

O [especificador de tipo](<#/doc/language/declarations>) para uma struct é idêntico ao especificador de tipo de [`union`](<#/doc/language/union>), exceto pela palavra-chave utilizada:

### Sintaxe

---
`struct` attr-spec-seq ﻿(optional) name ﻿(optional) `{` struct-declaration-list `}` | (1) |
`struct` attr-spec-seq ﻿(optional) name | (2) |

1) Definição de struct: introduz o novo tipo struct name e define seu significado

2) Se usado em uma linha própria, como em `struct` name `;`, _declara_ mas não define a struct `name` (veja declaração antecipada abaixo). Em outros contextos, nomeia a struct previamente declarada, e attr-spec-seq não é permitido.

- **name** — o nome da struct que está sendo definida
- **struct-declaration-list** — qualquer número de declarações de variáveis, declarações de [bit-field](<#/doc/language/bit_field>) e declarações de [static assert](<#/doc/language/static_assert>). Membros de tipo incompleto e membros de tipo função não são permitidos (exceto para o membro de array flexível descrito abaixo)
- **attr-spec-seq** — (C23) lista opcional de [atributos](<#/doc/language/attributes>), aplicada ao tipo struct

### Explicação

Dentro de um objeto struct, os endereços de seus elementos (e os endereços das unidades de alocação de bit-field) aumentam na ordem em que os membros foram definidos. Um ponteiro para uma struct pode ser convertido para um ponteiro para seu primeiro membro (ou, se o membro for um bit-field, para sua unidade de alocação). Da mesma forma, um ponteiro para o primeiro membro de uma struct pode ser convertido para um ponteiro para a struct que o contém. Pode haver preenchimento (padding) sem nome entre quaisquer dois membros de uma struct ou após o último membro, mas não antes do primeiro membro. O tamanho de uma struct é pelo menos tão grande quanto a soma dos tamanhos de seus membros.

Se uma struct define pelo menos um membro nomeado, é permitido declarar adicionalmente seu último membro com tipo de array incompleto. Quando um elemento do membro de array flexível é acessado (em uma expressão que usa o operador `.` ou `- >` com o nome do membro de array flexível como operando do lado direito), então a struct se comporta como se o membro de array tivesse o maior tamanho que coubesse na memória alocada para este objeto. Se nenhum armazenamento adicional foi alocado, ela se comporta como se fosse um array com 1 elemento, exceto que o comportamento é indefinido se esse elemento for acessado ou se um ponteiro para uma posição além desse elemento for produzido. A inicialização e o operador de atribuição ignoram o membro de array flexível. sizeof o omite, mas pode ter mais preenchimento final do que a omissão implicaria. Estruturas com membros de array flexíveis (ou unions que possuem um membro de estrutura recursivo-possivelmente com membro de array flexível) não podem aparecer como elementos de array ou como membros de outras estruturas.
```c
    struct s { int n; double d[]; }; // s.d is a flexible array member
     
    struct s t1 = { 0 };          // OK, d is as if double d[1], but UB to access
    struct s t2 = { 1, { 4.2 } }; // error: initialization ignores flexible array
     
    // if sizeof (double) == 8
    struct s *s1 = malloc(sizeof (struct s) + 64); // as if d was double d[8]
    struct s *s2 = malloc(sizeof (struct s) + 40); // as if d was double d[5]
     
    s1 = malloc(sizeof (struct s) + 10); // now as if d was double d[1]. Two bytes excess.
    double *dp = &(s1->d[0]);    // OK
    *dp = 42;                    // OK
    s1->d[1]++;                  // Undefined behavior. 2 excess bytes can't be accessed
                                 // as double.
     
    s2 = malloc(sizeof (struct s) + 6);  // same, but UB to access because 2 bytes are
                                         // missing to complete 1 double
    dp = &(s2->d[0]);            // OK, can take address just fine
    *dp = 42;                    // undefined behavior
     
    *s1 = *s2; // only copies s.n, not any element of s.d
               // except those caught in sizeof (struct s)
```

| (desde C99)
Similar a union, um membro sem nome de uma struct cujo tipo é uma struct sem nome é conhecido como _struct anônima_. Cada membro de uma struct anônima é considerado um membro da struct ou union que o contém, mantendo seu layout de estrutura. Isso se aplica recursivamente se a struct ou union que o contém também for anônima.
```c
    struct v
    {
       union // anonymous union
       {
          struct { int i, j; }; // anonymous structure
          struct { long k, l; } w;
       };
       int m;
    } v1;
     
    v1.i = 2;   // valid
    v1.k = 3;   // invalid: inner structure is not anonymous
    v1.w.k = 5; // valid
```

Similar a union, o comportamento do programa é indefinido se a struct for definida sem nenhum membro nomeado (incluindo aqueles obtidos via structs ou unions anônimas aninhadas). | (desde C11)

### Declaração antecipada

Uma declaração da seguinte forma

---
`struct` attr-spec-seq ﻿(optional) name `;`

oculta qualquer significado previamente declarado para o nome name no espaço de nomes de tags e declara name como um novo nome de struct no escopo atual, que será definido posteriormente. Até que a definição apareça, este nome de struct tem [tipo incompleto](<#/doc/language/compatible_type>).

Isso permite structs que se referem umas às outras:
```c
    struct y;
    struct x { struct y *p; /* ... */ };
    struct y { struct x *q; /* ... */ };
```

Note que um novo nome de struct também pode ser introduzido apenas usando uma tag struct dentro de outra declaração, mas se uma struct previamente declarada com o mesmo nome existir no [espaço de nomes](<#/doc/language/name_space>) de tags, a tag se referiria a esse nome
```c
    struct s* p = NULL; // tag naming an unknown struct declares it
    struct s { int a; }; // definition for the struct pointed to by p
    void g(void)
    {
        struct s; // forward declaration of a new, local struct s
                  // this hides global struct s until the end of this block
        struct s *p;  // pointer to local struct s
                      // without the forward declaration above,
                      // this would point at the file-scope s
        struct s { char* p; }; // definitions of the local struct s
    }
```

### Palavras-chave

[`struct`](<#/doc/keyword/struct>)

### Notas

Veja [inicialização de struct](<#/doc/language/struct_initialization>) para as regras relativas aos inicializadores para structs.

Como membros de tipo incompleto não são permitidos, e um tipo struct não está completo até o final da definição, uma struct não pode ter um membro de seu próprio tipo. Um ponteiro para seu próprio tipo é permitido e é comumente usado para implementar nós em listas encadeadas ou árvores.

Como uma declaração de struct não estabelece [escopo](<#/doc/language/scope>), tipos aninhados, enumerações e enumeradores introduzidos por declarações dentro de struct-declaration-list são visíveis no escopo circundante onde a struct é definida.

### Exemplo

Execute este código
```c
    #include <stddef.h>
    #include <stdio.h>
     
    int main(void)
    {
        // Declare the struct type.
        struct car
        {
            char* make;
            int year;
        };
        // Declare and initialize an object of a previously-declared struct type.
        struct car c = {.year = 1923, .make = "Nash"};
        printf("1) Car: %d %s\n", c.year, c.make);
     
        // Declare a struct type, an object of that type, and a pointer to it.
        struct spaceship
        {
            char* model;
            int max_speed;
        } ship = {"T-65 X-wing starfighter", 1050},
        *pship = &ship;
        printf("2) Spaceship: %s. Max speed: %d km/h\n\n", ship.model, ship.max_speed);
     
        // Address increase in order of definition. Padding may be inserted.
        struct A { char a; double b; char c; };
        printf(
            "3) Offset of char a = %zu\n"
            "4) Offset of double b = %zu\n"
            "5) Offset of char c = %zu\n"
            "6) Size of struct A = %zu\n\n",
            offsetof(struct A, a),
            offsetof(struct A, b),
            offsetof(struct A, c),
            sizeof(struct A)
        );
        struct B { char a; char b; double c; };
        printf(
            "7) Offset of char a = %zu\n"
            "8) Offset of char b = %zu\n"
            "9) Offset of double c = %zu\n"
            "A) Size of struct B = %zu\n\n",
            offsetof(struct B, a),
            offsetof(struct B, b),
            offsetof(struct B, c),
            sizeof(struct B)
        );
     
        // A pointer to a struct can be cast to a pointer
        // to its first member and vice versa.
        char** pmodel = (char **)pship;
        printf("B) %s\n", *pmodel);
        pship = (struct spaceship *)pmodel;
    }
```

Saída possível:
```
    1) Car: 1923 Nash
    2) Spaceship: T-65 X-wing starfighter. Max speed: 1050 km/h
     
    3) Offset of char a = 0
    4) Offset of double b = 8
    5) Offset of char c = 16
    6) Size of struct A = 24
     
    7) Offset of char a = 0
    8) Offset of char b = 1
    9) Offset of double c = 8
    A) Size of struct B = 16
     
    B) T-65 X-wing starfighter
```

### Relatórios de defeitos

Os seguintes relatórios de defeitos que alteram o comportamento foram aplicados retroativamente a padrões C publicados anteriormente.

DR | Aplicado a | Comportamento conforme publicado | Comportamento correto
[DR 499](<https://www.open-std.org/jtc1/sc22/wg14/www/docs/n2396.htm#dr_499>) | C11 | membros de structs/unions anônimas eram considerados membros da struct/union que os continha | eles mantêm seu layout de memória

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 6.7.2.1 Especificadores de estrutura e união (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 6.7.2.1 Especificadores de estrutura e união (p: 81-84)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 6.7.2.1 Especificadores de estrutura e união (p: 112-117)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 6.7.2.1 Especificadores de estrutura e união (p: 101-104)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 3.5.2.1 Especificadores de estrutura e união

### Veja também

  * [acesso a membros de struct e union](<#/doc/language/operator_member_access>)
  * [bit-field](<#/doc/language/bit_field>)
  * [inicialização de struct](<#/doc/language/struct_initialization>)

[Documentação C++](<#/>) para declaração de classe
---