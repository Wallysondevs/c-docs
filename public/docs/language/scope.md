# Escopo

Cada [identificador](<#/doc/language/identifier>) que aparece em um programa C é _visível_ (ou seja, pode ser usado) apenas em alguma porção possivelmente descontínua do código-fonte chamada seu _escopo_.

Dentro de um escopo, um identificador pode designar mais de uma entidade apenas se as entidades estiverem em [espaços de nomes](<#/doc/language/name_space>) diferentes.

C tem quatro tipos de escopos:

*   escopo de bloco
*   escopo de arquivo
*   escopo de função
*   escopo de protótipo de função

### Escopos aninhados

Se duas entidades diferentes nomeadas pelo mesmo identificador estão em escopo ao mesmo tempo, e elas pertencem ao mesmo [espaço de nomes](<#/doc/language/name_space>), os escopos são aninhados (nenhuma outra forma de sobreposição de escopo é permitida), e a declaração que aparece no escopo interno oculta a declaração que aparece no escopo externo:
```c
    // O espaço de nomes aqui são identificadores comuns.

    int a;   // escopo de arquivo do nome a começa aqui

    void f(void)
    {
        int a = 1; // o escopo de bloco do nome a começa aqui; oculta o 'a' de escopo de arquivo
        {
          int a = 2;         // o escopo do 'a' interno começa aqui, o 'a' externo é ocultado
          printf("%d\n", a); // o 'a' interno está em escopo, imprime 2
        }                    // o escopo de bloco do 'a' interno termina aqui
        printf("%d\n", a);   // o 'a' externo está em escopo, imprime 1
    }                        // o escopo do 'a' externo termina aqui

    void g(int a);   // o nome a tem escopo de protótipo de função; oculta o 'a' de escopo de arquivo
```

### Escopo de bloco

O escopo de qualquer identificador declarado dentro de uma [instrução composta](<#/doc/language/statements>), incluindo corpos de função, ou em qualquer expressão, declaração ou instrução que aparece em [if](<#/doc/language/if>), [switch](<#/doc/language/switch>), [for](<#/doc/language/for>), [while](<#/doc/language/while>), ou [do-while](<#/doc/language/do>) (desde C99), ou dentro da lista de parâmetros de uma [definição de função](<#/doc/language/function_definition>) começa no ponto de declaração e termina no final do bloco ou instrução em que foi declarado.
```c
    void f(int n)  // o escopo do parâmetro de função 'n' começa
    {         // o corpo da função começa
       ++n;   // 'n' está em escopo e se refere ao parâmetro da função
    // int n = 2; // erro: não é possível redeclarar identificador no mesmo escopo
       for(int n = 0; n<10; ++n) { // o escopo do 'n' local do loop começa
           printf("%d\n", n); // imprime 0 1 2 3 4 5 6 7 8 9
       } // o escopo do 'n' local do loop termina
         // o parâmetro de função 'n' está de volta ao escopo
       printf("%d\n", n); // imprime o valor do parâmetro
    } // o escopo do parâmetro de função 'n' termina
    int a = n; // Erro: o nome 'n' não está em escopo
```

Até C99, as instruções de seleção e iteração não estabeleciam seus próprios escopos de bloco (embora se uma instrução composta fosse usada na instrução, ela tivesse seu escopo de bloco usual):
```c
    enum {a, b};
    int different(void)
    {
        if (sizeof(enum {b, a}) != sizeof(int))
            return a; // a == 1
        return b; // b == 0 em C89, b == 1 em C99
    }
```

| (desde C99)

Variáveis com escopo de bloco têm [nenhuma ligação](<#/doc/language/storage_duration>) e [duração de armazenamento automática](<#/doc/language/storage_duration>) por padrão. Note que a duração de armazenamento para variáveis locais não-VLA começa quando o bloco é inserido, mas até que a declaração seja vista, a variável não está em escopo e não pode ser acessada.

### Escopo de arquivo

O escopo de qualquer identificador declarado fora de qualquer bloco ou lista de parâmetros começa no ponto de declaração e termina no final da unidade de tradução.
```c
    int i; // o escopo de i começa
    static int g(int a) { return a; } // o escopo de g começa (note, "a" tem escopo de bloco)
    int main(void)
    {
        i = g(2); // i e g estão em escopo
    }
```

Identificadores com escopo de arquivo têm [ligação externa](<#/doc/language/storage_duration>) e [duração de armazenamento estática](<#/doc/language/storage_duration>) por padrão.

### Escopo de função

Um [rótulo (e apenas um rótulo)](<#/doc/language/statements>) declarado dentro de uma função está em escopo em toda essa função, em todos os blocos aninhados, antes e depois de sua própria declaração. Nota: um rótulo é declarado implicitamente, usando um identificador de outra forma não utilizado antes do caractere de dois pontos antes de qualquer instrução.
```c
    void f()
    {
       {
           goto label; // rótulo em escopo mesmo que declarado depois
    label:;
       }
       goto label; // rótulo ignora escopo de bloco
    }

    void g()
    {
        goto label; // erro: rótulo não está em escopo em g()
    }
```

### Escopo de protótipo de função

O escopo de um nome introduzido na lista de parâmetros de uma [declaração de função](<#/doc/language/function_declaration>) que não é uma definição termina no final do [declarador](<#/doc/language/declarations>) da função.
```c
    int f(int n,
          int a[n]); // n está em escopo e se refere ao primeiro parâmetro
```

Note que se houver múltiplos ou aninhados declaradores na declaração, o escopo termina no final do declarador de função mais próximo que o envolve:
```c
    void f ( // o nome da função 'f' está em escopo de arquivo
     long double f,            // o identificador 'f' está agora em escopo, o 'f' de escopo de arquivo é ocultado
     char (**a)[10 * sizeof f] // 'f' se refere ao primeiro parâmetro, que está em escopo
    );

    enum{ n = 3 };
    int (*(*g)(int n))[n]; // o escopo do parâmetro de função 'n'
                           // termina no final de seu declarador de função
                           // no declarador de array, o 'n' global está em escopo
    // (isso declara um ponteiro para função que retorna um ponteiro para um array de 3 int)
```

### Ponto de declaração

O escopo de tags de estrutura, união e enumeração começa imediatamente após a aparição da tag em um especificador de tipo que declara a tag.
```c
    struct Node {
       struct Node* next; // Node está em escopo e se refere a esta struct
    };
```

O escopo de uma constante de enumeração começa imediatamente após a aparição de seu enumerador definidor em uma lista de enumeradores.
```c
    enum { x = 12 };
    {
        enum { x = x + 1, // o novo x não está em escopo até a vírgula, x é inicializado para 13
               y = x + 1  // o novo enumerador x está agora em escopo, y é inicializado para 14
             };
    }
```

O escopo de qualquer outro identificador começa logo após o final de seu declarador e antes do inicializador, se houver:
```c
    int x = 2; // o escopo do primeiro 'x' começa
    {
        int x[x]; // o escopo do 'x' recém-declarado começa após o declarador (x[x]).
                  // Dentro do declarador, o 'x' externo ainda está em escopo.
                  // Isso declara um array VLA de 2 int.
    }
```
```c
    unsigned char x = 32; // o escopo do 'x' externo começa
    {
        unsigned char x = x;
                // o escopo do 'x' interno começa antes do inicializador (= x)
                // isso não inicializa o 'x' interno com o valor 32,
                // isso inicializa o 'x' interno com seu próprio valor, indeterminado
    }

    unsigned long factorial(unsigned long n)
    // o declarador termina, 'factorial' está em escopo a partir deste ponto
    {
       return n<2 ? 1 : n*factorial(n-1); // chamada recursiva
    }
```

Como um caso especial, o escopo de um [nome de tipo](<#/doc/language/compatible_type>) que não é uma declaração de um identificador é considerado para começar logo após o local dentro do nome de tipo onde o identificador apareceria se não fosse omitido.

### Notas

Antes de C89, identificadores com ligação externa tinham escopo de arquivo mesmo quando introduzidos dentro de um bloco, e por causa disso, um compilador C89 não é obrigado a diagnosticar o uso de um identificador extern que saiu do escopo (tal uso é comportamento indefinido).

Variáveis locais dentro do corpo de um loop podem ocultar variáveis declaradas na cláusula init de um loop [for](<#/doc/language/for>) em C (seus escopos são aninhados), mas não podem fazer isso em C++.

Ao contrário de C++, C não tem escopo de struct: nomes declarados dentro de uma declaração de struct/union/enum estão no mesmo escopo que a declaração da struct (exceto que os membros de dados estão em seu próprio [espaço de nomes de membro](<#/doc/language/name_space>)):
```c
    struct foo {
        struct baz {};
        enum color {RED, BLUE};
    };
    struct baz b; // baz está em escopo
    enum color x = RED; // color e RED estão em escopo
```

### Referências

*   Padrão C23 (ISO/IEC 9899:2024):
    *   6.2.1 Escopos de identificadores, nomes de tipo e literais compostos (p: TBD)
*   Padrão C17 (ISO/IEC 9899:2018):
    *   6.2.1 Escopos de identificadores (p: 28-29)
*   Padrão C11 (ISO/IEC 9899:2011):
    *   6.2.1 Escopos de identificadores (p: 35-36)
*   Padrão C99 (ISO/IEC 9899:1999):
    *   6.2.1 Escopos de identificadores (p: 29-30)
*   Padrão C89/C90 (ISO/IEC 9899:1990):
    *   3.1.2.1 Escopos de identificadores

### Veja também

[documentação C++](<#/>) para Escopo
---