# laço do-while

Executa uma instrução repetidamente até que o valor da expressão de condição se torne falso. O teste ocorre após cada iteração.

### Sintaxe

---
attr-spec-seq(optional) `do` statement `while (` expression `)` `;`
- **expression** — qualquer [expressão](<#/doc/language/expressions>) de [tipo escalar](<#/doc/language/compatible_type>). Esta expressão é avaliada após cada iteração, e se ela for igual a zero, o laço é encerrado.
- **statement** — qualquer [instrução](<#/doc/language/statements>), tipicamente uma instrução composta, que é o corpo do laço
- **attr-spec-seq** — (C23)lista opcional de [atributos](<#/doc/language/attributes>), aplicados à instrução do laço

### Explicação

Uma instrução `do-while` faz com que a instrução (também chamada de _corpo do laço_) seja executada repetidamente até que a expressão (também chamada de _expressão de controle_) seja igual a 0. A repetição ocorre independentemente de o corpo do laço ser inserido normalmente ou por um [goto](<#/doc/language/goto>) no meio da instrução.

A avaliação da expressão ocorre após cada execução da instrução (seja inserida normalmente ou por um goto). Se a expressão de controle precisar ser avaliada antes do corpo do laço, o [laço while](<#/doc/language/while>) ou o [laço for](<#/doc/language/for>) podem ser usados.

Se a execução do laço precisar ser terminada em algum ponto, a [instrução break](<#/doc/language/break>) pode ser usada como instrução de término.

Se a execução do laço precisar ser continuada no final do corpo do laço, a [instrução continue](<#/doc/language/continue>) pode ser usada como atalho.

Um programa com um laço infinito tem comportamento indefinido se o laço não tiver comportamento observável (E/S, acessos voláteis, operação atômica ou de sincronização) em qualquer parte de sua instrução ou expressão. Isso permite que os compiladores otimizem todos os laços não observáveis sem provar que eles terminam. As únicas exceções são os laços onde a expressão é uma expressão constante; `do {...} while(true);` é sempre um laço infinito.

Assim como todas as outras instruções de seleção e iteração, a instrução do-while estabelece [escopo de bloco](<#/doc/language/scope>): qualquer identificador introduzido na expressão sai do escopo após a instrução. | (desde C99)

### Notas

Expressões booleanas e de ponteiro são frequentemente usadas como expressões de controle de laço. O valor booleano `false` e o valor de ponteiro nulo de qualquer tipo de ponteiro são iguais a zero.

### Palavras-chave

[`do`](<#/doc/keyword/do>), [`while`](<#/doc/keyword/while>)

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
    enum { SIZE = 8 };
    int main(void)
    {
        // trivial example
        int array[SIZE], n = 0;
        do array[n++] = rand() % 2; // the loop body is a single expression statement
        while(n < SIZE);
        puts("Array filled!");
        n = 0;
        do { // the loop body is a compound statement
            printf("%d ", array[n]);
            ++n;
        } while (n < SIZE);
        printf("\n");
    
        // the loop from K&R itoa(). The do-while loop is used
        // because there is always at least one digit to generate
        int num = 1234, i=0;
        char s[10];
        do s[i++] = num % 10 + '0'; // get next digit in reverse order
        while ((num /= 10) > 0);
        s[i] = '\0';
        puts(s);
    }
```

Saída possível:
```
    Array filled!
    1 0 1 1 1 1 0 0
    4321
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 6.8.5.2 A instrução do (p: 109)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 6.8.5.2 A instrução do (p: 151)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 6.8.5.2 A instrução do (p: 136)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 3.6.5.2 A instrução do

### Veja também

[Documentação C++](<#/>) para o laço `do`-`while`
---