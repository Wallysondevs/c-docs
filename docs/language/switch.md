# instrução switch

Executa código de acordo com o valor de um argumento integral.

Usado quando um ou vários de muitos ramos de código precisam ser executados de acordo com um valor integral.

### Sintaxe

---
attr-spec-seq(opcional) `switch (` expression `)` statement
- **attr-spec-seq** — (C23)lista opcional de [atributos](<#/doc/language/attributes>), aplicada à instrução `switch`
- **expression** — qualquer [expressão](<#/doc/language/expressions>) de [tipo inteiro](<#/doc/language/compatible_type>) (char, inteiro com ou sem sinal, ou enumeração)
- **statement** — qualquer [instrução](<#/doc/language/statements>) (tipicamente uma instrução composta). Rótulos `case:` e `default:` são permitidos na statement, e a instrução `break;` tem um significado especial.
---
`case` constant-expression `:` statement | (1) | (ate C23)
attr-spec-seq(opcional) `case` constant-expression `:` statement(opcional) | (1) | (desde C23)
`default` `:` statement | (2) | (ate C23)
attr-spec-seq(opcional) `default` `:` statement(opcional) | (2) | (desde C23)
- **constant-expression** — qualquer [expressão constante](<#/doc/language/constant_expression>) inteira
- **attr-spec-seq** — (C23)lista opcional de [atributos](<#/doc/language/attributes>), aplicada ao rótulo

### Explicação

O corpo de uma instrução `switch` pode ter um número arbitrário de rótulos `case:`, desde que os valores de todas as constant-expressions sejam únicos (após [conversão](<#/doc/language/conversion>) para o [tipo promovido](<#/doc/language/conversion>) da expression). No máximo um rótulo `default:` pode estar presente (embora instruções `switch` aninhadas possam usar seus próprios rótulos `default:` ou ter rótulos `case:` cujas constantes são idênticas às usadas na instrução `switch` envolvente).

Se expression for avaliada para um valor que é igual ao valor de uma das constant-expressions após a conversão para o tipo promovido da expression, então o controle é transferido para a instrução que é rotulada com aquela constant-expression.

Se expression for avaliada para um valor que não corresponde a nenhum dos rótulos `case:`, e o rótulo `default:` estiver presente, o controle é transferido para a instrução rotulada com o rótulo `default:`.

Se expression for avaliada para um valor que não corresponde a nenhum dos rótulos `case:`, e o rótulo `default:` não estiver presente, nenhuma parte do corpo do `switch` é executada.

A instrução [break](<#/doc/language/break>), quando encontrada em qualquer lugar na statement, sai da instrução `switch`:
```c
    switch(1) {
        case 1 : puts("1"); // imprime "1",
        case 2 : puts("2"); // então imprime "2" ("fall-through")
    }
```
```c
    switch(1) {
        case 1 : puts("1"); // imprime "1"
                 break;     // e sai do switch
        case 2 : puts("2");
                 break;
    }
```

Assim como todas as outras instruções de seleção e iteração, a instrução `switch` estabelece [escopo de bloco](<#/doc/language/scope>): qualquer identificador introduzido na expression sai do escopo após a statement. Se um VLA ou outro identificador com tipo variably-modified tiver um rótulo `case:` ou `default:` dentro de seu escopo, a instrução `switch` inteira deve estar em seu escopo (em outras palavras, um VLA deve ser declarado antes de todo o `switch` ou após o último rótulo):
```c
    switch (expr)
    {
            int i = 4; // não é um VLA; OK para declarar aqui
            f(i); // nunca chamado
    //      int a[i]; // erro: VLA não pode ser declarado aqui
        case 0:
            i = 17;
        default:
            int a[i]; // OK para declarar VLA aqui
            printf("%d\n", i); // imprime 17 se expr == 0, imprime valor indeterminado caso contrário
    }
```

| (desde C99)

### Palavras-chave

[`switch`](<#/doc/keyword/switch>), [`case`](<#/doc/keyword/case>), [`default`](<#/doc/keyword/default>)

### Exemplo

Execute este código
```c
    #include <stdio.h>
     
    void func(int x)
    {
       printf("func(%d): ", x);
       switch(x)
       {
          case 1: printf("case 1, ");
          case 2: printf("case 2, ");
          case 3: printf("case 3.\n"); break;
          case 4: printf("case 4, ");
          case 5:
          case 6: printf("case 5 or case 6, ");
          default: printf("default.\n");
       }
    }
     
    int main(void)
    {
       for(int i = 1; i < 9; ++i) func(i);
    }
```

Saída:
```
    func(1): case 1, case 2, case 3.
    func(2): case 2, case 3.
    func(3): case 3.
    func(4): case 4, case 5 or case 6, default.
    func(5): case 5 or case 6, default.
    func(6): case 5 or case 6, default.
    func(7): default.
    func(8): default.
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 6.8.4.2 A instrução switch (p: 108-109)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 6.8.4.2 A instrução switch (p: 149-150)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 6.8.4.2 A instrução switch (p: 134-135)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 3.6.4.2 A instrução switch

### Veja também

[documentação C++](<#/>) para a instrução `switch`
---