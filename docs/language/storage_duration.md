# Especificadores de classe de armazenamento

Especificam a _duração de armazenamento_ e a _ligação_ de objetos e funções:

*   `auto` \- duração automática e sem ligação
*   `register` \- duração automática e sem ligação; o endereço desta variável não pode ser obtido
*   `static` \- duração estática e ligação interna (a menos que em escopo de bloco)
*   `extern` \- duração estática e ligação externa (a menos que já declarada como interna)

*   `_Thread_local`(até C23)`thread_local`(desde C23) \- duração de armazenamento de thread

| (desde C11)

### Explicação

Especificadores de classe de armazenamento aparecem em [declarações](<#/doc/language/declarations>) e expressões de [literal composto](<#/doc/language/compound_literal>)(desde C23). No máximo um especificador pode ser usado, exceto que _Thread_local(até C23)[thread_local](<#/doc/thread/thread_local>)(desde C23) pode ser combinado com static ou extern para ajustar a ligação(desde C11). Os especificadores de classe de armazenamento determinam duas propriedades independentes dos nomes que eles declaram: _duração de armazenamento_ e _ligação_.

1) O especificador auto é permitido apenas para objetos declarados em escopo de bloco (exceto listas de parâmetros de função). Ele indica duração de armazenamento automática e sem ligação, que são os padrões para esses tipos de declarações.

2) O especificador register é permitido apenas para objetos declarados em escopo de bloco, incluindo listas de parâmetros de função. Ele indica duração de armazenamento automática e sem ligação (que é o padrão para esses tipos de declarações), mas adicionalmente sugere ao otimizador que armazene o valor desta variável em um registrador da CPU, se possível. Independentemente de esta otimização ocorrer ou não, variáveis declaradas register não podem ser usadas como argumentos para o [operador de endereço](<#/doc/language/operator_member_access>), não podem usar [`_Alignas`](<#/doc/language/alignas>)(até C23)[`alignas`](<#/doc/language/alignas>)(desde C23)(desde C11), e arrays register não são conversíveis para ponteiros.

3) O especificador static especifica tanto duração de armazenamento estática (a menos que combinado com _Thread_local)(desde C11) quanto ligação interna (a menos que usado em escopo de bloco). Ele pode ser usado com funções em escopo de arquivo e com variáveis em escopo de arquivo e de bloco, mas não em listas de parâmetros de função.

