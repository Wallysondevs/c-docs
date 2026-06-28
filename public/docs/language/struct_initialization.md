# Inicialização de struct e union

Ao [inicializar](<#/doc/language/initialization>) um objeto do tipo [struct](<#/doc/language/struct>) ou [union](<#/doc/language/union>), o inicializador deve ser uma lista de inicializadores não vazia (até C23), delimitada por chaves e separada por vírgulas, para os membros:

---
`=` `{` expression `,` `...` `}` | (1) | (até C99)
`=` `{` designator(opcional) expression `,` `...` `}` | (2) | (desde C99)
`=` `{` `}` | (3) | (desde C23)

onde o designador é uma sequência (separada por espaços em branco ou adjacente) de designadores de membro individuais na forma `.` member e [designadores de array](<#/doc/language/array_initialization>) na forma `[` index `]`.

Todos os membros que não são inicializados explicitamente são [inicializados vazios](<#/doc/language/initialization>).

### Explicação

Ao inicializar uma [union](<#/doc/language/union>), a lista de inicializadores deve ter apenas um membro, que inicializa o primeiro membro da union, a menos que um inicializador designado seja usado (desde C99).
```c
    union { int x; char c[4]; }
      u = {1},           // torna u.x ativo com o valor 1
     u2 = { .c={'\1'} }; // torna u2.c ativo com o valor {'\1','\0','\0','\0'}
```

Ao inicializar uma [struct](<#/doc/language/struct>), o primeiro inicializador na lista inicializa o primeiro membro declarado (a menos que um designador seja especificado) (desde C99), e todos os inicializadores subsequentes sem designadores (desde C99) inicializam os membros da struct declarados após aquele inicializado pela expressão anterior.
```c
    struct point {double x,y,z;} p = {1.2, 1.3}; // p.x=1.2, p.y=1.3, p.z=0.0
    div_t answer = {.quot = 2, .rem = -1 };      // a ordem dos elementos em div_t pode variar
```

Um designador faz com que o inicializador seguinte inicialize o membro da struct descrito pelo designador. A inicialização então continua para frente na ordem de declaração, começando com o próximo elemento declarado após aquele descrito pelo designador.
```c
    struct {int sec,min,hour,day,mon,year;} z
       = {.day=31,12,2014,.sec=30,15,17}; // inicializa z para {30,15,17,31,12,2014}
```

| (desde C99)

É um erro fornecer mais inicializadores do que membros.

### Inicialização aninhada

Se os membros da struct ou union forem arrays, structs ou unions, os inicializadores correspondentes na lista de inicializadores delimitada por chaves são quaisquer inicializadores válidos para esses membros, exceto que suas chaves podem ser omitidas da seguinte forma:

Se o inicializador aninhado começar com uma chave de abertura, todo o inicializador aninhado até sua chave de fechamento inicializa o objeto membro correspondente. Cada chave de abertura esquerda estabelece um novo _objeto atual_. Os membros do objeto atual são inicializados em sua ordem natural, a menos que designadores sejam usados (desde C99): elementos de array em ordem de subscrito, membros de struct em ordem de declaração, apenas o primeiro membro declarado de qualquer union. Os subobjetos dentro do objeto atual que não são explicitamente inicializados pela chave de fechamento são [inicializados vazios](<#/doc/language/initialization>).
```c
    struct example {
        struct addr_t {
           uint32_t port;
        } addr;
        union {
           uint8_t a8[4];
           uint16_t a16[2];
        } in_u;
    };
    struct example ex = { // início da lista de inicializadores para struct example
                         { // início da lista de inicializadores para ex.addr
                            80 // inicializa o único membro da struct
                         }, // fim da lista de inicializadores para ex.addr
                         { // início da lista de inicializadores para ex.in_u
                            {127,0,0,1} // inicializa o primeiro elemento da union
                         } };
```

Se o inicializador aninhado não começar com uma chave de abertura, apenas inicializadores suficientes da lista são usados para contabilizar os elementos ou membros do array, struct ou union membro; quaisquer inicializadores restantes são deixados para inicializar o próximo membro da struct:
```c
    struct example ex = {80, 127, 0, 0, 1}; // 80 inicializa ex.addr.port
                                            // 127 inicializa ex.in_u.a8[0]
                                            // 0 inicializa ex.in_u.a8[1]
                                            // 0 inicializa ex.in_u.a8[2]
                                            // 1 inicializa ex.in_u.a8[3]
```

Quando os designadores são aninhados, os designadores para os membros seguem os designadores para as structs/unions/arrays que os contêm. Dentro de qualquer lista de inicializadores aninhada entre colchetes, o designador mais externo refere-se ao _objeto atual_ e seleciona o subobjeto a ser inicializado apenas dentro do _objeto atual_.
```c
    struct example ex2 = { // o objeto atual é ex2, os designadores são para membros de example
                           .in_u.a8[0]=127, 0, 0, 1, .addr=80}; 
    struct example ex3 = {80, .in_u={ // muda o objeto atual para a union ex.in_u
                               127,
                               .a8[2]=1 // este designador refere-se ao membro de in_u
                          } };
```

Se qualquer subobjeto for explicitamente inicializado duas vezes (o que pode acontecer quando designadores são usados), o inicializador que aparece mais tarde na lista é o que é usado (o inicializador anterior pode não ser avaliado):
```c
    struct {int n;} s = {printf("a\n"), // isso pode ser impresso ou ignorado
                         .n=printf("b\n")}; // sempre impresso
```

Embora quaisquer subobjetos não inicializados sejam inicializados implicitamente, a inicialização implícita de um subobjeto nunca substitui a inicialização explícita do mesmo subobjeto se ela apareceu anteriormente na lista de inicializadores (escolha clang para observar a saída correta): Execute este código
```c
    #include <stdio.h>
    typedef struct { int k; int l; int a[2]; } T;
    typedef struct { int i;  T t; } S;
    T x = {.l = 43, .k = 42, .a[1] = 19, .a[0] = 18 };
     // x inicializado para {42, 43, {18, 19} }
    int main(void)
    {
        S l = { 1,          // inicializa l.i para 1
               .t = x,      // inicializa l.t para {42, 43, {18, 19} }
               .t.l = 41,   // muda l.t para {42, 41, {18, 19} }
               .t.a[1] = 17 // muda l.t para {42, 41, {18, 17} }
              };
        printf("l.t.k is %d\n", l.t.k); // .t = x define l.t.k para 42 explicitamente
                                        // .t.l = 41 zeraria l.t.k implicitamente
    }
```

Saída:
```
    l.t.k is 42
```

No entanto, quando um inicializador começa com uma chave de abertura esquerda, seu _objeto atual_ é totalmente reinicializado e quaisquer inicializadores explícitos anteriores para qualquer um de seus subobjetos são ignorados:
```c
    struct fred { char s[4]; int n; };
    struct fred x[ ] = { { { "abc" }, 1 }, // inicializa x[0] para { {'a','b','c','\0'}, 1 }
                          [0].s[0] = 'q'   // muda x[0] para { {'q','b','c','\0'}, 1 }
                       };
    struct fred y[ ] = { { { "abc" }, 1 }, // inicializa y[0] para { {'a','b','c','\0'}, 1 }
                         [0] = { // o objeto atual é agora o objeto y[0] inteiro
                                 .s[0] = 'q' 
                                } // substitui y[0] por { {'q','\0','\0','\0'}, 0 }
                        };
```

| (desde C99)

### Notas

A lista de inicializadores pode ter uma vírgula final, que é ignorada.
```c
    struct {double x,y;} p = {1.0,
                              2.0, // vírgula final OK
                              };
```

Em C, a lista de inicializadores entre chaves não pode ser vazia (note que C++ permite listas vazias, e também note que uma [struct](<#/doc/language/struct>) em C não pode ser vazia): | (até C23)
A lista de inicializadores pode ser vazia em C, assim como em C++: | (desde C23)
```c
    struct {int n;} s = {0}; // OK
    struct {int n;} s = {}; // Erro até C23: lista de inicializadores não pode ser vazia
                            // OK desde C23: s.n é inicializado para 0
    struct {} s = {}; // Erro: struct não pode ser vazia
```

Toda expressão na lista de inicializadores deve ser uma [expressão constante](<#/doc/language/constant_expression>) ao inicializar agregados de qualquer duração de armazenamento. | (até C99)
Assim como em todas as outras [inicializações](<#/doc/language/initialization>), toda expressão na lista de inicializadores deve ser uma [expressão constante](<#/doc/language/constant_expression>) ao inicializar agregados com [duração de armazenamento](<#/doc/language/storage_duration>) estática ou thread-local (desde C11):
```c
    static struct {char* p} s = {malloc(1)}; // erro
```

A [ordem de avaliação](<#/doc/language/eval_order>) das subexpressões em qualquer inicializador é sequenciada de forma indeterminada (mas não em C++ desde C++11):
```c
    int n = 1;
    struct {int x,y;} p = {n++, n++}; // não especificado, mas comportamento bem definido:
                                      // n é incrementado duas vezes em ordem arbitrária
                                      // p igual a {1,2} e {2,1} são ambos válidos
```

| (desde C99)

### Exemplo

| Esta seção está incompleta
Razão: mais exemplos práticos, talvez inicializar algumas structs de socket

Execute este código
```c
    #include <stdio.h>
    #include <time.h>
     
    int main(void)
    {
        char buff[70];
        // inicializadores designados simplificam o uso de structs cuja
        // ordem dos membros é não especificada
        struct tm my_time = { .tm_year=2012-1900, .tm_mon=9, .tm_mday=9,
                              .tm_hour=8, .tm_min=10, .tm_sec=20 };
        strftime(buff, sizeof buff, "%A %c", &my_time);
        puts(buff);
    }
```

Saída possível:
```
    Sunday Sun Oct  9 08:10:20 2012
```

### Referências

  * C17 standard (ISO/IEC 9899:2018):

    

  * 6.7.9/12-39 Initialization (p: 101-105)

  * C11 standard (ISO/IEC 9899:2011):

    

  * 6.7.9/12-38 Initialization (p: 140-144)

  * C99 standard (ISO/IEC 9899:1999):

    

  * 6.7.8/12-38 Initialization (p: 126-130)

  * C89/C90 standard (ISO/IEC 9899:1990):

    

  * 6.5.7 Initialization

### Veja também

[Documentação C++](<#/>) para Inicialização de agregado
---