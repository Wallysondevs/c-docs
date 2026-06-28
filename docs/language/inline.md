# especificador de função inline

Declara uma [função inline](<https://en.wikipedia.org/wiki/inline_function> "enwiki:inline function").

### Sintaxe

---
inline function_declaration | | (desde C99)

### Explicação

A intenção do especificador `inline` é servir como uma dica para o compilador realizar otimizações, como [inlining de função](<https://en.wikipedia.org/wiki/inline_expansion> "enwiki:inline expansion"), que geralmente exigem que a definição de uma função seja visível no local da chamada. Os compiladores podem (e geralmente o fazem) ignorar a presença ou ausência do especificador `inline` para fins de otimização.

Se o compilador realiza o inlining de função, ele substitui uma chamada dessa função pelo seu corpo, evitando a sobrecarga de uma chamada de função (colocar dados na pilha e recuperar o resultado), o que pode resultar em um executável maior, pois o código da função precisa ser repetido várias vezes. O resultado é semelhante a [macros tipo função](<#/doc/preprocessor/replace>), exceto que identificadores e macros usados na função se referem às definições visíveis no ponto de definição, não no ponto de chamada.

Independentemente de o inlining ocorrer, as seguintes semânticas de funções inline são garantidas:

*   Qualquer função com ligação interna pode ser declarada `static inline` sem outras restrições.

*   Uma função inline não-estática não pode definir uma variável estática local de função não-const e não pode se referir a uma variável estática de escopo de arquivo.
```c
    static int x;
     
    inline void f(void)
    {
        static int n = 1; // erro: estática não-const em uma função inline não-estática
        int k = x; // erro: função inline não-estática acessa uma variável estática
    }
```

Se uma função não-estática é declarada `inline`, então ela deve ser definida na mesma unidade de tradução. A definição inline que não usa `extern` não é externamente visível e não impede que outras unidades de tradução definam a mesma função. Isso torna a palavra-chave `inline` uma alternativa a `static` para definir funções dentro de arquivos de cabeçalho (headers), que podem ser incluídos em múltiplas unidades de tradução do mesmo programa.

Se uma função é declarada `inline` em algumas unidades de tradução, ela não precisa ser declarada `inline` em todos os lugares: no máximo uma unidade de tradução pode também fornecer uma função regular, não-inline e não-estática, ou uma função declarada `extern inline`. Esta única unidade de tradução é dita fornecer a _definição externa_. Para evitar [comportamento indefinido](comportamento indefinido), uma definição externa deve existir no programa se o nome da função com ligação externa for usado em uma expressão, veja [regra de uma definição](<#/doc/language/extern>).

O endereço de uma função inline com ligação externa é sempre o endereço da definição externa, mas quando este endereço é usado para fazer uma chamada de função, é não especificado se a _definição inline_ (se presente na unidade de tradução) ou a _definição externa_ é chamada. Os objetos estáticos definidos dentro de uma definição inline são distintos dos objetos estáticos definidos dentro da definição externa:
```c
    inline const char *saddr(void) // a definição inline para uso neste arquivo
    {
        static const char name[] = "saddr";
        return name;
    }
     
    int compare_name(void)
    {
        return saddr() == saddr(); // comportamento não especificado, uma chamada pode ser externa
    }
     
    extern const char *saddr(void); // uma definição externa também é gerada
```

Um programa C não deve depender se a versão inline ou a versão externa de uma função é chamada, caso contrário o comportamento é não especificado.

### Palavras-chave

[`inline`](<#/doc/keyword/inline>)

### Notas

A palavra-chave `inline` foi adotada do C++, mas em C++, se uma função é declarada `inline`, ela deve ser declarada `inline` em cada unidade de tradução, e também cada definição de uma função inline deve ser exatamente a mesma (em C, as definições podem ser diferentes, e depender das diferenças apenas resulta em comportamento não especificado). Por outro lado, C++ permite estáticas locais de função não-const e todas as estáticas locais de função de diferentes definições de uma função inline são as mesmas em C++ mas distintas em C.

### Exemplo

Arquivo de cabeçalho "test.h"
```c
    #ifndef TEST_H_INCLUDED
    #define TEST_H_INCLUDED
     
    inline int sum(int a, int b)
    {
        return a + b;
    }
     
    #endif
```

Arquivo fonte "sum.c"
```c
    #include "test.h"
     
    extern inline int sum(int a, int b); // fornece definição externa
```

Arquivo fonte "test1.c"
```c
    #include <stdio.h>
    #include "test.h"
     
    extern int f(void);
     
    int main(void)
    {
        printf("%d\n", sum(1, 2) + f());
    }
```

Arquivo fonte "test2.c"
```c
    #include "test.h"
     
    int f(void)
    {
        return sum(3, 4);
    }
```

Saída
```
    10
```

|---|---|

### Referências

*   Padrão C23 (ISO/IEC 9899:2024):

    *   6.7.4 Especificadores de função (p: TBD)

*   Padrão C17 (ISO/IEC 9899:2018):

    *   6.7.4 Especificadores de função (p: TBD)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   6.7.4 Especificadores de função (p: 125-127)

*   Padrão C99 (ISO/IEC 9899:1999):

    *   6.7.4 Especificadores de função (p: 112-113)

### Veja também

[Documentação C++](<#/>) para o especificador `inline`
---