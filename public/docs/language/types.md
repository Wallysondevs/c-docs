# Tipo

(Veja também [tipos aritméticos](<#/doc/language/arithmetic_types>) para detalhes sobre a maioria dos tipos embutidos e [a lista de utilitários relacionados a tipos](<#/doc/types>) fornecidos pela biblioteca C.)  
  
[Objetos](<#/doc/language/object>), [funções](<#/doc/language/functions>) e [expressões](<#/doc/language/expressions>) possuem uma propriedade chamada _tipo_, que determina a interpretação do valor binário armazenado em um objeto ou avaliado pela expressão.

### Classificação de tipos

O sistema de tipos C consiste nos seguintes tipos:

  * o tipo void
  * tipos básicos

    

  * o tipo char
  * tipos inteiros com sinal

    

  * padrão: signed char, short, int, long, long long (desde C99)

    

    

  * precisos em bits: _BitInt(N) onde N é uma expressão constante inteira que especifica o número de bits usados para representar o tipo, incluindo o bit de sinal. Cada valor de N designa um tipo distinto.

| (desde C23)  
  
    

    

  * estendidos: definidos pela implementação, ex: __int128

| (desde C99)  
  
    

  * tipos inteiros sem sinal

    

  * padrão: _Bool, (desde C99) unsigned char, unsigned short, unsigned int, unsigned long, unsigned long long (desde C99)

    

    

  * precisos em bits: unsigned _BitInt(N) onde `N` é uma expressão constante inteira que especifica o número de bits usados para representar o tipo. Cada valor de `N` designa um tipo distinto. Esta categoria inclui o tipo unsigned _BitInt(1) que não possui um tipo inteiro com sinal preciso em bits correspondente.

| (desde C23)  
  
    

    

  * estendidos: definidos pela implementação, ex: __uint128

| (desde C99)  
  
    

  * tipos de ponto flutuante

    

  * tipos de ponto flutuante real: float, double, long double

    

    

  * tipos de ponto flutuante real decimal: _Decimal32, _Decimal64, _Decimal128

| (desde C23)  
  
    

    

  * tipos complexos: float _Complex, double _Complex, long double _Complex
  * tipos imaginários: float _Imaginary, double _Imaginary, long double _Imaginary

| (desde C99)  
  
  * [tipos enumerados](<#/doc/language/enum>)

  * tipos derivados

    

  * [tipos array](<#/doc/language/array>)
  * [tipos estrutura](<#/doc/language/struct>)
  * [tipos união](<#/doc/language/union>)
  * [tipos função](<#/doc/language/functions>)
  * [tipos ponteiro](<#/doc/language/pointer>)

    

  * [tipos atômicos](<#/doc/language/atomic>)

| (desde C11)  
  
Para cada tipo listado acima, várias versões qualificadas de seu tipo podem existir, correspondendo às combinações de um, dois ou todos os três qualificadores [`const`](<#/doc/language/const>), [`volatile`](<#/doc/language/volatile>) e [`restrict`](<#/doc/language/restrict>) (onde permitido pela semântica do qualificador).

#### Grupos de tipos

  * _tipos de objeto_ : todos os tipos que não são tipos de função
  * _tipos de caractere_ : char, signed char, unsigned char
  * _tipos inteiros_ : char, tipos inteiros com sinal, tipos inteiros sem sinal, tipos enumerados
  * _tipos reais_ : tipos inteiros e tipos de ponto flutuante real
  * [tipos aritméticos](<#/doc/language/arithmetic_types>): tipos inteiros e tipos de ponto flutuante
  * _tipos escalares_ : tipos aritméticos, tipos ponteiro e [nullptr_t](<#/doc/types/nullptr_t>) (desde C23)
  * _tipos agregados_ : tipos array e tipos estrutura
  * _tipos de declarador derivado_ : tipos array, tipos função e tipos ponteiro

Construir um tipo de objeto completo de tal forma que o número de bytes em sua representação de objeto não seja representável no tipo [size_t](<#/doc/types/size_t>) (ou seja, o tipo de resultado do operador [`sizeof`](<#/doc/language/sizeof>)), incluindo a formação de tal tipo VLA em tempo de execução, (desde C99) é comportamento indefinido.

### Tipos compatíveis

Em um programa C, as declarações que se referem ao mesmo objeto ou função em _unidades de tradução diferentes_ não precisam usar o mesmo tipo. Elas apenas precisam usar tipos suficientemente semelhantes, formalmente conhecidos como _tipos compatíveis_. O mesmo se aplica a chamadas de função e acessos a lvalue; os tipos de argumento devem ser _compatíveis_ com os tipos de parâmetro e o tipo da expressão lvalue deve ser _compatível_ com o tipo de objeto que está sendo acessado.

Os tipos `T` e `U` são compatíveis, se

  * eles são do mesmo tipo (mesmo nome ou aliases introduzidos por um [`typedef`](<#/doc/language/typedef>))
  * eles são versões cvr-qualificadas identicamente de tipos não qualificados compatíveis
  * eles são tipos ponteiro e apontam para tipos compatíveis
  * eles são tipos array, e

    

  * seus tipos de elemento são compatíveis, e
  * se ambos tiverem tamanho constante, esse tamanho é o mesmo. Nota: arrays de limite desconhecido são compatíveis com qualquer array de tipo de elemento compatível. VLA é compatível com qualquer array de tipo de elemento compatível. (desde C99)

  * eles são ambos tipos estrutura/união/enumeração, e

    

  * (C99) se um for declarado com uma tag, o outro também deve ser declarado com a mesma tag.
  * se ambos forem tipos completos, seus membros devem corresponder exatamente em número, ser declarados com tipos compatíveis e ter nomes correspondentes.
  * adicionalmente, se forem enumerações, os membros correspondentes também devem ter os mesmos valores.
  * adicionalmente, se forem estruturas ou uniões,

    

  * Os membros correspondentes devem ser declarados na mesma ordem (apenas estruturas)
  * Os [campos de bits](<#/doc/language/bit_field>) correspondentes devem ter as mesmas larguras.

  * um é um tipo enumerado e o outro é o tipo subjacente dessa enumeração
  * eles são tipos de função, e

    

  * seus tipos de retorno são compatíveis
  * ambos usam listas de parâmetros, o número de parâmetros (incluindo o uso das reticências) é o mesmo, e o parâmetro correspondente, após aplicar os ajustes de tipo array-para-ponteiro e função-para-ponteiro e após remover os qualificadores de nível superior, têm tipos compatíveis

    

  * um é uma definição de estilo antigo (sem parâmetros), o outro tem uma lista de parâmetros, a lista de parâmetros não usa reticências e cada parâmetro é compatível (após ajuste do tipo de parâmetro de função) com o parâmetro de estilo antigo correspondente após as promoções de argumento padrão
  * uma é uma declaração de estilo antigo (sem parâmetros), a outra tem uma lista de parâmetros, a lista de parâmetros não usa reticências, e todos os parâmetros (após ajuste do tipo de parâmetro de função) não são afetados pelas promoções de argumento padrão

| (até C23)  
  
O tipo char não é compatível com signed char e não é compatível com unsigned char.

Se duas declarações se referem ao mesmo objeto ou função e não usam tipos compatíveis, o comportamento do programa é indefinido.
```c
    // Unidade de Tradução 1
    struct S { int a; };
    extern struct S *x; // compatível com o x da TU2, mas não com o x da TU3
    
    // Unidade de Tradução 2
    struct S;
    extern struct S *x; // compatível com ambos os x's
    
    // Unidade de Tradução 3
    struct S { float a; };
    extern struct S *x; // compatível com o x da TU2, mas não com o x da TU1
    
    // o comportamento é indefinido
```
```c
    // Unidade de Tradução 1
    #include <stdio.h>
    
    struct s { int i; }; // compatível com o s da TU3, mas não com o da TU2
    extern struct s x = {0}; // compatível com o x da TU3
    extern void f(void); // compatível com o f da TU2
    
    int main()
    {
        f();
        return x.i;
    }
    
    // Unidade de Tradução 2
    struct s { float f; }; // compatível com o s da TU4, mas não com o s da TU1
    extern struct s y = {3.14}; // compatível com o y da TU4
    void f() // compatível com o f da TU1
    {
        return;
    }
    
    // Unidade de Tradução 3
    struct s { int i; }; // compatível com o s da TU1, mas não com o s da TU2
    extern struct s x; // compatível com o x da TU1
    
    // Unidade de Tradução 4
    struct s { float f; }; // compatível com o s da TU2, mas não com o s da TU1
    extern struct s y; // compatível com o y da TU2
    
    // o comportamento é bem definido: apenas múltiplas declarações
    // de objetos e funções devem ter tipos compatíveis, não os próprios tipos
```

Nota: C++ não possui o conceito de tipos compatíveis. Um programa C que declara dois tipos que são compatíveis, mas não idênticos em diferentes unidades de tradução, não é um programa C++ válido.

### Tipos compostos

Um tipo composto pode ser construído a partir de dois tipos que são compatíveis; é um tipo que é compatível com ambos os dois tipos e satisfaz as seguintes condições:

  * Se ambos os tipos são tipos array, as seguintes regras são aplicadas:

    

  * Se um tipo é um array de tamanho constante conhecido, o tipo composto é um array desse tamanho.

    

  * Caso contrário, se um tipo é um VLA cujo tamanho é especificado por uma expressão que não é avaliada, um programa que necessita do tipo composto de ambos os tipos tem comportamento indefinido.
  * Caso contrário, se um tipo é um VLA cujo tamanho é especificado, o tipo composto é um VLA desse tamanho.
  * Caso contrário, se um tipo é um VLA de tamanho não especificado, o tipo composto é um VLA de tamanho não especificado.

| (desde C99)  
  
    

  * Caso contrário, ambos os tipos são arrays de tamanho desconhecido e o tipo composto é um array de tamanho desconhecido.

    O tipo de elemento do tipo composto é o tipo composto dos dois tipos de elemento.

  * Se apenas um tipo é um tipo de função com uma lista de tipos de parâmetro (um protótipo de função), o tipo composto é um protótipo de função com a lista de tipos de parâmetro.

| (até C23)  
  
  * Se ambos os tipos são tipos de função com listas de tipos de parâmetro, o tipo de cada parâmetro na lista de tipos de parâmetro composta é o tipo composto dos parâmetros correspondentes.

Essas regras se aplicam recursivamente aos tipos dos quais os dois tipos são derivados.
```c
    // Dadas as duas declarações de escopo de arquivo a seguir:
    int f(int (*)(), double (*)[3]);
    int f(int (*)(char *), double (*)[]); // C23: Erro: tipos conflitantes para 'f'
    // O tipo composto resultante para a função é:
    int f(int (*)(char *), double (*)[3]);
```

Para um identificador com [ligação](<#/doc/language/storage_duration>) interna ou externa declarado em um escopo no qual uma declaração anterior desse identificador é visível, se a declaração anterior especificar ligação interna ou externa, o tipo do identificador na declaração posterior torna-se o tipo composto.

### Tipos incompletos

Um tipo incompleto é um tipo de objeto que não possui informações suficientes para determinar o tamanho dos objetos desse tipo. Um tipo incompleto pode ser completado em algum ponto na unidade de tradução.

Os seguintes tipos são incompletos:

  * o tipo void. Este tipo não pode ser completado.
  * tipo array de tamanho desconhecido. Ele pode ser completado por uma declaração posterior que especifica o tamanho.

```c
    extern char a[]; // o tipo de a é incompleto (isso tipicamente aparece em um cabeçalho)
    char a[10];      // o tipo de a agora está completo (isso tipicamente aparece em um arquivo fonte)
```

  * tipo estrutura ou união de conteúdo desconhecido. Ele pode ser completado por uma declaração da mesma estrutura ou união que define seu conteúdo mais tarde no mesmo escopo.

```c
    struct node
    {
        struct node* next; // struct node é incompleto neste ponto
    }; // struct node está completo neste ponto
```

### Nomes de tipos

Um tipo pode precisar ser nomeado em contextos diferentes da [declaração](<#/doc/language/declarations>). Nessas situações, usa-se _nome de tipo_, que é, gramaticalmente, exatamente o mesmo que uma lista de _especificadores de tipo_ e _qualificadores de tipo_, seguida pelo _declarador_ (veja [declarações](<#/doc/language/declarations>)) como seria usado para declarar um único objeto ou função desse tipo, exceto que o identificador é omitido:
```c
    int n; // declaração de um int
    sizeof(int); // uso de nome de tipo
    
    int *a[3]; // declaração de um array de 3 ponteiros para int
    sizeof(int *[3]); // uso de nome de tipo
    
    int (*p)[3]; // declaração de um ponteiro para array de 3 int
    sizeof(int (*)[3]); // uso de nome de tipo
    
    int (*a)[*] // declaração de ponteiro para VLA (em um parâmetro de função)
    sizeof(int (*)[*]) // uso de nome de tipo (em um parâmetro de função)
    
    int *f(void); // declaração de função
    sizeof(int *(void)); // uso de nome de tipo
    
    int (*p)(void); // declaração de ponteiro para função
    sizeof(int (*)(void)); // uso de nome de tipo
    
    int (*const a[])(unsigned int, ...) = {0}; // array de ponteiros para funções
    sizeof(int (*const [])(unsigned int, ...)); // uso de nome de tipo
```

Exceto que os parênteses redundantes em torno do identificador são significativos em um nome de tipo e representam "função sem especificação de parâmetro":
```c
    int (n); // declara n do tipo int
    sizeof(int ()); // usa o tipo "função que retorna int"
```

Nomes de tipos são usados nas seguintes situações:

  * [cast](<#/doc/language/cast>)
  * [sizeof](<#/doc/language/sizeof>)

  * [literal composto](<#/doc/language/compound_literal>)

| (desde C99)  
  
  * [seleção genérica](<#/doc/language/generic>)
  * [`_Alignof`](<#/doc/language/alignof>) (até C23) [`alignof`](<#/doc/language/alignof>) (desde C23)
  * [`_Alignas`](<#/doc/language/alignas>) (até C23) [`alignas`](<#/doc/language/alignas>) (desde C23)
  * [`_Atomic`](<#/doc/language/atomic>) (quando usado como um especificador de tipo)

| (desde C11)  
  
Um nome de tipo pode introduzir um novo tipo:
```c
    void* p = (void*)(struct X { int i; } *)0;
    // nome de tipo "struct X {int i;}*" usado na expressão de cast
    // introduz o novo tipo "struct X"
    struct X x = {1}; // struct X agora está no escopo
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 6.2.5 Tipos (p: TBD)

    

  * 6.2.6 Representações de tipos (p: TBD)

    

  * 6.2.7 Tipo compatível e tipo composto (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 6.2.5 Tipos (p: 31-33)

    

  * 6.2.6 Representações de tipos (p: 31-35)

    

  * 6.2.7 Tipo compatível e tipo composto (p: 35-36)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 6.2.5 Tipos (p: 39-43)

    

  * 6.2.6 Representações de tipos (p: 44-46)

    

  * 6.2.7 Tipo compatível e tipo composto (p: 47-48)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 6.2.5 Tipos (p: 33-37)

    

  * 6.2.6 Representações de tipos (p: 37-40)

    

  * 6.2.7 Tipo compatível e tipo composto (p: 40-41)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 3.1.2.5 Tipos

    

  * 3.1.2.6 Tipo compatível e tipo composto

### Veja também

[documentação C++](<#/>) para Tipo  
---