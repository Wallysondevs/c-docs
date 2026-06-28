# instrução if

Executa código condicionalmente.

Usado onde o código precisa ser executado apenas se alguma condição for verdadeira.

### Sintaxe

---
attr-spec-seq(optional) `if (` expression `)` statement-true | (1) |
attr-spec-seq(optional) `if (` expression `)` statement-true `else` statement-false | (2) |
- **attr-spec-seq** — (C23)lista opcional de [atributos](<#/doc/language/attributes>), aplicada à instrução `if`
- **expression** — uma [expressão](<#/doc/language/expressions>) de qualquer tipo escalar
- **statement-true** — qualquer [instrução](<#/doc/language/statements>) (frequentemente uma instrução composta), que é executada se expression for diferente de ​0​
- **statement-false** — qualquer [instrução](<#/doc/language/statements>) (frequentemente uma instrução composta), que é executada se expression for igual a ​0​

### Explicação

expression deve ser uma expressão de qualquer [tipo escalar](<#/doc/language/compatible_type>).

Se expression for diferente do inteiro zero, statement-true é executada.

Na forma (2), se expression for igual ao inteiro zero, statement_false é executada.

Assim como todas as outras instruções de seleção e iteração, a instrução if completa possui seu próprio escopo de bloco:
```c
    enum {a, b};
    int different(void)
    {
        if (sizeof(enum {b, a}) != sizeof(int))
            return a; // a == 1
        return b; // b == 0 in C89, b == 1 in C99
    }
```

| (desde C99)

### Notas

O `else` é sempre associado ao `if` precedente mais próximo (em outras palavras, se statement-true também for uma instrução `if`, então essa instrução `if` interna também deve conter uma parte `else`):
```c
    int j = 1;
    if (i > 1)
       if(j > 2)
           printf("%d > 1 and %d > 2\n", i, j);
        else // este else faz parte de if(j>2), não faz parte de if(i>1)
           printf("%d > 1 and %d <= 2\n", i, j);
```

Se statement-true for acessada através de um [goto](<#/doc/language/goto>), statement-false não é executada.

### Palavras-chave

[`if`](<#/doc/keyword/if>), [`else`](<#/doc/keyword/else>)

### Exemplo

Execute este código
```c
    #include <stdio.h>
     
    int main(void)
    {
        int i = 2;
        if (i > 2) {
            printf("first is true\n");
        } else {
            printf("first is false\n");
        }
     
        i = 3;
        if (i == 3) printf("i == 3\n");
     
        if (i != 3) printf("i != 3 is true\n");
        else        printf("i != 3 is false\n");
    }
```

Saída:
```
    first is false
    i == 3
    i != 3 is false
```

### Referências

  * C17 standard (ISO/IEC 9899:2018):

    

  * 6.8.4.1 The if statement (p: 108-109)

  * C11 standard (ISO/IEC 9899:2011):

    

  * 6.8.4.1 The if statement (p: 148-149)

  * C99 standard (ISO/IEC 9899:1999):

    

  * 6.8.4.1 The if statement (p: 133-134)

  * C89/C90 standard (ISO/IEC 9899:1990):

    

  * 3.6.4.1 The if statement

### Veja também

[documentação C++](<#/>) para a instrução `if`
---