4) O especificador extern especifica duração de armazenamento estática (a menos que combinado com _Thread_local(até C23)[thread_local](<#/doc/thread/thread_local>)(desde C23))(desde C11) e ligação externa. Ele pode ser usado com declarações de função e objeto tanto em escopo de arquivo quanto de bloco (excluindo listas de parâmetros de função). Se extern aparecer em uma redeclaração de um identificador que já foi declarado com ligação interna, a ligação permanece interna. Caso contrário (se a declaração anterior era externa, sem ligação, ou não está em escopo), a ligação é externa.

5) _Thread_local(até C23)[thread_local](<#/doc/thread/thread_local>)(desde C23) indica _duração de armazenamento de thread_. Não pode ser usado com declarações de função. Se for usado em uma declaração de um objeto, deve estar presente em todas as declarações do mesmo objeto. Se for usado em uma declaração de escopo de bloco, deve ser combinado com static ou extern para decidir a ligação. | (desde C11)

Se nenhum especificador de classe de armazenamento for fornecido, os padrões são:

*   `extern` para todas as funções
*   `extern` para objetos em escopo de arquivo
*   `auto` para objetos em escopo de bloco

Para qualquer struct ou union declarada com um especificador de classe de armazenamento, a duração de armazenamento (mas não a ligação) se aplica aos seus membros, recursivamente.

Declarações de função em escopo de bloco podem usar extern ou nenhuma. Declarações de função em escopo de arquivo podem usar extern ou static.

Parâmetros de função não podem usar nenhum especificador de classe de armazenamento além de register. Note que static tem um significado especial em parâmetros de função do tipo array.

### Duração de armazenamento

Todo [objeto](<#/doc/language/object>) possui uma propriedade chamada _duração de armazenamento_, que limita o [tempo de vida](<#/doc/language/lifetime>) do objeto. Existem quatro tipos de duração de armazenamento em C:

*   _**automática**_ duração de armazenamento. O armazenamento é alocado quando o [bloco](<#/doc/language/statements>) no qual o objeto foi declarado é inserido e desalocado quando é saído por qualquer meio ([goto](<#/doc/language/goto>), [return](<#/doc/language/return>), atingindo o final). Uma exceção são os [VLAs](<#/doc/language/array>); seu armazenamento é alocado quando a declaração é executada, não na entrada do bloco, e desalocado quando a declaração sai do escopo, não quando o bloco é saído(desde C99). Se o bloco for inserido recursivamente, uma nova alocação é realizada para cada nível de recursão. Todos os parâmetros de função e objetos de escopo de bloco não estáticos têm esta duração de armazenamento, assim como [literais compostos](<#/doc/language/compound_literal>) usados em escopo de bloco(até C23)
*   _**estática**_ duração de armazenamento. A duração de armazenamento é a execução completa do programa, e o valor armazenado no objeto é inicializado apenas uma vez, antes da [função main](<#/doc/language/main_function>). Todos os objetos declarados static e todos os objetos com ligação interna ou externa que não são declarados _Thread_local(até C23)[thread_local](<#/doc/thread/thread_local>)(desde C23)(desde C11) têm esta duração de armazenamento.

*   _**de thread**_ duração de armazenamento. A duração de armazenamento é a execução completa da thread na qual foi criado, e o valor armazenado no objeto é inicializado quando a thread é iniciada. Cada thread tem seu próprio objeto distinto. Se a thread que executa a expressão que acessa este objeto não for a thread que executou sua inicialização, o comportamento é definido pela implementação. Todos os objetos declarados _Thread_local(até C23)[thread_local](<#/doc/thread/thread_local>)(desde C23) têm esta duração de armazenamento.

| (desde C11)

*   _**alocada**_ duração de armazenamento. O armazenamento é alocado e desalocado sob demanda, usando funções de [alocação dinâmica de memória](<#/doc/memory>).

#### Ligação

Ligação refere-se à capacidade de um identificador (variável ou função) ser referenciado em outros escopos. Se uma variável ou função com o mesmo identificador for declarada em vários escopos, mas não puder ser referenciada de todos eles, então várias instâncias da variável são geradas. As seguintes ligações são reconhecidas:

*   _**sem ligação**_. A variável ou função pode ser referenciada apenas a partir do escopo em que está (escopo de bloco). Todas as variáveis de escopo de bloco que não são declaradas `extern` têm esta ligação, assim como todos os parâmetros de função e todos os identificadores que não são funções ou variáveis.

*   _**ligação interna**_. A variável ou função pode ser referenciada a partir de todos os escopos na unidade de tradução atual. Todas as variáveis de escopo de arquivo que são declaradas `static` ou `constexpr`(desde C23) têm esta ligação, e todas as funções de escopo de arquivo declaradas `static` (declarações de função static são permitidas apenas em escopo de arquivo).

*   _**ligação externa**_. A variável ou função pode ser referenciada a partir de quaisquer outras unidades de tradução em todo o programa. Todas as variáveis de escopo de arquivo que não são declaradas `static` ou `constexpr`(desde C23) têm esta ligação, todas as declarações de função de escopo de arquivo que não são declaradas `static`, todas as declarações de função de escopo de bloco e, adicionalmente, todas as variáveis ou funções declaradas `extern` têm esta ligação, a menos que uma declaração anterior com ligação interna seja visível naquele ponto.

Se o mesmo identificador aparecer com ligação interna e externa na mesma unidade de tradução, o comportamento é indefinido. Isso é possível quando [definições tentativas](<#/doc/language/extern>) são usadas.

#### Ligação e bibliotecas

| Esta seção está incompleta
Motivo: deveria ser uma entrada de nível superior separada em c/language em Miscelânea?

Declarações com ligação externa são comumente disponibilizadas em arquivos de cabeçalho para que todas as unidades de tradução que [#include](<#/doc/preprocessor/include>) o arquivo possam se referir ao mesmo identificador que são definidos em outro lugar.

Qualquer declaração com ligação interna que aparece em um arquivo de cabeçalho resulta em um objeto separado e distinto em cada unidade de tradução que inclui esse arquivo.

Interface da biblioteca, arquivo de cabeçalho "flib.h":
```c
    #ifndef FLIB_H
    #define FLIB_H
    void f(void);              // function declaration with external linkage
    extern int state;          // variable declaration with external linkage
    static const int size = 5; // definition of a read-only variable with internal linkage
    enum { MAX = 10 };         // constant definition
    inline int sum (int a, int b) { return a + b; } // inline function definition
    #endif // FLIB_H
```

Implementação da biblioteca, arquivo fonte "flib.c":
```c
    #include "flib.h"
    
    static void local_f(int s) {} // definition with internal linkage (only used in this file)
    static int local_state;       // definition with internal linkage (only used in this file)
    
    int state;                       // definition with external linkage (used by main.c)
    void f(void) { local_f(state); } // definition with external linkage (used by main.c)
```

Código da aplicação, arquivo fonte "main.c":
```c
    #include "flib.h"
    
    int main(void)
    {
        int x[MAX] = {size}; // uses the constant and the read-only variable
        state = 7;           // modifies state in flib.c
        f();                 // calls f() in flib.c
    }
```

|

### Palavras-chave

[`auto`](<#/doc/keyword/auto>), [`register`](<#/doc/keyword/register>), [`static`](<#/doc/keyword/static>), [`extern`](<#/doc/keyword/extern>), [`_Thread_local`](<#/doc/keyword/_Thread_local>) [`thread_local`](<#/doc/keyword/thread_local>)

### Notas

A palavra-chave _Thread_local é geralmente usada através da macro de conveniência [thread_local](<#/doc/thread/thread_local>), definida no cabeçalho [`<threads.h>`](<#/doc/thread>). | (até C23)

Os especificadores [`typedef`](<#/doc/language/typedef>) e [`constexpr`](<#/doc/language/constexpr>)(desde C23) são formalmente listados como especificadores de classe de armazenamento na gramática da linguagem C, mas não especificam armazenamento.

O especificador auto também é usado para inferência de tipo. | (desde C23)

Nomes em escopo de arquivo que são const e não extern têm ligação externa em C (como o padrão para todas as declarações de escopo de arquivo), mas ligação interna em C++.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
    
    // static storage duration
    int A;
    
    int main(void)
    {
        printf("&A = %p\n", (void*)&A);
    
        // automatic storage duration
        int A = 1;   // hides global A
        printf("&A = %p\n", (void*)&A);
    
        // allocated storage duration
        int* ptr_1 = malloc(sizeof(int));   // start allocated storage duration
        printf("address of int in allocated memory = %p\n", (void*)ptr_1);
        free(ptr_1);                        // stop allocated storage duration
    }
```

Saída possível:
```
    &A = 0x600ae4
    &A = 0x7ffefb064f5c
    address of int in allocated memory = 0x1f28c30
```

### Referências

*   Padrão C23 (ISO/IEC 9899:2024):
    *   6.2.2 Ligações de identificadores (p: 35-36)
    *   6.2.4 Duração de armazenamento de objetos (p: 36-37)
    *   6.7.1 Especificadores de classe de armazenamento (p: 97-100)
*   Padrão C17 (ISO/IEC 9899:2018):
    *   6.2.2 Ligações de identificadores (p: 29-30)
    *   6.2.4 Duração de armazenamento de objetos (p: 30)
    *   6.7.1 Especificadores de classe de armazenamento (p: 79)
*   Padrão C11 (ISO/IEC 9899:2011):
    *   6.2.2 Ligações de identificadores (p: 36-37)
    *   6.2.4 Duração de armazenamento de objetos (p: 38-39)
    *   6.7.1 Especificadores de classe de armazenamento (p: 109-110)
*   Padrão C99 (ISO/IEC 9899:1999):
    *   6.2.2 Ligações de identificadores (p: 30-31)
    *   6.2.4 Duração de armazenamento de objetos (p: 32)
    *   6.7.1 Especificadores de classe de armazenamento (p: 98-99)
*   Padrão C89/C90 (ISO/IEC 9899:1990):
    *   3.1.2.2 Ligações de identificadores
    *   3.1.2.4 Duração de armazenamento de objetos
    *   3.5.1 Especificadores de classe de armazenamento

### Veja também

[Documentação C++](<#/>) para especificadores de classe de armazenamento
---