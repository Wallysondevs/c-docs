# Outros operadores

Uma coleção de operadores que não se encaixam em nenhuma das outras categorias principais.

| Esta seção está incompleta
Razão: considerar um Sumário (ToC) mais genérico para esta e outras tabelas que cobrem múltiplos tópicos
Operador | Nome do operador | Exemplo | Descrição
(...) | [chamada de função](<#/doc/language/operator_other>) | f(...) | chama a função **f**(), com zero ou mais argumentos
, | [operador vírgula](<#/doc/language/operator_other>) | a, b | avalia a expressão **a**, descarta seu valor de retorno e completa quaisquer efeitos colaterais, então avalia a expressão **b**, retornando o tipo e o resultado desta avaliação
(type) | [conversão de tipo (cast)](<#/doc/language/cast>) | (type)a | converte o tipo de **a** para **type**
? : | [operador condicional](<#/doc/language/operator_other>) | a ? b : c | se **a** for logicamente verdadeiro (não avalia para zero), então avalia a expressão **b**, caso contrário avalia a expressão **c**
sizeof | [operador sizeof](<#/doc/language/sizeof>) | sizeof a | o tamanho em bytes de **a**
_Alignof
(desde C11) | [operador _Alignof](<#/doc/language/alignof>) | _Alignof(type) | o alinhamento requerido de **type**
typeof | [operadores typeof](<#/doc/language/typeof_unqual>) | typeof(a) | o tipo de **a**

### Chamada de função

A expressão de chamada de função tem a forma

---
expression `(` lista-de-argumentos ﻿(opcional) `)`
---

onde

- **expression** — qualquer expressão do tipo ponteiro para função (após [conversões lvalue](<#/doc/language/conversion>))
- **argument-list** — lista de expressões separadas por vírgulas (que não podem ser operadores vírgula) de qualquer tipo de objeto completo. Pode ser omitida ao chamar funções que não recebem argumentos.

O comportamento da expressão de chamada de função depende se o protótipo da função sendo chamada está [no escopo](<#/doc/language/scope>) no ponto da chamada.

#### Chamada para uma função com protótipo

1) O número de parâmetros deve ser igual ao número de argumentos (a menos que o parâmetro de reticências seja usado).

2) O tipo de cada parâmetro deve ser um tipo tal que exista uma [conversão implícita como se por atribuição](<#/doc/language/conversion>) que converta o tipo não qualificado do argumento correspondente para o tipo do parâmetro.

Além disso, para cada parâmetro de [tipo array](<#/doc/language/array>) que usa a palavra-chave `static` entre `[` e `]`, a expressão do argumento deve designar um ponteiro para o elemento de um array com pelo menos tantos elementos quanto especificado na expressão de tamanho do parâmetro. | (desde C99)

3) Os argumentos são avaliados [em ordem não especificada e sem sequenciamento](<#/doc/language/eval_order>).

4) A [atribuição](<#/doc/language/operator_assignment>) é realizada para copiar o valor de cada argumento para o parâmetro de função correspondente, ignorando quaisquer qualificadores de tipo no tipo do parâmetro e seus elementos ou membros possivelmente recursivos, se houver (nota: a função pode modificar seus parâmetros, e essas mudanças não afetam os argumentos; chamadas de função em C são apenas por valor).

* se houver um parâmetro de [reticências final](<#/doc/language/variadic>), [promoções de argumento padrão](<https://en.cppreference.com/mwiki/index.php?title=conversion&action=edit&redlink=1> "conversion \(page does not exist\)") são realizadas nos argumentos restantes, que são disponibilizados para va_list.

5) A função é executada, e o valor que ela retorna se torna o valor da expressão de chamada de função (se a função retornar void, a expressão de chamada de função é uma expressão void)
```c
    void f(char* p, int x) {}
    int main(void)
    {
        f("abc", 3.14); // array to pointer and float to int conversions
    }
```

#### Chamada para uma função sem protótipo

1) Os argumentos são avaliados [em ordem não especificada e sem sequenciamento](<#/doc/language/eval_order>). 2) [Promoções de argumento padrão](<#/doc/language/conversion>) são realizadas em cada expressão de argumento. 3) A [atribuição](<#/doc/language/operator_assignment>) é realizada para copiar o valor de cada argumento para o parâmetro de função correspondente, ignorando quaisquer qualificadores de tipo no tipo do parâmetro e seus elementos ou membros possivelmente recursivos, se houver. 4) A função é executada, e o valor que ela retorna se torna o valor da expressão de chamada de função (se a função retornar void, a expressão de chamada de função é uma expressão void)
```c
    void f(); // no prototype
    int main(void)
    {
        f(1, 1.0f); // UB unless f is defined to take an int and a double
    }
    void f(int a, double c) {}
```

O comportamento de uma chamada de função para uma função sem protótipo é comportamento indefinido se

* o número de argumentos não corresponde ao número de parâmetros.
* os tipos promovidos dos argumentos não são [compatíveis](<#/doc/language/compatible_type>) com os tipos promovidos dos parâmetros, exceto que

* versões signed e unsigned do mesmo tipo inteiro são consideradas compatíveis se o valor do argumento for representável por ambos os tipos.
* ponteiros para void e ponteiros para tipos de caractere (possivelmente cvr-qualificados) são considerados compatíveis

| (até C23)

#### Notas

As avaliações da expressão que designa a função a ser chamada e de todos os argumentos são [não sequenciadas](<#/doc/language/eval_order>) em relação umas às outras (mas há um ponto de sequência antes que o corpo da função comece a ser executado)
```c
    (*pf[f1()]) (f2(), f3() + f4()); // f1, f2, f3, f4 may be called in any order
```

Embora a chamada de função seja definida apenas para ponteiros para funções, ela funciona com designadores de função devido à [conversão implícita de função para ponteiro](<#/doc/language/conversion>).
```c
    int f(void) { return 1; }
    int (*pf)(void) = f;
    
    int main(void)
    {
        f();    // convert f to pointer, then call
        (&f)(); // create a pointer to function, then call
    
        pf();    // call the function
        (*pf)(); // obtain the function designator, convert to pointer, then calls
    
        (****f)(); // convert to pointer, obtain the function, repeat 4x, then call
        (****pf)(); // also OK
    }
```

Funções que ignoram argumentos não utilizados, como [printf](<#/doc/io/fprintf>), devem ser chamadas com um protótipo no escopo (o protótipo de tais funções necessariamente usa o parâmetro de [reticências final](<#/doc/language/variadic>)) para evitar invocar comportamento indefinido.

A redação atual do padrão sobre a semântica de preparação de parâmetros de função é defeituosa, porque especifica que os parâmetros são atribuídos a partir dos argumentos durante a chamada, o que rejeita incorretamente parâmetros ou tipos de membros qualificados com const, e aplica inadequadamente a semântica de volatile, que é inviável para parâmetros de função em muitas plataformas. Um relatório de defeito pós-C11 [DR427](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2396.htm#dr_427>) propôs a mudança de tal semântica de atribuição para inicialização, mas foi fechado como não sendo um defeito.

Uma expressão de chamada de função onde a expressão consiste inteiramente de um identificador e esse identificador não é declarado age como se o identificador fosse declarado como
```c
    extern int identifier(); // returns int and has no prototype
```

Assim, o seguinte programa completo é C89 válido:
```c
    main()
    {
        int n = atoi("123"); // implicitly declares atoi as int atoi()
    }
```

| (até C99)

### Operador vírgula

A expressão do operador vírgula tem a forma

---
lhs `,` rhs
---

onde

- **lhs** — qualquer expressão
- **rhs** — qualquer expressão que não seja outro operador vírgula (em outras palavras, a [associatividade](<#/doc/language/operator_precedence>) do operador vírgula é da esquerda para a direita)

Primeiro, o operando esquerdo, lhs, é avaliado e seu valor de resultado é descartado.

Em seguida, ocorre um [ponto de sequência](<#/doc/language/eval_order>), de modo que todos os efeitos colaterais de lhs sejam concluídos.

Em seguida, o operando direito, rhs, é avaliado e seu resultado é retornado pelo operador vírgula como um [não-lvalue](<#/doc/language/value_category>).

### Notas

O tipo de lhs pode ser void (ou seja, pode ser uma chamada para uma função que retorna void, ou pode ser uma expressão [convertida (cast)](<#/doc/language/cast>) para void)

O operador vírgula pode ser lvalue em C++, mas nunca em C

O operador vírgula pode retornar uma struct (as únicas outras expressões que retornam structs são literais compostos, chamadas de função, atribuições e o operador condicional)

Nos seguintes contextos, o operador vírgula não pode aparecer no nível superior de uma expressão porque a vírgula tem um significado diferente:

* lista de argumentos em uma chamada de função
* expressão inicializadora ou [lista de inicializadores](<#/doc/language/initialization>)
* [seleção genérica](<#/doc/language/generic>)

Se o operador vírgula precisar ser usado em tal contexto, ele deve ser colocado entre parênteses:
```c
    // int n = 2,3; // error, comma assumed to begin the next declarator
    // int a[2] = {1,2,3}; // error: more initializers than elements
    int n = (2,3), a[2] = {(1,2),3}; // OK
    
    f(a, (t=3, t+2), c); // OK, first, stores 3 in t, then calls f with three arguments
```

O operador vírgula de nível superior também é proibido em limites de array
```c
    // int a[2,3]; // error
    int a[(2,3)]; // OK, VLA array of size 3 (VLA because (2,3) is not a constant expression)
```

O operador vírgula não é permitido em [expressões constantes](<#/doc/language/constant_expression>), independentemente de estar no nível superior ou não
```c
    // static int n = (1,2); // Error: constant expression cannot call the comma operator
```

### Operador de conversão (cast)

Veja [operador de conversão (cast)](<#/doc/language/cast>)

### Operador condicional

A expressão do operador condicional tem a forma

---
condição `?` expressão-verdadeira `:` expressão-falsa
---

onde

- **condição** — uma expressão de tipo escalar
- **expression-true** — a expressão que será avaliada se condição for diferente de zero
- **expression-false** — a expressão que será avaliada se condição for igual a zero

Apenas as seguintes expressões são permitidas como expression-true e expression-false

* duas expressões de qualquer [tipo aritmético](<#/doc/language/arithmetic_types>)
* duas expressões do mesmo tipo [struct](<#/doc/language/struct>) ou [union](<#/doc/language/union>)
* duas expressões do tipo void
* duas expressões de tipo ponteiro, apontando para tipos que são [compatíveis](<#/doc/language/compatible_type>), ignorando qualificadores cvr

* duas expressões do tipo [nullptr_t](<#/doc/types/nullptr_t>) | (desde C23)

* uma expressão é um ponteiro e a outra é a constante de ponteiro nulo (como [NULL](<#/doc/types/NULL>)) ou um valor [nullptr_t](<#/doc/types/nullptr_t>) (desde C23)
* uma expressão é um ponteiro para objeto e a outra é um ponteiro para void (possivelmente qualificado)

1) Primeiro, avalia condição. Há um [ponto de sequência](<#/doc/language/eval_order>) após esta avaliação.

2) Se o resultado de condição for diferente de zero, executa expression-true, caso contrário executa expression-false

3) Realiza uma [conversão](<#/doc/language/conversion>) do resultado da avaliação para o _tipo comum_, definido como segue:

1) se as expressões tiverem tipo aritmético, o tipo comum é o tipo após [conversões aritméticas usuais](<#/doc/language/conversion>)

2) se as expressões tiverem tipo struct/union, o tipo comum é esse tipo struct/union

3) se ambas as expressões forem void, a expressão completa do operador condicional é uma expressão void

4) se um for um ponteiro e o outro for a constante de ponteiro nulo ou um valor [nullptr_t](<#/doc/types/nullptr_t>) (desde C23), o tipo é o tipo desse ponteiro

5) se ambos forem ponteiros, o resultado é o ponteiro para o tipo que combina os qualificadores cvr de ambos os tipos apontados (ou seja, se um for const int* e o outro for volatile int*, o resultado é const volatile int*), e se os tipos forem diferentes, o tipo apontado é o [tipo composto](<#/doc/language/types>).

6) se um for um ponteiro para void, o resultado é um ponteiro para void com qualificadores cvr combinados

7) se ambos tiverem o tipo [nullptr_t](<#/doc/types/nullptr_t>), o tipo comum também é [nullptr_t](<#/doc/types/nullptr_t>) | (desde C23)
```c
    #define ICE(x) (sizeof(*(1 ? ((void*)((x) * 0l)) : (int*)1)))
    
    // if x is an Integer Constant Expression then macro expands to
    
    sizeof(*(1 ? NULL : (int *) 1))  // (void *)((x)*0l)) -> NULL
    
    // according to point (4) this further converts into
    
    sizeof(int)
    
    // if x is not an Integer Constant Expression then macro expands to
    // according to point (6)
    
    (sizeof(*(void *)(x))           // Error due incomplete type
```

#### Notas

O operador condicional nunca é uma [expressão lvalue](<#/doc/language/value_category>), embora possa retornar objetos do tipo struct/union. As únicas outras expressões que podem retornar structs são [atribuição](<#/doc/language/operator_assignment>), [vírgula](<#/doc/language/operator_other>), [chamada de função](<#/doc/language/operator_other>) e [literal composto](<#/doc/language/compound_literal>).

Note que em C++, pode ser uma expressão lvalue.

Veja [precedência de operadores](<#/doc/language/operator_precedence>) para detalhes sobre a precedência relativa deste operador e da atribuição.

O operador condicional tem associatividade da direita para a esquerda, o que permite o encadeamento

Execute este código
```c
    #include <assert.h>
    
    enum vehicle { bus, airplane, train, car, horse, feet };
    
    enum vehicle choose(char arg)
    {
        return arg == 'B' ? bus      :
               arg == 'A' ? airplane :
               arg == 'T' ? train    :
               arg == 'C' ? car      :
               arg == 'H' ? horse    :
                            feet     ;
    }
    
    int main(void)
    {
        assert(choose('H') == horse && choose('F') == feet);
    }
```

### Operador `sizeof`

Veja [operador sizeof](<#/doc/language/sizeof>)

### Operador `_Alignof`

Veja [operador _Alignof](<#/doc/language/alignof>)

### Operadores `typeof`

Veja [operadores typeof](<#/doc/language/typeof_unqual>)

### Referências

* Padrão C23 (ISO/IEC 9899:2024):

* 6.5.2.2 Chamadas de função (p: TBD)

* 6.5.3.4 Os operadores sizeof e _Alignof (p: TBD)

* 6.5.4 Operadores de conversão (cast) (p: TBD)

* 6.5.15 Operador condicional (p: TBD)

* 6.5.17 Operador vírgula (p: TBD)

* 6.7.3.5 Especificadores typeof (p: 115-118)

* Padrão C17 (ISO/IEC 9899:2018):

* 6.5.2.2 Chamadas de função (p: 58-59)

* 6.5.3.4 Os operadores sizeof e _Alignof (p: 64-65)

* 6.5.4 Operadores de conversão (cast) (p: 65-66)

* 6.5.15 Operador condicional (p: 71-72)

* 6.5.17 Operador vírgula (p: 75)

* Padrão C11 (ISO/IEC 9899:2011):

* 6.5.2.2 Chamadas de função (p: 81-82)

* 6.5.3.4 Os operadores sizeof e _Alignof (p: 90-91)

* 6.5.4 Operadores de conversão (cast) (p: 91)

* 6.5.15 Operador condicional (p: 100)

* 6.5.17 Operador vírgula (p: 105)

* Padrão C99 (ISO/IEC 9899:1999):

* 6.5.2.2 Chamadas de função (p: 71-72)

* 6.5.3.4 O operador sizeof (p: 80-81)

* 6.5.4 Operadores de conversão (cast) (p: 81)

* 6.5.15 Operador condicional (p: 90-91)

* 6.5.17 Operador vírgula (p: 94)

* Padrão C89/C90 (ISO/IEC 9899:1990):

* 3.3.2.2 Chamadas de função

* 3.3.3.4 O operador sizeof

* 3.3.4 Operadores de conversão (cast)

* 3.3.15 Operador condicional

* 3.3.17 Operador vírgula

### Veja também

* [Precedência de operadores](<#/doc/language/operator_precedence>)

Operadores comuns
---
[atribuição](<#/doc/language/operator_assignment>) | [incremento
decremento](<#/doc/language/operator_incdec>) | [aritméticos](<#/doc/language/operator_arithmetic>) | [lógicos](<#/doc/language/operator_logical>) | [comparação](<#/doc/language/operator_comparison>) | [acesso a membro](<#/doc/language/operator_member_access>) | **outros**
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
[Documentação C++](<#/>) para Outros operadores
---