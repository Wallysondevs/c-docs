# laço for

Executa um laço.

Usado como um equivalente mais curto do [laço while](<#/doc/language/while>).

### Sintaxe

---
attr-spec-seq(desde C23)(opcional) `for` `(` init-clause `;` cond-expression `;` iteration-expression `)` loop-statement

### Explicação

Comporta-se da seguinte forma:

*   init-clause pode ser uma expressão ou uma declaração (desde C99).

*   Um init-clause, que é uma expressão, é avaliado uma vez, antes da primeira avaliação de cond-expression e seu resultado é descartado.

*   Um init-clause, que é uma declaração, está no escopo em todo o corpo do laço, incluindo o restante de init-clause, todo o cond-expression, todo o iteration-expression e todo o loop-statement. Apenas os [especificadores de classe de armazenamento](<#/doc/language/storage_duration>) `auto` e `register` são permitidos para as variáveis declaradas nesta declaração.

| (desde C99)

*   cond-expression é avaliado antes do corpo do laço. Se o resultado da expressão for zero, a instrução do laço é encerrada imediatamente.
*   iteration-expression é avaliado após o corpo do laço e seu resultado é descartado. Após avaliar iteration-expression, o controle é transferido para cond-expression.

init-clause, cond-expression e iteration-expression são todos opcionais. Se cond-expression for omitido, ele é substituído por uma constante inteira não-zero, o que torna o laço infinito:
```c
    for(;;) {
       printf("endless loop!");
    }
```

loop-statement não é opcional, mas pode ser uma instrução nula:
```c
    for(int n = 0; n < 10; ++n, printf("%d\n", n))
        ; // instrução nula
```

Se a execução do laço precisar ser terminada em algum ponto, uma [instrução break](<#/doc/language/break>) pode ser usada em qualquer lugar dentro do loop-statement.

A [instrução continue](<#/doc/language/continue>) usada em qualquer lugar dentro do loop-statement transfere o controle para iteration-expression.

Um programa com um laço infinito tem comportamento indefinido se o laço não tiver comportamento observável (E/S, acessos voláteis, operação atômica ou de sincronização) em qualquer parte de seu cond-expression, iteration-expression ou loop-statement. Isso permite que os compiladores otimizem todos os laços não observáveis sem provar que eles terminam. As únicas exceções são os laços onde cond-expression é omitido ou é uma expressão constante; `for(;;)` é sempre um laço infinito.

Assim como todas as outras instruções de seleção e iteração, a instrução `for` estabelece [escopo de bloco](<#/doc/language/scope>): qualquer identificador introduzido no init-clause, cond-expression ou iteration-expression sai do escopo após o loop-statement. | (desde C99)
attr-spec-seq é uma lista opcional de [atributos](<#/doc/language/attributes>), aplicada à instrução `for`. | (desde C23)

### Palavras-chave

[`for`](<#/doc/keyword/for>)

### Notas

A instrução de expressão usada como loop-statement estabelece seu próprio escopo de bloco, distinto do escopo de init-clause, diferente do C++:
```c
    for (int i = 0; ; ) {
        long i = 1;   // C válido, C++ inválido
        // ...
    }
```

É possível entrar no corpo de um laço usando [goto](<#/doc/language/goto>). Ao entrar em um laço dessa maneira, init-clause e cond-expression não são executados. (Se o controle então atingir o final do corpo do laço, a repetição pode ocorrer, incluindo a execução de cond-expression.)

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
    enum { SIZE = 8 };
    int main(void)
    {
        int array[SIZE];
        for(size_t i = 0 ; i < SIZE; ++i)
            array [i] = rand() % 2;
        printf("Array filled!\n");
        for (size_t i = 0; i < SIZE; ++i)
            printf("%d ", array[i]);
        putchar('\n');
    }
```

Saída possível:
```
    Array filled!
    1 0 1 1 1 1 0 0
```

### Referências

*   Padrão C17 (ISO/IEC 9899:2018):

    *   6.8.5.3 A instrução for (p: 110)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   6.8.5.3 A instrução for (p: 151)

*   Padrão C99 (ISO/IEC 9899:1999):

    *   6.8.5.3 A instrução for (p: 136)

*   Padrão C89/C90 (ISO/IEC 9899:1990):

    *   3.6.5.3 A instrução for

### Veja também

[Documentação C++](<#/>) para o laço `for`
---