# instrução continue

Faz com que a porção restante do corpo do laço [for](<#/doc/language/for>), [while](<#/doc/language/while>) ou [do-while](<#/doc/language/do>) envolvente seja ignorada.

Usada quando seria de outra forma complicado ignorar a porção restante do laço usando instruções condicionais.

### Sintaxe

---
attr-spec-seq(opcional) `continue` `;`
- **attr-spec-seq** — (C23)lista opcional de [atributos](<#/doc/language/attributes>), aplicada à instrução `continue`

### Explicação

A instrução `continue` causa um salto, como se fosse por [goto](<#/doc/language/goto>), para o final do corpo do laço (ela só pode aparecer dentro do corpo dos laços [for](<#/doc/language/for>), [while](<#/doc/language/while>) e [do-while](<#/doc/language/do>)).

Para o laço [while](<#/doc/language/while>), ela age como
```c
    while (/* ... */) {
       // ... 
       continue; // acts as goto contin;
       // ... 
       contin:;
    }
```

Para o laço [do-while](<#/doc/language/do>), ela age como:
```c
    do {
        // ... 
        continue; // acts as goto contin;
        // ... 
        contin:;
    } while (/* ... */);
```

Para o laço [for](<#/doc/language/for>), ela age como:
```c
    for (/* ... */) {
        // ... 
        continue; // acts as goto contin;
        // ... 
        contin:;
    }
```

### Palavras-chave

[`continue`](<#/doc/keyword/continue>)

### Exemplo

Execute este código
```c
    #include <stdio.h>
    
    int main(void) 
    {
        for (int i = 0; i < 10; i++) {
            if (i != 5) continue;
            printf("%d ", i);             // esta instrução é ignorada toda vez que i != 5
        }
    
        printf("\n");
    
        for (int j = 0; j < 2; j++) {
            for (int k = 0; k < 5; k++) { // apenas este laço é afetado por continue
                if (k == 3) continue;
                printf("%d%d ", j, k);    // esta instrução é ignorada toda vez que k == 3
            }
        }
    }
```

Saída:
```
    5
    00 01 02 04 10 11 12 14
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 6.8.6.2 A instrução continue (p: 111)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 6.8.6.2 A instrução continue (p: 153)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 6.8.6.2 A instrução continue (p: 138)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 3.6.6.2 A instrução continue

### Veja também

[Documentação C++](<#/>) para a instrução `continue`
---