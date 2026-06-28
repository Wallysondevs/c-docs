# Comportamento indefinido

O padrão da linguagem C especifica precisamente o [comportamento observável](<#/doc/language/as_if>) dos programas da linguagem C, exceto para aqueles nas seguintes categorias:

*   _comportamento indefinido_ - não há restrições sobre o comportamento do programa. Exemplos de comportamento indefinido são acessos de memória fora dos limites de um array, overflow de inteiro com sinal, desreferência de ponteiro nulo, modificação do mesmo escalar [mais de uma vez](<#/doc/language/eval_order>) em uma expressão sem pontos de sequência, acesso a um objeto através de um ponteiro de um tipo diferente, etc. Compiladores não são obrigados a diagnosticar comportamento indefinido (embora muitas situações simples sejam diagnosticadas), e o programa compilado não é obrigado a fazer nada significativo.

*   _comportamento não especificado_ - dois ou mais comportamentos são permitidos e a implementação não é obrigada a documentar os efeitos de cada comportamento. Por exemplo, [ordem de avaliação](<#/doc/language/eval_order>), se [literais de string](<#/doc/language/string_literal>) idênticos são distintos, etc. Cada comportamento não especificado resulta em um de um conjunto de resultados válidos e pode produzir um resultado diferente quando repetido no mesmo programa.

*   _comportamento definido pela implementação_ - comportamento não especificado onde cada implementação documenta como a escolha é feita. Por exemplo, número de bits em um byte, ou se o deslocamento à direita de inteiro com sinal é aritmético ou lógico.

*   _comportamento específico da localidade_ - comportamento definido pela implementação que depende da [localidade atualmente escolhida](<#/doc/locale/setlocale>). Por exemplo, se [islower](<#/doc/string/byte/islower>) retorna true para qualquer caractere diferente das 26 letras latinas minúsculas.

(Nota: Programas [estritamente conformes](<#/doc/language/conformance>) não dependem de nenhum comportamento não especificado, indefinido ou definido pela implementação)

Os compiladores são obrigados a emitir mensagens de diagnóstico (erros ou avisos) para quaisquer programas que violem qualquer regra de sintaxe C ou restrição semântica, mesmo que seu comportamento seja especificado como indefinido ou definido pela implementação, ou se o compilador fornecer uma extensão de linguagem que permita aceitar tal programa. Diagnósticos para comportamento indefinido não são exigidos de outra forma.

### Comportamento Indefinido e otimização

Como programas C corretos são livres de comportamento indefinido, os compiladores podem produzir resultados inesperados quando um programa que realmente possui comportamento indefinido é compilado com otimização habilitada:

Por exemplo,

#### Overflow de inteiro com sinal
```c
    int foo(int x)
    {
        return x + 1 > x; // ou true ou comportamento indefinido devido a overflow de inteiro com sinal
    }
```

pode ser compilado como ([demo](<https://godbolt.org/z/9dh7b71TK>))
```asm
    foo:
            mov     eax, 1
            ret
```

#### Acesso fora dos limites
```c
    int table[4] = {0};
    int exists_in_table(int v)
    {
        // retorna 1 em uma das primeiras 4 iterações ou comportamento indefinido devido a acesso fora dos limites
        for (int i = 0; i <= 4; i++)
            if (table[i] == v)
                return 1;
        return 0;
    }
```

Pode ser compilado como ([demo](<https://godbolt.org/z/48bn19Tsb>))
```asm
    exists_in_table:
            mov     eax, 1
            ret
```

#### Escalar não inicializado
```c
    _Bool p; // variável local não inicializada
    if (p) // Acesso com comportamento indefinido a escalar não inicializado
        puts("p is true");
    if (!p) // Acesso com comportamento indefinido a escalar não inicializado
        puts("p is false");
```

Pode produzir a seguinte saída (observado com uma versão mais antiga do gcc):
```
    p is true
    p is false
```
```c
    size_t f(int x)
    {
        size_t a;
        if (x) // ou x diferente de zero ou comportamento indefinido
            a = 42;
        return a;
    }
```

Pode ser compilado como ([demo](<https://godbolt.org/z/9nz6EMPTG>))
```asm
    f:
            mov     eax, 42
            ret
```

#### Escalar inválido
```c
    int f(void)
    {
        _Bool b = 0;
        unsigned char* p = (unsigned char*)&b;
        *p = 10;
        // ler de b agora é comportamento indefinido
        return b == 0;
    }
```

Pode ser compilado como ([demo](<https://godbolt.org/z/rjx77bjoh>))
```asm
    f:
            mov     eax, 11
            ret
```

#### Desreferência de ponteiro nulo
```c
    int foo(int* p)
    {
        int x = *p;
        if (!p)
            return x; // Ou comportamento indefinido acima ou este ramo nunca é executado
        else
            return 0;
    }
    
    int bar()
    {
        int* p = NULL;
        return *p;    // Comportamento indefinido incondicional
    }
```

pode ser compilado como ([demo](<https://godbolt.org/z/8jnjMjcPz>))
```asm
    foo:
            xor     eax, eax
            ret
    bar:
            ret
```

#### Acesso a ponteiro passado para [realloc](<#/doc/memory/realloc>)

Escolha clang para observar a saída mostrada

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(void)
    {
        int *p = (int*)malloc(sizeof(int));
        int *q = (int*)realloc(p, sizeof(int));
        *p = 1; // Acesso com comportamento indefinido a um ponteiro que foi passado para realloc
        *q = 2;
        if (p == q) // Acesso com comportamento indefinido a um ponteiro que foi passado para realloc
            printf("%d%d\n", *p, *q);
    }
```

Saída possível:
```
    12
```

#### Loop infinito sem efeitos colaterais

Escolha clang para observar a saída mostrada

Execute este código
```c
    #include <stdio.h>
    
    int fermat()
    {
        const int MAX = 1000;
        // Loop infinito sem efeitos colaterais é comportamento indefinido
        for (int a = 1, b = 1, c = 1; 1;)
        {
            if (((a * a * a) == ((b * b * b) + (c * c * c))))
                return 1;
            ++a;
            if (a > MAX)
            {
                a = 1;
                ++b;
            }
            if (b > MAX)
            {
                b = 1;
                ++c;
            }
            if (c > MAX)
                c = 1;
        }
        return 0;
    }
    
    int main(void)
    {
        if (fermat())
            puts("Fermat's Last Theorem has been disproved.");
        else
            puts("Fermat's Last Theorem has not been disproved.");
    }
```

Saída possível:
```
    Fermat's Last Theorem has been disproved.
```

### Referências

*   Padrão C23 (ISO/IEC 9899:2024):

    *   3.4 Comportamento (p: TBD)

    *   4 Conformidade (p: TBD)

*   Padrão C17 (ISO/IEC 9899:2018):

    *   3.4 Comportamento (p: 3-4)

    *   4 Conformidade (p: 8)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   3.4 Comportamento (p: 3-4)

    *   4/2 Comportamento indefinido (p: 8)

*   Padrão C99 (ISO/IEC 9899:1999):

    *   3.4 Comportamento (p: 3-4)

    *   4/2 Comportamento indefinido (p: 7)

*   Padrão C89/C90 (ISO/IEC 9899:1990):

    *   1.6 DEFINIÇÕES DE TERMOS

### Veja também

[Documentação C++](<#/>) para comportamento indefinido
---

### Links externos

1.  | [O que todo programador C deveria saber sobre comportamento indefinido #1/3](<https://blog.llvm.org/2011/05/what-every-c-programmer-should-know.html>)
2.  | [O que todo programador C deveria saber sobre comportamento indefinido #2/3](<https://blog.llvm.org/2011/05/what-every-c-programmer-should-know_14.html>)
3.  | [O que todo programador C deveria saber sobre comportamento indefinido #3/3](<https://blog.llvm.org/2011/05/what-every-c-programmer-should-know_21.html>)
4.  | [Comportamento indefinido pode resultar em viagem no tempo (entre outras coisas, mas viagem no tempo é o mais estranho)](<https://devblogs.microsoft.com/oldnewthing/20140627-00/?p=633>)
5.  | [Entendendo o Overflow de Inteiro em C/C++](<https://www.cs.utah.edu/~regehr/papers/overflow12.pdf>)
6.  | [Comportamento Indefinido e o Último Teorema de Fermat](<https://web.archive.org/web/20201108094235/https://kukuruku.co/post/undefined-behavior-and-fermats-last-theorem/>)
7.  | [Diversão com ponteiros NULL, parte 1](<https://lwn.net/Articles/342330/>) (exploit local no Linux 2.6.30 causado por comportamento indefinido devido a desreferência de ponteiro nulo)