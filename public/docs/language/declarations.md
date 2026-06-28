# Declarações

Uma _declaração_ é uma construção da linguagem C que introduz um ou mais [identificadores](<#/doc/language/identifier>) no programa e especifica seu significado e propriedades.

Declarações podem aparecer em qualquer escopo. Cada declaração termina com um ponto e vírgula (assim como [uma instrução](<#/doc/language/statements>)) e consiste em duas(até C23)três(desde C23) partes distintas:

---
specifiers-and-qualifiers declarators-and-initializers ﻿(opcional) `;` | (1) |
attr-spec-seq specifiers-and-qualifiers declarators-and-initializers `;` | (2) | (desde C23)
attr-spec-seq `;` | (3) | (desde C23)

onde

- **specifiers-and-qualifiers** — lista separada por espaços em branco de, em qualquer ordem,
* especificadores de tipo:
  * void
  * o nome de um [tipo aritmético](<#/doc/language/arithmetic_types>)
  * o nome de um [tipo atômico](<#/doc/language/atomic>)
  * um nome introduzido anteriormente por uma declaração [typedef](<#/doc/language/typedef>)
  * especificador [`struct`](<#/doc/language/struct>), [`union`](<#/doc/language/union>), ou [`enum`](<#/doc/language/enum>)
  * um especificador [typeof](<#/doc/language/typeof_unqual>) (desde C23)
* zero ou um especificador de classe de armazenamento: [`typedef`](<#/doc/language/typedef>), [`constexpr`](<#/doc/language/constexpr>), [`auto`](<#/doc/language/auto>), [register, static, extern, `_Thread_local`](<#/doc/language/storage_duration>)
* zero ou mais qualificadores de tipo: [`const`](<#/doc/language/const>), [`volatile`](<#/doc/language/volatile>), [`restrict`](<#/doc/language/restrict>), [`_Atomic`](<#/doc/language/atomic>)
* (somente ao declarar funções), zero ou mais especificadores de função: [`inline`](<#/doc/language/inline>), [`_Noreturn`](<#/doc/language/_Noreturn>)
* zero ou mais especificadores de alinhamento: [`_Alignas`](<#/doc/language/alignas>)(desde C11)(até C23)[`alignas`](<#/doc/language/alignas>)(desde C23)

- **declarators-and-initializers** — lista de declaradores separados por vírgulas (cada declarador fornece informações de tipo adicionais e/ou o identificador a ser declarado). Declaradores podem ser acompanhados por [inicializadores](<#/doc/language/initialization>). As declarações [enum](<#/doc/language/enum>), [struct](<#/doc/language/struct>) e [union](<#/doc/language/union>) podem omitir declaradores, caso em que elas apenas introduzem as constantes de enumeração e/ou tags.
- **attr-spec-seq** — (C23)lista opcional de [atributos](<#/doc/language/attributes>), aplicados às entidades declaradas, ou forma uma declaração de atributo se aparecer sozinha.

1,2) Declaração simples. Introduz um ou mais identificadores que denotam objetos, funções, tags de struct/union/enum, typedefs ou constantes de enumeração.

3) Declaração de atributo. Não declara nenhum identificador e tem significado definido pela implementação se o significado não for especificado pelo padrão.

Por exemplo,
```c
    int a, *b=NULL; // "int" é o especificador de tipo,
                    // "a" é um declarador
                    // "*b" é um declarador e NULL é seu inicializador
    const int *f(void); // "int" é o especificador de tipo
                        // "const" é o qualificador de tipo
                        // "*f(void)" é o declarador
    enum COLOR {RED, GREEN, BLUE} c; // "enum COLOR {RED, GREEN, BLUE}" é o especificador de tipo
                                     // "c" é o declarador
```

O tipo de cada identificador introduzido em uma declaração é determinado por uma combinação do tipo especificado pelo especificador de tipo e as modificações de tipo aplicadas por seu declarador. O tipo de uma variável também pode ser inferido se o especificador `auto` for usado.(desde C23)

[Atributos](<#/doc/language/attributes>)(desde C23) podem aparecer em `specifiers-and-qualifiers`, caso em que se aplicam ao tipo determinado pelos especificadores precedentes.

### Declaradores
Cada declarador é um dos seguintes:

---
identifier attr-spec-seq ﻿(opcional) | (1) |
`(` declarator `)` | (2) |
`*` attr-spec-seq ﻿(opcional) qualifiers ﻿(opcional) declarator | (3) |
noptr-declarator `[` `static`(opcional) qualifiers ﻿(opcional) expression `]` noptr-declarator `[` qualifiers ﻿(opcional) `*` `]` | (4) |
noptr-declarator `(` parameters-or-identifiers `)` | (5) |

1) o identificador que este declarador introduz.

2) qualquer declarador pode ser envolto em parênteses; isso é necessário para introduzir ponteiros para arrays e ponteiros para funções.

3) [declarador de ponteiro](<#/doc/language/pointer>): a declaração `S * cvr D;` declara `D` como um ponteiro cvr-qualificado para o tipo determinado por `S`.

4) [declarador de array](<#/doc/language/array>): a declaração `S D[N]` declara `D` como um array de `N` objetos do tipo determinado por `S`. `noptr-declarator` é qualquer outro declarador, exceto um declarador de ponteiro não-parentesizado.

5) [declarador de função](<#/doc/language/function_declaration>): a declaração `S D(params)` declara `D` como uma função que recebe os parâmetros `params` e retorna `S`. `noptr-declarator` é qualquer outro declarador, exceto um declarador de ponteiro não-parentesizado.

O raciocínio por trás dessa sintaxe é que, quando o identificador declarado pelo declarador aparece em uma expressão da mesma forma que o declarador, ele teria o tipo especificado pela sequência de especificadores de tipo.
```c
    struct C
    {
        int member; // "int" é o especificador de tipo
                    // "member" é o declarador
    } obj, *pObj = &obj;
    // "struct C { int member; }" é o especificador de tipo
    // o declarador "obj" define um objeto do tipo struct C
    // o declarador "*pObj" declara um ponteiro para C,
    // o inicializador "= &obj" fornece o valor inicial para esse ponteiro
    
    int a = 1, *p = NULL, f(void), (*pf)(double);
    // o especificador de tipo é "int"
    // o declarador "a" define um objeto do tipo int
    //   o inicializador "=1" fornece seu valor inicial
    // o declarador "*p" define um objeto do tipo ponteiro para int
    //   o inicializador "=NULL" fornece seu valor inicial
    // o declarador "f(void)" declara uma função que recebe void e retorna int
    // o declarador "(*pf)(double)" define um objeto do tipo ponteiro
    //   para função que recebe double e retorna int
    
    int (*(*foo)(double))[3] = NULL;
    // o especificador de tipo é int
    // 1. o declarador "(*(*foo)(double))[3]" é um declarador de array:
    //    o tipo declarado é "/declarador aninhado/ array de 3 int"
    // 2. o declarador aninhado é "*(*foo)(double))", que é um declarador de ponteiro
    //    o tipo declarado é "/declarador aninhado/ ponteiro para array de 3 int"
    // 3. o declarador aninhado é "(*foo)(double)", que é um declarador de função
    //    o tipo declarado é "/declarador aninhado/ função que recebe double e retorna
    //        ponteiro para array de 3 int"
    // 4. o declarador aninhado é "(*foo)" que é um declarador de ponteiro (entre parênteses,
    //        conforme exigido pela sintaxe do declarador de função).
    //    o tipo declarado é "/declarador aninhado/ ponteiro para função que recebe double
    //        e retorna ponteiro para array de 3 int"
    // 5. o declarador aninhado é "foo", que é um identificador.
    // A declaração introduz o identificador "foo" para se referir a um objeto do tipo
    // "ponteiro para função que recebe double e retorna ponteiro para array de 3 int"
    // O inicializador "= NULL" fornece o valor inicial deste ponteiro.
    
    // Se "foo" for usado em uma expressão da forma do declarador, seu tipo seria
    // int.
    int x = (*(*foo)(1.2))[0];
```

O final de cada declarador que não faz parte de outro declarador é um [ponto de sequência](<#/doc/language/eval_order>).

Em todos os casos, `attr-spec-seq` é uma sequência opcional de [atributos](<#/doc/language/attributes>)(desde C23). Quando aparece imediatamente após o identificador, aplica-se ao objeto ou função que está sendo declarado.

### Definições
Uma _definição_ é uma declaração que fornece todas as informações sobre os identificadores que ela declara.

Toda declaração de um [enum](<#/doc/language/enum>) ou um [typedef](<#/doc/language/typedef>) é uma definição.

Para funções, uma declaração que inclui o corpo da função é uma [definição de função](<#/doc/language/function_definition>):
```c
    int foo(double); // declaração
    int foo(double x) { return x; } // definição
```

Para objetos, uma declaração que aloca armazenamento ([automático ou estático](<#/doc/language/storage_duration>), mas não `extern`) é uma definição, enquanto uma declaração que não aloca armazenamento ([declaração externa](<#/doc/language/extern>)) não é.
```c
    extern int n; // declaração
    int n = 10; // definição
```

Para [structs](<#/doc/language/struct>) e [unions](<#/doc/language/union>), declarações que especificam a lista de membros são definições:
```c
    struct X; // declaração
    struct X { int n; }; // definição
```

### Redeclaração
Uma declaração não pode introduzir um identificador se outra declaração para o mesmo identificador no mesmo [escopo](<#/doc/language/scope>) aparecer anteriormente, exceto que
* Declarações de objetos [com ligação](<#/doc/language/storage_duration>) (externa ou interna) podem ser repetidas:

```c
    extern int x;
    int x = 10; // OK
    extern int x; // OK
    
    static int n;
    static int n = 10; // OK
    static int n; // OK
```

* [typedef](<#/doc/language/typedef>) não-VLA pode ser repetido desde que nomeie o mesmo tipo:

```c
    typedef int int_t;
    typedef int int_t; // OK
```

* Declarações de [struct](<#/doc/language/struct>) e [union](<#/doc/language/union>) podem ser repetidas:

```c
    struct X;
    struct X { int n; };
    struct X;
```

Essas regras simplificam o uso de arquivos de cabeçalho.

### Notas
Em C89, declarações dentro de qualquer [instrução composta](<#/doc/language/statements>) (escopo de bloco) devem aparecer no início do bloco, antes de quaisquer [instruções](<#/doc/language/statements>). Além disso, em C89, funções que retornam `int` podem ser implicitamente declaradas pelo [operador de chamada de função](<#/doc/language/operator_other>) e parâmetros de função do tipo `int` não precisam ser declarados ao usar [definições de função](<#/doc/language/function_definition>) de estilo antigo. | (até C99)

Declaradores vazios são proibidos; uma declaração simples deve ter pelo menos um declarador ou declarar pelo menos uma tag de struct/union/enum, ou introduzir pelo menos uma constante de enumeração.

Se qualquer parte de um declarador for um declarador de [array de tamanho variável](<#/doc/language/array>) (VLA), o tipo completo do declarador é conhecido como "tipo variably-modified". Tipos definidos a partir de tipos variably-modified também são variably modified (VM). Declarações de quaisquer tipos variably-modified podem aparecer apenas no [escopo de bloco](<#/doc/language/scope>) ou no escopo de protótipo de função e não podem ser membros de structs ou unions. Embora VLA só possa ter [duração de armazenamento](<#/doc/language/storage_duration>) automática ou alocada, um tipo VM como um ponteiro para um VLA pode ser `static`. Existem outras restrições no uso de tipos VM, veja [goto](<#/doc/language/goto>), [switch](<#/doc/language/switch>). [longjmp](<#/doc/program/longjmp>) | (desde C99)
[static_asserts](<#/doc/language/static_assert>) são consideradas declarações do ponto de vista da gramática C (para que possam aparecer onde uma declaração pode aparecer), mas não introduzem nenhum identificador e não seguem a sintaxe de declaração. | (desde C11)
Declarações de [atributo](<#/doc/language/attributes>) também são consideradas declarações (para que possam aparecer onde uma declaração pode aparecer), mas não introduzem nenhum identificador. Um único `;` sem `attr-spec-seq` não é uma declaração de atributo, mas uma instrução. | (desde C23)

### Referências
* Padrão C23 (ISO/IEC 9899:2024):
  * 6.7 Declarations (p: TBD)
* Padrão C17 (ISO/IEC 9899:2018):
  * 6.7 Declarations (p: 78-105)
* Padrão C11 (ISO/IEC 9899:2011):
  * 6.7 Declarations (p: 108-145)
* Padrão C99 (ISO/IEC 9899:1999):
  * 6.7 Declarations (p: 97-130)
* Padrão C89/C90 (ISO/IEC 9899:1990):
  * 3.5 Declarations

### Veja também
[Documentação C++](<#/>) para Declarações