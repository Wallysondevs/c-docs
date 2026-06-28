# laço while

Executa uma instrução repetidamente, até que o valor da expressão se torne igual a zero. O teste ocorre antes de cada iteração.

### Sintaxe

---
attr-spec-seq(optional) `while (` expression `)` statement
- **expression** — qualquer [expressão](<#/doc/language/expressions>) de [tipo escalar](<#/doc/language/compatible_type>). Esta expressão é avaliada antes de cada iteração e, se for igual a zero, o laço é encerrado.
- **statement** — qualquer [instrução](<#/doc/language/statements>), tipicamente uma instrução composta, que serve como o corpo do laço
- **attr-spec-seq** — (C23)lista opcional de [atributos](<#/doc/language/attributes>), aplicados à instrução do laço

### Explicação

Uma instrução `while` faz com que a instrução (também chamada de _corpo do laço_) seja executada repetidamente até que a expressão (também chamada de _expressão de controle_) seja igual a zero. A repetição ocorre independentemente de o corpo do laço ser iniciado normalmente ou por um [goto](<#/doc/language/goto>) no meio da instrução.

A avaliação da expressão ocorre antes de cada execução da instrução (a menos que seja iniciada por um goto). Se a expressão de controle precisar ser avaliada após o corpo do laço, o [laço do-while](<#/doc/language/do>) pode ser usado.

Se a execução do laço precisar ser terminada em algum ponto, a [instrução break](<#/doc/language/break>) pode ser usada como uma instrução de terminação.

Se a execução do laço precisar ser continuada no final do corpo do laço, a [instrução continue](<#/doc/language/continue>) pode ser usada como um atalho.

Um programa com um laço infinito tem comportamento indefinido se o laço não tiver comportamento observável (E/S, acessos voláteis, operação atômica ou de sincronização) em qualquer parte de sua instrução ou expressão. Isso permite que os compiladores otimizem todos os laços não observáveis sem provar que eles terminam. As únicas exceções são os laços onde a expressão é uma expressão constante; `while(true)` é sempre um laço infinito.

Assim como todas as outras instruções de seleção e iteração, a instrução while estabelece [escopo de bloco](<#/doc/language/scope>): qualquer identificador introduzido na expressão sai do escopo após a instrução. | (desde C99)

### Notas

Expressões booleanas e de ponteiro são frequentemente usadas como expressões de controle de laço. O valor booleano `false` e o valor de ponteiro nulo de qualquer tipo de ponteiro são iguais a zero.

### Palavras-chave

[`while`](<#/doc/keyword/while>)

### Exemplo

Execute este código
```
    #include <stdio.h>
    #include <stdlib.h>
    #include <string.h>
    enum { SIZE = 8 };
    int main(void)
    {
        // trivial example
        int array[SIZE], n = 0;
        while(n < SIZE) array[n++] = rand() % 2;
        puts("Array filled!");
        n = 0;
        while(n < SIZE) printf("%d ", array[n++]);
        printf("\n");
    
        // classic strcpy() implementation
        // (copies a null-terminated string from src to dst)
        char src[] = "Hello, world", dst[sizeof src], *p = dst, *q = src;
        while((*p++ = *q++)) // double parentheses (that are not strictly necessary)
                             // used to suppress warnings, ensuring that this is an
                             // assignment (as opposed to a comparison) by intention,
                             // whose result is used as a truth value
            ; // null statement
        puts(dst);
    }
```

Output:
```
    Array filled!
    1 0 1 1 1 1 0 0
    Hello, world
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 6.8.5.1 A instrução while (p: 109)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 6.8.5.1 A instrução while (p: 151)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 6.8.5.1 A instrução while (p: 136)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 3.6.5.1 A instrução while

### Veja também

[Documentação C++](<#/>) para o laço `while`
---