# Inicialização de arrays

Ao [inicializar](<#/doc/language/initialization>) um objeto do tipo [array](<#/doc/language/array>), o inicializador deve ser um [literal de string](<#/doc/language/string_literal>) (opcionalmente entre chaves) ou uma lista de inicializadores entre chaves para os membros do array:

---
`=` string-literal | (1) |
`=` `{` expression `,` `...` `}` | (2) | (até C99)
`=` `{` designator(optional) expression `,` `...` `}` | (2) | (desde C99)
`=` `{` `}` | (3) | (desde C23)

1) inicializador de literal de string para arrays de caracteres e caracteres largos

2) lista de expressões constantes (até C99) separadas por vírgulas que são inicializadores para elementos do array, opcionalmente usando designadores de array na forma `[` constant-expression `]` `=` (desde C99)

3) inicializador vazio inicializa a zero (empty-initializes) cada elemento do array

Arrays de tamanho conhecido e arrays de tamanho desconhecido podem ser inicializados, mas não VLAs (desde C99) (até C23). Um VLA só pode ser inicializado a zero (empty-initialized). (desde C23)

Todos os elementos do array que não são inicializados explicitamente são [inicializados a zero](<#/doc/language/initialization>).

### Inicialização a partir de strings

[Literais de string](<#/doc/language/string_literal>) (opcionalmente entre chaves) podem ser usados como inicializador para um array de tipo correspondente:

  * literais de string comuns e literais de string UTF-8 (desde C11) podem inicializar arrays de qualquer tipo de caractere (char, signed char, unsigned char)
  * literais de string largos prefixados com L podem ser usados para inicializar arrays de qualquer tipo compatível com (ignorando cv-qualificadores) wchar_t
  * literais de string largos prefixados com u podem ser usados para inicializar arrays de qualquer tipo compatível com (ignorando cv-qualificadores) char16_t
  * literais de string largos prefixados com U podem ser usados para inicializar arrays de qualquer tipo compatível com (ignorando cv-qualificadores) char32_t

| (desde C11)

Bytes sucessivos do literal de string ou caracteres largos do literal de string largo, incluindo o byte/caractere nulo terminador, inicializam os elementos do array:
```c
    char str[] = "abc"; // str has type char[4] and holds 'a', 'b', 'c', '\0'
    wchar_t wstr[4] = L"猫"; // str has type wchar_t[4] and holds L'猫', '\0', '\0', '\0'
```

Se o tamanho do array for conhecido, ele pode ser um a menos que o tamanho do literal de string, caso em que o caractere nulo terminador é ignorado:
```c
    char str[3] = "abc"; // str has type char[3] and holds 'a', 'b', 'c'
```

Note que o conteúdo de tal array é modificável, ao contrário de quando se acessa um literal de string diretamente com char* str = "abc";.

### Inicialização a partir de listas entre chaves

Quando um array é inicializado com uma lista de inicializadores entre chaves, o primeiro inicializador na lista inicializa o elemento do array no índice zero (a menos que um designador seja especificado) (desde C99), e cada inicializador subsequente sem um designador (desde C99) inicializa o elemento do array no índice um maior do que o inicializado pelo inicializador anterior.
```c
    int x[] = {1,2,3}; // x has type int[3] and holds 1,2,3
    int y[5] = {1,2,3}; // y has type int[5] and holds 1,2,3,0,0
    int z[4] = {1}; // z has type int[4] and holds 1,0,0,0
    int w[3] = {0}; // w has type int[3] and holds all zeroes
```

É um erro fornecer mais inicializadores do que elementos ao inicializar um array de tamanho conhecido (exceto ao inicializar arrays de caracteres a partir de literais de string).

Um designador faz com que o inicializador seguinte inicialize o elemento do array descrito pelo designador. A inicialização então continua em ordem, começando com o próximo elemento após aquele descrito pelo designador.
```c
    int n[5] = {[4]=5,[0]=1,2,3,4}; // holds 1,2,3,4,5
    
    int a[MAX] = { // starts initializing a[0] = 1, a[1] = 3, ...
        1, 3, 5, 7, 9, [MAX-5] = 8, 6, 4, 2, 0
    };
    // for MAX=6,  array holds 1,8,6,4,2,0
    // for MAX=13, array holds 1,3,5,7,9,0,0,0,8,6,4,2,0 ("sparse array")
```

| (desde C99)

Ao inicializar um array de tamanho desconhecido, o maior subscrito para o qual um inicializador é especificado determina o tamanho do array que está sendo declarado.

### Arrays aninhados

Se os elementos de um array forem arrays, structs ou unions, os inicializadores correspondentes na lista de inicializadores entre chaves são quaisquer inicializadores válidos para esses membros, exceto que suas chaves podem ser omitidas da seguinte forma:

Se o inicializador aninhado começar com uma chave de abertura, todo o inicializador aninhado até sua chave de fechamento inicializa o elemento do array correspondente:
```c
    int y[4][3] = { // array of 4 arrays of 3 ints each (4x3 matrix)
        { 1 },      // row 0 initialized to {1, 0, 0}
        { 0, 1 },   // row 1 initialized to {0, 1, 0}
        { [2]=1 },  // row 2 initialized to {0, 0, 1}
    };              // row 3 initialized to {0, 0, 0}
```

Se o inicializador aninhado não começar com uma chave de abertura, apenas inicializadores suficientes da lista são usados para contabilizar os elementos ou membros do sub-array, struct ou union; quaisquer inicializadores restantes são deixados para inicializar o próximo elemento do array:
```c
    int y[4][3] = {    // array of 4 arrays of 3 ints each (4x3 matrix)
    1, 3, 5, 2, 4, 6, 3, 5, 7 // row 0 initialized to {1, 3, 5}
    };                        // row 1 initialized to {2, 4, 6}
                              // row 2 initialized to {3, 5, 7}
                              // row 3 initialized to {0, 0, 0}
    
    struct { int a[3], b; } w[] = { { 1 }, 2 }; // array of structs
       // { 1 } is taken to be a fully-braced initializer for element #0 of the array
       // that element is initialized to { {1, 0, 0}, 0}
       // 2 is taken to be the first initialized for element #1 of the array
       // that element is initialized { {2, 0, 0}, 0}
```

Designadores de array podem ser aninhados; a expressão constante entre colchetes para arrays aninhados segue a expressão constante entre colchetes para o array externo:
```c
    int y[4][3] = {[0][0]=1, [1][1]=1, [2][0]=1};  // row 0 initialized to {1, 0, 0}
                                                   // row 1 initialized to {0, 1, 0}
                                                   // row 2 initialized to {1, 0, 0}
                                                   // row 3 initialized to {0, 0, 0}
```

| (desde C99)

### Notas

A [ordem de avaliação](<#/doc/language/eval_order>) de subexpressões em um inicializador de array é indeterminadamente sequenciada em C (mas não em C++ desde C++11):
```c
    int n = 1;
    int a[2] = {n++, n++}; // unspecified, but well-defined behavior,
                           // n is incremented twice (in arbitrary order)
                           // a initialized to {1, 2} and to {2, 1} are both valid
    puts((char[4]){'0'+n} + n++); // undefined behavior:
                                  // increment and read from n are unsequenced
```

Em C, a lista entre chaves de um inicializador não pode ser vazia. C++ permite lista vazia: | (até C23)
Um inicializador vazio pode ser usado para inicializar um array: | (desde C23)
```c
    int a[3] = {0}; // valid C and C++ way to zero-out a block-scope array
    int a[3] = {}; // valid C++ way to zero-out a block-scope array; valid in C since C23
```

Assim como em todas as outras [inicializações](<#/doc/language/initialization>), cada expressão na lista de inicializadores deve ser uma [expressão constante](<#/doc/language/constant_expression>) ao inicializar arrays com [duração de armazenamento](<#/doc/language/storage_duration>) estática ou thread-local:
```c
    static char* p[2] = {malloc(1), malloc(2)}; // error
```

### Exemplo

Execute este código
```c
    int main(void)
    {
        // The following four array declarations are the same
        short q1[4][3][2] = {
            { 1 },
            { 2, 3 },
            { 4, 5, 6 }
        };
    
        short q2[4][3][2] = {1, 0, 0, 0, 0, 0, 2, 3, 0, 0, 0, 0, 4, 5, 6};
    
        short q3[4][3][2] = {
            {
                { 1 },
            },
            {
                { 2, 3 },
            },
            {
                { 4, 5 },
                { 6 },
            }
        };
    
        short q4[4][3][2] = {1, [1]=2, 3, [2]=4, 5, 6};
    
    
        // Character names can be associated with enumeration constants
        // using arrays with designators:
        enum { RED, GREEN, BLUE };
        const char *nm[] = {
            [RED] = "red",
            [GREEN] = "green",
            [BLUE] = "blue",
        };
    }
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 6.7.9/12-39 Inicialização (p: 101-105)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 6.7.9/12-38 Inicialização (p: 140-144)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 6.7.8/12-38 Inicialização (p: 126-130)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 6.5.7 Inicialização