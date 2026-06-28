# Declaração de Array

Array é um tipo que consiste em uma sequência não vazia de objetos alocados contiguamente com um _tipo de elemento_ particular. O número desses objetos (o tamanho do array) nunca muda durante a vida útil do array.

### Sintaxe

Na [gramática de declaração](<#/doc/language/declarations>) de uma declaração de array, a sequência _type-specifier_ designa o _tipo de elemento_ (que deve ser um tipo de objeto completo), e o _declarador_ tem a forma:

---
`[` `static`(optional) qualifiers ﻿(optional) expression ﻿(optional) `]` attr-spec-seq ﻿(optional) | (1) |
`[` qualifiers ﻿(optional) `static`(optional) expression ﻿(optional) `]` attr-spec-seq ﻿(optional) | (2) |
`[` qualifiers ﻿(optional) `*` `]` attr-spec-seq ﻿(optional) | (3) |

1,2) Sintaxe geral do declarador de array

3) Declarador para VLA de tamanho não especificado (pode aparecer apenas no escopo do protótipo de função) onde

- **expression** — qualquer expressão diferente do [operador vírgula](<#/doc/language/operator_other>), designa o número de elementos no array
- **qualifiers** — qualquer combinação de qualificadores [`const`](<#/doc/language/const>), [`restrict`](<#/doc/language/restrict>), ou [`volatile`](<#/doc/language/volatile>), permitidos apenas em listas de parâmetros de função; isso qualifica o tipo de ponteiro para o qual este parâmetro de array é transformado
- **attr-spec-seq** — (C23)lista opcional de [atributos](<#/doc/language/attributes>), aplicados ao array declarado
```c
    float fa[11], *afp[17]; // fa é um array de 11 floats
                            // afp é um array de 17 ponteiros para floats
```

### Explicação

Existem várias variações de tipos de array: arrays de tamanho constante conhecido, arrays de tamanho variável e arrays de tamanho desconhecido.

#### Arrays de tamanho constante conhecido

Se a expressão em um declarador de array for uma [expressão constante inteira](<#/doc/language/constant_expression>) com um valor maior que zero e o tipo de elemento for um tipo com um tamanho constante conhecido (ou seja, os elementos não são VLA)(desde C99), então o declarador declara um array de tamanho constante conhecido:
```c
    int n[10]; // constantes inteiras são expressões constantes
    char o[sizeof(double)]; // sizeof é uma expressão constante
    enum { MAX_SZ=100 };
    int n[MAX_SZ]; // constantes enum são expressões constantes
```

Arrays de tamanho constante conhecido podem usar [inicializadores de array](<#/doc/language/array_initialization>) para fornecer seus valores iniciais:
```c
    int a[5] = {1,2,3}; // declara int[5] inicializado para 1,2,3,0,0
    char str[] = "abc"; // declara char[4] inicializado para 'a','b','c','\0'
```

Em listas de parâmetros de função, elementos de sintaxe adicionais são permitidos dentro dos declaradores de array: a palavra-chave `static` e qualificadores, que podem aparecer em qualquer ordem antes da expressão de tamanho (eles também podem aparecer mesmo quando a expressão de tamanho é omitida). Em cada [chamada de função](<#/doc/language/operator_other>) para uma função onde um parâmetro de array usa a palavra-chave `static` entre `[` e `]`, o valor do parâmetro real deve ser um ponteiro válido para o primeiro elemento de um array com pelo menos tantos elementos quanto especificado pela expressão:
```c
    void fadd(double a[static 10], const double b[static 10])
    {
        for (int i = 0; i < 10; i++)
        {
            if (a[i] < 0.0) return;
            a[i] += b[i];
        }
    }
    // uma chamada para fadd pode realizar verificação de limites em tempo de compilação
    // e também permite otimizações como prefetching de 10 doubles
    int main(void)
    {
        double a[10] = {0}, b[20] = {0};
        fadd(a, b); // OK
        double x[5] = {0};
        fadd(x, b); // comportamento indefinido: argumento do array é muito pequeno
    }
```

Se qualificadores estiverem presentes, eles qualificam o tipo de ponteiro para o qual o tipo de parâmetro de array é transformado:
```c
    int f(const int a[20])
    {
        // nesta função, a tem o tipo const int* (ponteiro para const int)
    }
    int g(const int a[const 20])
    {
        // nesta função, a tem o tipo const int* const (ponteiro const para const int)
    }
```

Isso é comumente usado com o qualificador de tipo [`restrict`](<#/doc/language/restrict>):
```c
    void fadd(double a[static restrict 10],
              const double b[static restrict 10])
    {
        for (int i = 0; i < 10; i++) // o loop pode ser desenrolado e reordenado
        {
            if (a[i] < 0.0)
                break;
            a[i] += b[i];
        }
    }
```

#### Arrays de tamanho variável

Se a expressão não for uma [expressão constante inteira](<#/doc/language/constant_expression>), o declarador é para um array de tamanho variável. Cada vez que o fluxo de controle passa pela declaração, a expressão é avaliada (e deve sempre avaliar para um valor maior que zero), e o array é alocado (correspondentemente, a [vida útil](<#/doc/language/lifetime>) de um VLA termina quando a declaração sai do escopo). O tamanho de cada instância de VLA não muda durante sua vida útil, mas em outra passagem sobre o mesmo código, ele pode ser alocado com um tamanho diferente. Execute este código
```c
    #include <stdio.h>
     
    int main(void)
    {
       int n = 1;
    label:;
       int a[n]; // realocado 10 vezes, cada um com um tamanho diferente
       printf("The array has %zu elements\n", sizeof a / sizeof *a);
       if (n++ < 10)
           goto label; // sair do escopo de um VLA encerra sua vida útil
    }
```

Se o tamanho for `*`, a declaração é para um VLA de tamanho não especificado. Tal declaração pode aparecer apenas no escopo de um protótipo de função e declara um array de um tipo completo. Na verdade, todos os declaradores VLA no escopo de protótipo de função são tratados como se a expressão fosse substituída por `*`.
```c
    void foo(size_t x, int a[*]);
    void foo(size_t x, int a[x])
    {
        printf("%zu\n", sizeof a); // o mesmo que sizeof(int*)
    }
```

Arrays de tamanho variável e os tipos derivados deles (ponteiros para eles, etc.) são comumente conhecidos como "tipos variably-modified" (VM). Objetos de qualquer tipo variably-modified podem ser declarados apenas no escopo de bloco ou no escopo de protótipo de função.
```c
    extern int n;
    int A[n];            // Erro: VLA de escopo de arquivo
    extern int (*p2)[n]; // Erro: VM de escopo de arquivo
    int B[100];          // OK: array de escopo de arquivo de tamanho constante conhecido
    void fvla(int m, int C[m][m]); // OK: VLA de escopo de protótipo
```

VLA devem ter duração de armazenamento automática ou alocada. Ponteiros para VLA, mas não os próprios VLA, também podem ter duração de armazenamento estática. Nenhum tipo VM pode ter ligação.
```c
    void fvla(int m, int C[m][m]) // OK: ponteiro de escopo de bloco/duração automática para VLA
    {
        typedef int VLA[m][m]; // OK: VLA de escopo de bloco
        int D[m];              // OK: VLA de escopo de bloco/duração automática
    //  static int E[m]; // Erro: VLA de duração estática
    //  extern int F[m]; // Erro: VLA com ligação
        int (*s)[m];     // OK: VM de escopo de bloco/duração automática
        s = malloc(m * sizeof(int)); // OK: s aponta para VLA em armazenamento alocado
    //  extern int (*r)[m]; // Erro: VM com ligação
        static int (*q)[m] = &B; // OK: VM de escopo de bloco/duração estática}
    }
```

Tipos variably-modified não podem ser membros de structs ou unions.
```c
    struct tag
    {
        int z[n]; // Erro: membro struct VLA
        int (*y)[n]; // Erro: membro struct VM
    };
```

| (desde C99)
Se o compilador definir a macro constante __STDC_NO_VLA__ para a constante inteira 1, então os tipos VLA e VM não são suportados. | (desde C11)
(ate C23)
Se o compilador definir a macro constante __STDC_NO_VLA__ para a constante inteira 1, então objetos VLA com duração de armazenamento automática não são suportados. O suporte para tipos VM e VLAs com durações de armazenamento alocadas é obrigatório. | (desde C23)

#### Arrays de tamanho desconhecido

Se a expressão em um declarador de array for omitida, ela declara um array de tamanho desconhecido. Exceto em listas de parâmetros de função (onde tais arrays são transformados em ponteiros) e quando um [inicializador](<#/doc/language/array_initialization>) está disponível, tal tipo é um [tipo incompleto](<#/doc/language/compatible_type>) (note que VLA de tamanho não especificado, declarado com `*` como o tamanho, é um tipo completo)(desde C99):
```c
    extern int x[]; // o tipo de x é "array de limite desconhecido de int"
    int a[] = {1,2,3}; // o tipo de a é "array de 3 int"
```

Dentro de uma definição de [struct](<#/doc/language/struct>), um array de tamanho desconhecido pode aparecer como o último membro (desde que haja pelo menos um outro membro nomeado), caso em que é um caso especial conhecido como _membro de array flexível_. Veja [struct](<#/doc/language/struct>) para detalhes:
```c
    struct s { int n; double d[]; }; // s.d é um membro de array flexível
    struct s *s1 = malloc(sizeof (struct s) + (sizeof (double) * 8)); // como se d fosse double d[8]
```

| (desde C99)

#### Qualificadores

Se um tipo de array for declarado com um qualificador [`const`](<#/doc/language/const>), [`volatile`](<#/doc/language/volatile>), ou [`restrict`](<#/doc/language/restrict>)(desde C99) (o que é possível através do uso de [typedef](<#/doc/language/typedef>)), o tipo de array não é qualificado, mas seu tipo de elemento é: | (ate C23)
Um tipo de array e seu tipo de elemento são sempre considerados identicamente qualificados, exceto que um tipo de array nunca é considerado qualificado como [`_Atomic`](<#/doc/language/atomic>). | (desde C23)
```c
    typedef int A[2][3];
    const A a = {{4, 5, 6}, {7, 8, 9}}; // array de array de int const
    int* pi = a[0]; // Erro: a[0] tem o tipo const int*
    void* unqual_ptr = a; // OK ate C23; erro desde C23
    // Notas: clang aplica a regra em C++/C23 mesmo nos modos C89-C17
```

[`_Atomic`](<#/doc/language/atomic>) não é permitido ser aplicado a um tipo de array, embora um array de tipo atômico seja permitido.
```c
    typedef int A[2];
    // _Atomic A a0 = {0};    // Erro
    // _Atomic(A) a1 = {0};   // Erro
    _Atomic int a2[2] = {0};  // OK
    _Atomic(int) a3[2] = {0}; // OK
```

| (desde C11)

#### Atribuição

Objetos do tipo array não são [lvalues modificáveis](<#/doc/language/value_category>), e embora seu endereço possa ser obtido, eles não podem aparecer no lado esquerdo de um operador de atribuição. No entanto, structs com membros de array são lvalues modificáveis e podem ser atribuídos:
```c
    int a[3] = {1,2,3}, b[3] = {4,5,6};
    int (*p)[3] = &a; // ok, o endereço de a pode ser obtido
    // a = b;            // erro, a é um array
    struct { int c[3]; } s1, s2 = {3,4,5};
    s1 = s2; // ok: pode atribuir structs que contêm membros de array
```

#### Conversão de array para ponteiro

Qualquer [expressão lvalue](<#/doc/language/value_category>) de tipo array, quando usada em qualquer contexto diferente de

  * como operando do [operador address-of](<#/doc/language/operator_member_access>)
  * como operando de [`sizeof`](<#/doc/language/sizeof>)
  * como operando de [`typeof`](<#/doc/language/typeof_unqual>) e [`typeof_unqual`](<#/doc/language/typeof_unqual>) (desde C23)
  * como o literal de string usado para [inicialização de array](<#/doc/language/array_initialization>)
  * como operando de [`_Alignof`](<#/doc/language/alignof>)(desde C11)(ate C23)[`alignof`](<#/doc/language/alignof>)(desde C23)

| (desde C11)

sofre uma [conversão implícita](<#/doc/language/conversion>) para o ponteiro para seu primeiro elemento. O resultado não é um lvalue.

Se o array foi declarado [`register`](<#/doc/language/storage_duration>), o comportamento do programa que tenta tal conversão é indefinido.
```c
    int a[3] = {1,2,3};
    int* p = a;
    printf("%zu\n", sizeof a); // imprime o tamanho do array
    printf("%zu\n", sizeof p); // imprime o tamanho de um ponteiro
```

Quando um tipo de array é usado em uma lista de parâmetros de função, ele é transformado para o tipo de ponteiro correspondente: int f(int a[2]) e int f(int* a) declaram a mesma função. Como o tipo de parâmetro real da função é um tipo de ponteiro, uma chamada de função com um argumento de array realiza a conversão de array para ponteiro; o tamanho do array argumento não está disponível para a função chamada e deve ser passado explicitamente:

Execute este código
```c
    #include <stdio.h>
     
    void f(int a[], int sz) // na verdade declara void f(int* a, int sz)
    {
        for (int i = 0; i < sz; ++i)
            printf("%d\n", a[i]);
    }
     
    void g(int (*a)[10]) // ponteiro para parâmetro de array não é transformado
    {
        for (int i = 0; i < 10; ++i)
            printf("%d\n", (*a)[i]);
    }
     
    int main(void)
    {
        int a[10] = {0};
        f(a, 10); // converte a para int*, passa o ponteiro
        g(&a);    // passa um ponteiro para o array (não há necessidade de passar o tamanho)
    }
```

#### Arrays multidimensionais

Quando o tipo de elemento de um array é outro array, diz-se que o array é multidimensional:
```c
    // array de 2 arrays de 3 ints cada
    int a[2][3] = {{1,2,3},  // pode ser visto como uma matriz 2x3
                   {4,5,6}}; // com layout row-major
```

Note que quando a conversão de array para ponteiro é aplicada, um array multidimensional é convertido para um ponteiro para seu primeiro elemento, por exemplo, ponteiro para a primeira linha:
```c
    int a[2][3]; // matriz 2x3
    int (*p1)[3] = a; // ponteiro para a primeira linha de 3 elementos
    int b[3][3][3]; // cubo 3x3x3
    int (*p2)[3][3] = b; // ponteiro para o primeiro plano 3x3
```

Arrays multidimensionais podem ser variably modified em todas as dimensões se VLAs forem suportados(desde C11):
```c
    int n = 10;
    int a[n][2*n];
```

| (desde C99)

### Notas

Declarações de array de comprimento zero não são permitidas, embora alguns compiladores as ofereçam como extensões (tipicamente como uma implementação pré-C99 de [membros de array flexíveis](<#/doc/language/struct>)).

Se a expressão de tamanho de um VLA tiver efeitos colaterais, eles são garantidos de serem produzidos, exceto quando faz parte de uma expressão sizeof cujo resultado não depende dela:
```c
    int n = 5, m = 5;
    size_t sz = sizeof(int (*[n++])[m++]); // n é incrementado, m pode ou não ser incrementado
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 6.7.6.2 Declaradores de array (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 6.7.6.2 Declaradores de array (p: 94-96)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 6.7.6.2 Declaradores de array (p: 130-132)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 6.7.5.2 Declaradores de array (p: 116-118)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 3.5.4.2 Declaradores de array

### Veja também

[Documentação C++](<#/>) para Declaração de Array
---