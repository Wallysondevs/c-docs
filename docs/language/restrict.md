# qualificador de tipo restrict (desde C99)

Cada tipo individual no [sistema de tipos](<#/doc/language/compatible_type>) do C possui várias versões _qualificadas_ desse tipo, correspondendo a um, dois ou todos os três qualificadores [`const`](<#/doc/language/const>), [`volatile`](<#/doc/language/volatile>) e, para ponteiros para tipos de objeto, `restrict`. Esta página descreve os efeitos do qualificador `restrict`.

Apenas um ponteiro para um [tipo de objeto](<#/doc/language/compatible_type>) ou um array (possivelmente multidimensional) do mesmo (desde C23) pode ser qualificado com restrict; em particular, os seguintes são _errôneos_:

  * int restrict *p
  * float (* restrict f9)(void)

A semântica de restrict se aplica apenas a expressões lvalue; por exemplo, um cast para um ponteiro qualificado com restrict ou uma chamada de função que retorna um ponteiro qualificado com restrict não são lvalues e o qualificador não tem efeito.

Durante cada execução de um bloco no qual um ponteiro restrito `P` é declarado (tipicamente cada execução de um corpo de função no qual `P` é um parâmetro de função), se algum objeto que é acessível através de `P` (direta ou indiretamente) for modificado, por qualquer meio, então todos os acessos a esse objeto (tanto leituras quanto escritas) nesse bloco devem ocorrer através de `P` (direta ou indiretamente), caso contrário, o comportamento é indefinido:
```c
    void f(int n, int * restrict p, int * restrict q)
    {
        while (n-- > 0)
            *p++ = *q++; // nenhum dos objetos modificados através de *p é o mesmo
                         // que qualquer um dos objetos lidos através de *q
                         // o compilador é livre para otimizar, vetorizar, mapear páginas, etc.
    }
    
    void g(void)
    {
        extern int d[100];
        f(50, d + 50, d); // OK
        f(50, d + 1, d);  // Comportamento indefinido: d[1] é acessado através de p e q em f
    }
```

Se o objeto nunca for modificado, ele pode ser apelidado (aliased) e acessado através de diferentes ponteiros qualificados com restrict (note que se os objetos apontados por ponteiros qualificados com restrict que são apelidados forem, por sua vez, ponteiros, esse aliasing pode inibir a otimização).

A atribuição de um ponteiro restrito para outro é comportamento indefinido, exceto ao atribuir de um ponteiro para um objeto em um bloco externo para um ponteiro em um bloco interno (incluindo o uso de um argumento de ponteiro restrito ao chamar uma função com um parâmetro de ponteiro restrito) ou ao retornar de uma função (e, de outra forma, quando o bloco do ponteiro de origem terminou):
```c
    int* restrict p1 = &a;
    int* restrict p2 = &b;
    p1 = p2; // comportamento indefinido
```

Ponteiros restritos podem ser atribuídos livremente a ponteiros não restritos, as oportunidades de otimização permanecem enquanto o compilador for capaz de analisar o código:
```c
    void f(int n, float * restrict r, float * restrict s)
    {
        float *p = r, *q = s; // OK
        while (n-- > 0)
            *p++ = *q++; // quase certamente otimizado da mesma forma que *r++ = *s++
    }
```

Se um tipo de array for declarado com o qualificador de tipo restrict (através do uso de [typedef](<#/doc/language/typedef>)), o tipo de array não é qualificado com restrict, mas seu tipo de elemento é: | (até C23)
Um tipo de array e seu tipo de elemento são sempre considerados identicamente qualificados com restrict: | (desde C23)
```c
    typedef int *array_t[10];
    
    restrict array_t a; // o tipo de a é int *restrict[10]
    // Notas: clang e icc rejeitam isso com base no fato de que array_t não é um tipo de ponteiro
    
    void *unqual_ptr = &a; // OK até C23; erro desde C23
    // Notas: clang aplica a regra em C++/C23 mesmo nos modos C89-C17
```

Em uma declaração de função, a palavra-chave `restrict` pode aparecer dentro dos colchetes que são usados para declarar um tipo de array de um parâmetro de função. Ela qualifica o tipo de ponteiro para o qual o tipo de array é transformado:
```c
    void f(int m, int n, float a[restrict m][n], float b[restrict m][n]);
    
    void g12(int n, float (*p)[n])
    {
       f(10, n, p, p+10); // OK
       f(20, n, p, p+10); // comportamento possivelmente indefinido (dependendo do que f faz)
    }
```

### Notas

O uso pretendido do qualificador restrict (assim como a classe de armazenamento register) é promover a otimização, e a exclusão de todas as instâncias do qualificador de todas as unidades de tradução de pré-processamento que compõem um programa em conformidade não altera seu significado (ou seja, comportamento observável).

O compilador é livre para ignorar quaisquer ou todas as implicações de aliasing dos usos de `restrict`.

Para evitar comportamento indefinido, o programador deve garantir que as asserções de aliasing feitas pelos ponteiros qualificados com restrict não sejam violadas.

Muitos compiladores fornecem, como uma extensão de linguagem, o oposto de `restrict`: um atributo indicando que ponteiros podem ter aliasing mesmo que seus tipos sejam diferentes: [`may_alias`](<https://gcc.gnu.org/onlinedocs/gcc/Common-Type-Attributes.html#index-g_t_0040code_007bmay_005falias_007d-type-attribute-3667>) (gcc),

### Padrões de uso

Existem vários padrões de uso comuns para ponteiros qualificados com restrict:

#### Escopo de arquivo

Um ponteiro qualificado com restrict de escopo de arquivo deve apontar para um único objeto de array durante a execução do programa. Esse objeto de array não pode ser referenciado tanto através do ponteiro restrito quanto através de seu nome declarado (se houver) ou de outro ponteiro restrito.

Ponteiros restritos de escopo de arquivo são úteis para fornecer acesso a arrays globais alocados dinamicamente; a semântica de restrict torna possível otimizar referências através deste ponteiro tão efetivamente quanto referências a um array estático através de seu nome declarado:
```c
    float *restrict a, *restrict b;
    float c[100];
    
    int init(int n)
    {
       float * t = malloc(2*n*sizeof(float));
       a = t;      // a se refere à 1ª metade
       b = t + n;  // b se refere à 2ª metade
    }
    // o compilador pode deduzir dos qualificadores restrict que
    // não há potencial aliasing entre os nomes a, b e c
```

#### Parâmetro de função

O caso de uso mais popular para ponteiros qualificados com restrict é o uso como parâmetros de função.

No exemplo a seguir, o compilador pode inferir que não há aliasing de objetos modificados e, assim, otimizar o loop agressivamente. Na entrada para `f`, o ponteiro restrito a deve fornecer acesso exclusivo ao seu array associado. Em particular, dentro de `f`, nem `b` nem `c` podem apontar para o array associado a `a`, porque nenhum deles recebe um valor de ponteiro baseado em `a`. Para `b`, isso é evidente pelo qualificador const em sua declaração, mas para `c`, uma inspeção do corpo de `f` é necessária:
```c
    float x[100];
    float *c;
    
    void f(int n, float * restrict a, float * const b)
    {
        int i;
        for ( i=0; i<n; i++ )
           a[i] = b[i] + c[i];
    }
    
    void g3(void)
    {
        float d[100], e[100];
        c = x; f(100,   d,    e); // OK
               f( 50,   d, d+50); // OK
               f( 99, d+1,    d); // comportamento indefinido
        c = d; f( 99, d+1,    e); // comportamento indefinido
               f( 99,   e,  d+1); // OK
    }
```

Note que é permitido que c aponte para o array associado a b. Note também que, para esses propósitos, o "array" associado a um ponteiro particular significa apenas a porção de um objeto de array que é realmente referenciada através desse ponteiro.

Note que no exemplo acima, o compilador pode inferir que a e b não têm aliasing porque a constness de b garante que ele não pode se tornar dependente de a no corpo da função. Equivalentemente, o programador poderia escrever void f(int n, float * a, float const * restrict b), caso em que o compilador pode inferir que objetos referenciados através de b não podem ser modificados, e assim nenhum objeto modificado pode ser referenciado usando tanto b quanto a. Se o programador escrevesse void f(int n, float * restrict a, float * b), o compilador seria incapaz de inferir o não-aliasing de a e b sem examinar o corpo da função.

Em geral, é melhor anotar explicitamente todos os ponteiros sem aliasing no protótipo de uma função com restrict.

#### Escopo de bloco

Um ponteiro qualificado com restrict de escopo de bloco faz uma asserção de aliasing que é limitada ao seu bloco. Ele permite asserções locais que se aplicam apenas a blocos importantes, como loops otimizados. Também torna possível converter uma função que aceita ponteiros qualificados com restrict em uma macro:
```c
    float x[100];
    float *c;
    
    #define f3(N, A, B)                                    \
    do                                                     \
    {   int n = (N);                                       \
        float * restrict a = (A);                          \
        float * const    b = (B);                          \
        int i;                                             \
        for ( i=0; i<n; i++ )                              \
            a[i] = b[i] + c[i];                            \
    } while(0)
```

#### Membros de struct

O escopo da asserção de aliasing feita por um ponteiro qualificado com restrict que é membro de uma struct é o escopo do identificador usado para acessar a struct.

Mesmo que a struct seja declarada no escopo de arquivo, quando o identificador usado para acessar a struct tem escopo de bloco, as asserções de aliasing na struct também têm escopo de bloco; as asserções de aliasing só estão em vigor dentro de uma execução de bloco ou de uma chamada de função, dependendo de como o objeto desse tipo de struct foi criado:
```c
    struct t      // Ponteiros restritos afirmam que
    {
       int n;     // membros apontam para armazenamento disjunto.
       float * restrict p;
       float * restrict q;
    };
    
    void ff(struct t r, struct t s)
    {
       struct t u;
       // r,s,u têm escopo de bloco
       // r.p, r.q, s.p, s.q, u.p, u.q devem todos apontar para
       // armazenamento disjunto durante cada execução de ff.
       // ...
    }
```

### Palavras-chave

[`restrict`](<#/doc/keyword/restrict>)

### Exemplo

exemplo de geração de código; compile com -S (gcc, clang, etc) ou /FA (visual studio)
```c
    int foo(int *a, int *b)
    {
        *a = 5;
        *b = 6;
        return *a + *b;
    }
    
    int rfoo(int *restrict a, int *restrict b)
    {
        *a = 5;
        *b = 6;
        return *a + *b;
    }
```

Saída possível:
```assembly
    ; código gerado em plataforma Intel de 64 bits:
    foo:
        movl    $5, (%rdi)    ; armazena 5 em *a
        movl    $6, (%rsi)    ; armazena 6 em *b
        movl    (%rdi), %eax  ; lê novamente de *a caso a gravação anterior o tenha modificado
        addl    $6, %eax      ; adiciona 6 ao valor lido de *a
        ret
    
    rfoo:
        movl      $11, %eax   ; o resultado é 11, uma constante em tempo de compilação
        movl      $5, (%rdi)  ; armazena 5 em *a
        movl      $6, (%rsi)  ; armazena 6 em *b
        ret
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 6.7.3.1 Definição formal de restrict (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 6.7.3.1 Definição formal de restrict (p: 89-90) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 6.7.3.1 Definição formal de restrict (p: 123-125) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 6.7.3.1 Definição formal de restrict (p: 110-112)