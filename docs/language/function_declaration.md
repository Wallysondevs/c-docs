# Declarações de função

Uma declaração de função introduz um [identificador](<#/doc/language/identifier>) que designa uma função e, opcionalmente, especifica os tipos dos parâmetros da função (o _protótipo_). Declarações de função (ao contrário das [definições](<#/doc/language/function_definition>)) podem aparecer tanto no escopo de bloco quanto no escopo de arquivo.

### Sintaxe

Na [gramática de declaração](<#/doc/language/declarations>) de uma declaração de função, a sequência de especificadores de tipo, possivelmente modificada pelo declarador, designa o _tipo de retorno_ (que pode ser qualquer tipo diferente de array ou tipo de função), e o declarador tem uma das três formas:

---
noptr-declarator `(` parameter-list `)` attr-spec-seq(optional) | (1) |
noptr-declarator `(` identifier-list `)` attr-spec-seq(optional) | (2) | (até C23)
noptr-declarator `(` `)` attr-spec-seq(optional) | (3) |

onde

- **noptr-declarator** — qualquer [declarador](<#/doc/language/declarations>) exceto um declarador de ponteiro não-parentesizado. O identificador contido neste declarador é o identificador que se torna o designador da função.
- **parameter-list** — ou a palavra-chave única void ou uma lista de _parâmetros_ separada por vírgulas, que pode terminar com um [parâmetro de reticências](<#/doc/language/variadic>)
- **identifier-list** — lista de identificadores separada por vírgulas, somente possível se este declarador for usado como parte de uma [definição de função](<#/doc/language/function_definition>) de estilo antigo
- **attr-spec-seq** — (C23)uma lista opcional de [atributos](<#/doc/language/attributes>), aplicada ao tipo da função

1) Declaração de função de estilo novo (C89). Esta declaração introduz o próprio designador da função e também serve como um protótipo de função para quaisquer futuras [expressões de chamada de função](<#/doc/language/operator_other>), forçando conversões de expressões de argumento para os tipos de parâmetro declarados e verificações em tempo de compilação para o número de argumentos.
```c
    int max(int a, int b); // declaration
    int n = max(12.01, 3.14); // OK, conversion from double to int
```

2) (até C23) Definição de função de estilo antigo (K&R). Esta declaração não introduz um protótipo e quaisquer futuras [expressões de chamada de função](<#/doc/language/operator_other>) realizarão promoções de argumento padrão e invocarão comportamento indefinido se o número de argumentos não corresponder ao número de parâmetros.
```c
    int max(a, b)
        int a, b; // definition expects ints; the second call is undefined
    {
        return a > b ? a : b;
    }

    int n = max(true, (char)'a'); // calls max with two int args (after promotions)

    int n = max(12.01f, 3.14); // calls max with two double args (after promotions)
```

3) Declaração de função sem protótipo. Esta declaração não introduz um protótipo (até C23). Uma declaração de função de estilo novo equivalente à lista de parâmetros void (desde C23).

### Explicação

O tipo de retorno da função, determinado pelo especificador de tipo em especificadores-e-qualificadores e possivelmente modificado pelo declarador como de costume em [declarações](<#/doc/language/declarations>), deve ser um tipo de objeto não-array ou o tipo void. Se a declaração de função não for uma definição, o tipo de retorno pode ser [incompleto](<#/doc/language/compatible_type>). O tipo de retorno não pode ser cvr-qualificado: qualquer tipo de retorno qualificado é ajustado para sua versão não qualificada para o propósito de construir o tipo da função.
```c
    void f(char *s);                    // return type is void
    int sum(int a, int b);              // return type of sum is int.
    int (*foo(const void *p))[3];       // return type is pointer to array of 3 int

    double const bar(void);             // declares function of type double(void)
    double (*barp)(void) = bar;         // OK: barp is a pointer to double(void)
    double const (*barpc)(void) = barp; // OK: barpc is also a pointer to double(void)
```

Declaradores de função podem ser combinados com outros declaradores, desde que possam compartilhar seus especificadores de tipo e qualificadores
```c
    int f(void), *fip(), (*pfi)(), *ap[3]; // declares two functions and two objects
    inline int g(int), n; // Error: inline qualifier is for functions only
    typedef int array_t[3];
    array_t a, h(); // Error: array type cannot be a return type for a function
```

Se uma declaração de função aparecer fora de qualquer função, o identificador que ela introduz tem [escopo de arquivo](<#/doc/language/scope>) e [ligação externa](<#/doc/language/storage_duration>), a menos que `static` seja usado ou uma declaração estática anterior seja visível. Se a declaração ocorrer dentro de outra função, o identificador tem escopo de bloco (e também ligação interna ou externa).
```c
    int main(void)
    {
        int f(int); // external linkage, block scope
        f(1); // definition needs to be available somewhere in the program
    }
```

Os parâmetros em uma declaração que não faz parte de uma [definição de função](<#/doc/language/function_definition>) (até C23) não precisam ser nomeados:
```c
    int f(int, int); // declaration
    // int f(int, int) { return 7; } // Error: parameters must be named in definitions
    // Esta definição é permitida desde C23
```

Cada parâmetro em uma lista de parâmetros é uma [declaração](<#/doc/language/declarations>) que introduz uma única variável, com as seguintes propriedades adicionais:

  * o identificador no declarador é opcional (exceto se esta declaração de função for parte de uma definição de função) (até C23)

```c
    int f(int, double); // OK
    int g(int a, double b); // also OK
    // int f(int, double) { return 1; } // Error: definition must name parameters
    // Esta definição é permitida desde C23
```

  * o único [especificador de classe de armazenamento](<#/doc/language/storage_duration>) permitido para parâmetros é `register`, e ele é ignorado em declarações de função que não são definições

```c
    int f(static int x); // Error
    int f(int [static 10]); // OK (o índice de array static não é um especificador de classe de armazenamento)
```

  * qualquer parâmetro de tipo array é ajustado para o tipo de ponteiro correspondente, que pode ser qualificado se houver qualificadores entre os colchetes do declarador de array (desde C99)

```c
    int f(int[]); // declara int f(int*)
    int g(const int[10]); // declara int g(const int*)
    int h(int[const volatile]); // declara int h(int * const volatile)
    int x(int[*]); // declara int x(int*)
```

  * qualquer parâmetro de tipo função é ajustado para o tipo de ponteiro correspondente

```c
    int f(char g(double)); // declara int f(char (*g)(double))
    int h(int(void)); // declara int h(int (*)(void))
```

  * a lista de parâmetros pode terminar com `, ...` ou ser `...` (desde C23), veja [funções variádicas](<#/doc/language/variadic>) para detalhes.

```c
    int f(int, ...);
```

  * parâmetros não podem ter o tipo void (mas podem ter o tipo ponteiro para void). A lista de parâmetros especial que consiste inteiramente na palavra-chave void é usada para declarar funções que não recebem parâmetros.

```c
    int f(void); // OK
    int g(void x); // Error
```

  * qualquer identificador que aparece em uma lista de parâmetros que poderia ser tratado como um nome de typedef ou como um nome de parâmetro é tratado como um nome de typedef: int f([size_t](<#/doc/types/size_t>), [uintptr_t](<#/doc/types/integer>)) é analisado como um declarador de estilo novo para uma função que recebe dois parâmetros sem nome do tipo size_t e uintptr_t, não um declarador de estilo antigo que inicia a definição de uma função que recebe dois parâmetros nomeados "size_t" e "uintptr_t"
  * parâmetros podem ter tipo incompleto e podem usar a notação VLA [*] (desde C99) (exceto que em uma [definição de função](<#/doc/language/function_definition>), os tipos de parâmetro após o ajuste de array-para-ponteiro e função-para-ponteiro devem ser completos)

[Sequências de especificadores de atributo](<#/doc/language/attributes>) também podem ser aplicadas a parâmetros de função. | (desde C23)

Veja [operador de chamada de função](<#/doc/language/operator_other>) para outros detalhes sobre a mecânica de uma chamada de função e [return](<#/doc/language/return>) para retornar de funções.

### Notas

Ao contrário do C++, os declaradores f() e f(void) têm significados diferentes: o declarador f(void) é um declarador de estilo novo (protótipo) que declara uma função que não recebe parâmetros. O declarador f() é um declarador que declara uma função que recebe um número _não especificado_ de parâmetros (a menos que usado em uma definição de função)
```c
    int f(void); // declaração: não recebe parâmetros
    int g(); // declaração: recebe parâmetros desconhecidos

    int main(void) {
        f(1); // erro em tempo de compilação
        g(2); // comportamento indefinido
    }

    int f(void) { return 1; } // definição real
    int g(a,b,c,d) int a,b,c,d; { return 2; } // definição real
```
| (até C23)

Ao contrário de uma [definição de função](<#/doc/language/function_definition>), a lista de parâmetros pode ser herdada de um typedef
```c
    typedef int p(int q, int r); // p é um tipo de função int(int, int)
    p f; // declara int f(int, int)
```

No C89, especificadores-e-qualificadores era opcional, e se omitido, o tipo de retorno da função assumia int por padrão (possivelmente alterado pelo declarador).
```c
    *f() { // função que retorna int*
       return NULL;
    }
```
| (até C99)

### Relatórios de defeito

Os seguintes relatórios de defeito que alteram o comportamento foram aplicados retroativamente a padrões C publicados anteriormente.

DR | Aplicado a | Comportamento conforme publicado | Comportamento correto
[DR 423](<https://www.open-std.org/jtc1/sc22/wg14/www/docs/n2396.htm#dr_423>) | C89 | o tipo de retorno poderia ser qualificado | o tipo de retorno é implicitamente desqualificado

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 6.7.6.3 Declaradores de função (incluindo protótipos) (p: 96-98)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 6.7.6.3 Declaradores de função (incluindo protótipos) (p: 133-136)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 6.7.5.3 Declaradores de função (incluindo protótipos) (p: 118-121)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 3.5.4.3 Declaradores de função (incluindo protótipos)

### Veja também

[Documentação C++](<#/>) para Declaração de função
---