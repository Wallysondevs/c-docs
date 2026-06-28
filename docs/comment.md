# Comentários

Comentários servem como uma espécie de documentação dentro do código. Quando inseridos em um programa, eles são efetivamente ignorados pelo compilador; são destinados unicamente a serem usados como notas pelos humanos que leem o código-fonte.

### Sintaxe

---
`/*` comment `*/` | (1) |
`//` comment | (2) | (desde C99)
---

1) Frequentemente conhecidos como comentários "estilo C" ou "de múltiplas linhas".

2) Frequentemente conhecidos como comentários "estilo C++" ou "de linha única".

Todos os comentários são removidos do programa na [fase de tradução 3](<#/doc/language/translation_phases>) substituindo cada comentário por um único caractere de espaço em branco.

### Estilo C

Comentários estilo C são geralmente usados para comentar grandes blocos de texto ou pequenos fragmentos de código; no entanto, eles podem ser usados para comentar linhas únicas. Para inserir texto como um comentário estilo C, basta cercar o texto com `/*` e `*/`. Comentários estilo C dizem ao compilador para ignorar todo o conteúdo entre `/*` e `*/`. Embora não faça parte do padrão C, `/` e `/` são frequentemente usados para indicar blocos de documentação; isso é legal porque o segundo asterisco é simplesmente tratado como parte do comentário.

Exceto dentro de uma [constante de caractere](<#/doc/language/character_constant>), um [literal de string](<#/doc/language/string_literal>), ou um comentário, os caracteres `/*` introduzem um comentário. O conteúdo de tal comentário é examinado apenas para identificar caracteres multibyte e para encontrar os caracteres `*/` que encerram o comentário. Comentários estilo C não podem ser aninhados.

### Estilo C++

Comentários estilo C++ são geralmente usados para comentar linhas únicas de texto ou código; no entanto, eles podem ser colocados juntos para formar comentários de múltiplas linhas. Para inserir texto como um comentário estilo C++, basta preceder o texto com `//` e seguir o texto com o caractere de nova linha. Comentários estilo C++ dizem ao compilador para ignorar todo o conteúdo entre `//` e uma nova linha. Exceto dentro de uma [constante de caractere](<#/doc/language/character_constant>), um [literal de string](<#/doc/language/string_literal>), ou um comentário, os caracteres `//` introduzem um comentário que inclui todos os caracteres multibyte até, mas não incluindo, o próximo caractere de nova linha. O conteúdo de tal comentário é examinado apenas para identificar caracteres multibyte e para encontrar o caractere de nova linha que encerra o comentário. Comentários estilo C++ podem ser aninhados:
```
    //  y = f(x);   // invoke algorithm
```

Um comentário estilo C pode aparecer dentro de um comentário estilo C++:
```
    //  y = f(x);   /* invoke algorithm */
```

Um comentário estilo C++ pode aparecer dentro de um comentário estilo C; este é um mecanismo para excluir um pequeno bloco de código-fonte:
```
    /*
        y = f(x);   // invoke algorithms
        z = g(x);
    */
```

| (desde C99)

### Notas

Como os comentários [são removidos](<#/doc/language/translation_phases>) antes da fase do pré-processador, uma macro não pode ser usada para formar um comentário e um comentário estilo C não terminado não se estende de um arquivo #include'd.
```
    /* An attempt to use a macro to form a comment. */
    /* But, a space replaces characters "//".       */
    #ifndef DEBUG
        #define PRINTF //
    #else
        #define PRINTF printf
    #endif
    ...
    PRINTF("Error in file %s at line %i\n", __FILE__, __LINE__);
```

Além de comentar, outros mecanismos usados para exclusão de código-fonte são:
```
    #if 0
        puts("this will not be compiled");
        /* no conflict with C-style comments */
        // no conflict with C++-style comments
    #endif
```

e
```
    if(0) {
        puts("this will be compiled but not be executed");
        /* no conflict with C-style comments */
        // no conflict with C++-style comments
    }
```

A introdução de comentários `//` em C99 foi uma mudança disruptiva em algumas raras circunstâncias:
```
    a = b //*divisor:*/ c
    + d; /* C89 compiles a = b / c + d;
            C99 compiles a = b + d; */
```

### Exemplo

Execute este código
```
    #include <stdio.h>
    /*
    Comentários estilo C podem conter
    múltiplas linhas.
    */
     
    /* Ou, apenas uma linha. */
     
    // Comentários estilo C++ podem comentar uma linha.
     
    // Ou, eles podem
    // ser encadeados.
     
    int main(void)
    {
      // O código abaixo não será executado
      // puts("Hello");
     
      // O código abaixo será executado
      puts("World");
     
      // Uma nota sobre barra invertida + nova linha.
      // Apesar de pertencer à fase de tradução 2 (vs fase 3 para comentários),
      // '\' ainda determina qual porção do código-fonte é considerada
      // como 'comentários':
      // Este comentário será promovido para a próxima linha \
      puts("Won't be run"); // pode emitir um aviso "multi-line comment"
      puts("Hello, again");
    }
```

Saída:
```
    World
    Hello, again
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 6.4.9 Comentários (p: 54)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 6.4.9 Comentários (p: 75)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 6.4.9 Comentários (p: 66)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 3.1.9 Comentários

### Veja também

[Documentação C++](<#/>) para Comentários
---