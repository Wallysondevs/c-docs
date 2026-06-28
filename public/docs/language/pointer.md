# Declaração de Ponteiro

Ponteiro é um tipo de objeto que se refere a uma função ou a um objeto de outro tipo, possivelmente adicionando qualificadores. Um ponteiro também pode se referir a nada, o que é indicado pelo valor especial de ponteiro nulo.

### Sintaxe

Na [gramática de declaração](<#/doc/language/declarations>) de uma declaração de ponteiro, a sequência de especificadores de tipo designa o tipo apontado (que pode ser um tipo de função ou objeto e pode ser incompleto), e o declarador tem a forma:

---
`*` attr-spec-seq ﻿(opcional) qualifiers ﻿(opcional) declarator
  
onde declarator pode ser o identificador que nomeia o ponteiro que está sendo declarado, incluindo outro declarador de ponteiro (o que indicaria um ponteiro para um ponteiro):
```c
    float *p, **pp; // p is a pointer to float
                    // pp is a pointer to a pointer to float
    int (*fp)(int); // fp is a pointer to function with type int(int)
```

Os qualificadores que aparecem entre `*` e o identificador (ou outro declarador aninhado) qualificam o tipo do ponteiro que está sendo declarado:
```c
    int n;
    const int * pc = &n; // pc is a non-const pointer to a const int
    // *pc = 2; // Error: n cannot be changed through pc without a cast
    pc = NULL; // OK: pc itself can be changed
     
    int * const cp = &n; // cp is a const pointer to a non-const int
    *cp = 2; // OK to change n through cp
    // cp = NULL; // Error: cp itself cannot be changed
     
    int * const * pcp = &cp; // non-const pointer to const pointer to non-const int
```

O attr-spec-seq(C23) é uma lista opcional de [atributos](<#/doc/language/attributes>), aplicada ao ponteiro declarado.

### Explicação

Ponteiros são usados para indireção, que é uma técnica de programação ubíqua; eles podem ser usados para implementar semânticas de passagem por referência, para acessar objetos com [duração de armazenamento](<#/doc/language/storage_duration>) dinâmica, para implementar tipos "opcionais" (usando o valor de ponteiro nulo), relacionamento de agregação entre structs, callbacks (usando ponteiros para funções), interfaces genéricas (usando ponteiros para void), e muito mais.

#### Ponteiros para objetos

Um ponteiro para objeto pode ser inicializado com o resultado do [operador address-of](<#/doc/language/operator_member_access>) aplicado a uma expressão de tipo de objeto (que pode ser incompleto):
```c
    int n;
    int *np = &n; // pointer to int
    int *const *npp = &np; // non-const pointer to const pointer to non-const int
     
    int a[2];
    int (*ap)[2] = &a; // pointer to array of int
     
    struct S { int n; } s = {1}
    int* sp = &s.n; // pointer to the int that is a member of s
```

Ponteiros podem aparecer como operandos para o [operador de indireção](<#/doc/language/operator_member_access>) (unário `*`), que retorna [o lvalue](<#/doc/language/value_category>) que identifica o objeto apontado:
```c
    int n;
    int* p = &n; // pointer p is pointing to n
    *p = 7; // stores 7 in n
    printf("%d\n", *p); // lvalue-to-rvalue conversion reads the value from n
```

Ponteiros para objetos dos tipos [struct](<#/doc/language/struct>) e [union](<#/doc/language/union>) também podem aparecer como operandos do lado esquerdo do [operador de acesso a membro através de ponteiro](<#/doc/language/operator_member_access>) `- >`.

Devido à conversão implícita de [array para ponteiro](<#/doc/language/array>), o ponteiro para o primeiro elemento de um array pode ser inicializado com uma expressão de tipo array:
```c
    int a[2];
    int *p = a; // pointer to a[0]
     
    int b[3][3];
    int (*row)[3] = b; // pointer to b[0]
```

Certos operadores de [adição, subtração](<#/doc/language/operator_arithmetic>), [atribuição composta](<#/doc/language/operator_assignment>), [incremento e decremento](<#/doc/language/operator_incdec>) são definidos para ponteiros para elementos de arrays.

[Operadores de comparação](<#/doc/language/operator_comparison>) são definidos para ponteiros para objetos em algumas situações: dois ponteiros que representam o mesmo endereço comparam como iguais, dois valores de ponteiro nulo comparam como iguais, ponteiros para elementos do mesmo array comparam da mesma forma que os índices de array desses elementos, e ponteiros para membros de struct comparam na ordem de declaração desses membros.

Muitas implementações também fornecem [ordenação total estrita](<https://en.wikipedia.org/wiki/Total_order#Strict_total_order> "enwiki:Total order") de ponteiros de origem aleatória, por exemplo, se forem implementados como endereços dentro de um espaço de endereço virtual contínuo ("plano").

#### Ponteiros para funções

Um ponteiro para função pode ser inicializado com o endereço de uma função. Devido à conversão de [função para ponteiro](<#/doc/language/conversion>), o operador address-of é opcional:
```c
    void f(int);
    void (*pf1)(int) = &f;
    void (*pf2)(int) = f; // same as &f
```

Ao contrário das funções, ponteiros para funções são objetos e, portanto, podem ser armazenados em arrays, copiados, atribuídos, passados para outras funções como argumentos, etc.

Um ponteiro para função pode ser usado no lado esquerdo do [operador de chamada de função](<#/doc/language/operator_other>); isso invoca a função apontada:
```c
    #include <stdio.h>
     
    int f(int n)
    {
        printf("%d\n", n);
        return n * n;
    }
     
    int main(void)
    {
        int (*p)(int) = f;
        int x = p(7);
    }
```

Desreferenciar um ponteiro de função resulta no designador de função para a função apontada:
```c
    int f();
    int (*p)() = f;    // pointer p is pointing to f
    (*p)(); // function f invoked through the function designator
    p();    // function f invoked directly through the pointer
```

[Operadores de comparação de igualdade](<#/doc/language/operator_comparison>) são definidos para ponteiros para funções (eles comparam como iguais se apontarem para a mesma função).

Como a [compatibilidade de tipos de função](<#/doc/language/compatible_type>) ignora qualificadores de nível superior dos parâmetros da função, ponteiros para funções cujos parâmetros diferem apenas em seus qualificadores de nível superior são intercambiáveis:
```c
    int f(int), fc(const int);
    int (*pc)(const int) = f; // OK
    int (*p)(int) = fc;       // OK
    pc = p;                   // OK
```

#### Ponteiros para void

Ponteiro para objeto de qualquer tipo pode ser [implicitamente convertido](<#/doc/language/conversion>) para ponteiro para void (opcionalmente qualificado com [const](<#/doc/language/const>) ou [volatile](<#/doc/language/volatile>)), e vice-versa:
```c
    int n=1, *p=&n;
    void* pv = p; // int* to void*
    int* p2 = pv; // void* to int*
    printf("%d\n", *p2); // prints 1
```

Ponteiros para void são usados para passar objetos de tipo desconhecido, o que é comum em interfaces genéricas: [malloc](<#/doc/memory/malloc>) retorna void*, [qsort](<#/doc/algorithm/qsort>) espera um callback fornecido pelo usuário que aceita dois argumentos const void*. [pthread_create](<http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_create.html>) espera um callback fornecido pelo usuário que aceita e retorna void*. Em todos os casos, é responsabilidade do chamador converter o ponteiro para o tipo correto antes do uso.

### Ponteiros nulos

Ponteiros de cada tipo têm um valor especial conhecido como _valor de ponteiro nulo_ desse tipo. Um ponteiro cujo valor é nulo não aponta para um objeto ou uma função (desreferenciar um ponteiro nulo é comportamento indefinido), e compara como igual a todos os ponteiros do mesmo tipo cujo valor também é _nulo_.

Para inicializar um ponteiro como nulo ou para atribuir o valor nulo a um ponteiro existente, uma constante de ponteiro nulo ([NULL](<#/doc/types/NULL>), ou qualquer outra constante inteira com o valor zero) pode ser usada. A [inicialização estática](<#/doc/language/initialization>) também inicializa ponteiros com seus valores nulos.

Ponteiros nulos podem indicar a ausência de um objeto ou podem ser usados para indicar outros tipos de condições de erro. Em geral, uma função que recebe um argumento ponteiro quase sempre precisa verificar se o valor é nulo e lidar com esse caso de forma diferente (por exemplo, [free](<#/doc/memory/free>) não faz nada quando um ponteiro nulo é passado).

### Notas

Embora qualquer ponteiro para objeto [possa ser convertido](<#/doc/language/cast>) para ponteiro para objeto de um tipo diferente, desreferenciar um ponteiro para um tipo diferente do tipo declarado do objeto é quase sempre comportamento indefinido. Veja [aliasing estrito](<#/doc/language/object>) para detalhes.

É possível indicar a uma função que acessa objetos através de ponteiros que esses ponteiros não fazem aliasing. Veja [restrict](<#/doc/language/restrict>) para detalhes. | (desde C99)
  
Expressões lvalue de tipo array, quando usadas na maioria dos contextos, sofrem uma [conversão implícita](<#/doc/language/conversion>) para o ponteiro para o primeiro elemento do array. Veja [array](<#/doc/language/array>) para detalhes.
```c
    char *str = "abc"; // "abc" is a char[4] array, str is a pointer to 'a'
```

Ponteiros para char são frequentemente [usados para representar strings](<#/doc/string/byte>). Para representar uma string de bytes válida, um ponteiro deve estar apontando para um char que é um elemento de um array de char, e deve haver um char com o valor zero em algum índice maior ou igual ao índice do elemento referenciado pelo ponteiro.

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 6.7.6.1 Declaradores de ponteiro (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 6.7.6.1 Declaradores de ponteiro (p: 93-94)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 6.7.6.1 Declaradores de ponteiro (p: 130)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 6.7.5.1 Declaradores de ponteiro (p: 115-116)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 3.5.4.1 Declaradores de ponteiro

### Veja também

[Documentação C++](<#/>) para Declaração de Ponteiro
---