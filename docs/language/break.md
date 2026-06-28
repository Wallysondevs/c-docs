# Instrução break

Faz com que o laço [for](<#/doc/language/for>), [while](<#/doc/language/while>) ou [do-while](<#/doc/language/do>) ou a [instrução switch](<#/doc/language/switch>) que o envolve seja encerrado.

Usado quando seria de outra forma complicado encerrar o laço usando a expressão de condição e instruções condicionais.

### Sintaxe

---
attr-spec-seq (opcional) `break` `;`
- **attr-spec-seq** — (C23) lista opcional de [atributos](<#/doc/language/attributes>), aplicados à instrução `break`

Aparece apenas dentro da instrução de um corpo de laço ([`while`](<#/doc/language/while>), [`do-while`](<#/doc/language/do>), [`for`](<#/doc/language/for>)) ou dentro da instrução de um [`switch`](<#/doc/language/switch>).

### Explicação

Após esta instrução, o controle é transferido para a instrução ou declaração imediatamente seguinte ao laço ou switch que a envolve, como se fosse por [`goto`](<#/doc/language/goto>).

### Palavras-chave

[`break`](<#/doc/keyword/break>)

### Observações

Uma instrução break não pode ser usada para sair de múltiplos laços aninhados. A [instrução goto](<#/doc/language/goto>) pode ser usada para este propósito.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    
    int main(void)
    {
        int i = 2;
        switch (i)
        {
            case 1: printf("1");
            case 2: printf("2");   // i==2, então a execução começa neste rótulo de caso
            case 3: printf("3");
            case 4:
            case 5: printf("45");
                    break;         // a execução dos casos subsequentes é encerrada
            case 6: printf("6");
        }
        printf("\n");
    
        // Compare as saídas destes dois laços for aninhados.
        for (int j = 0; j < 2; j++)
            for (int k = 0; k < 5; k++)
                printf("%d%d ", j,k);
        printf("\n");
    
        for (int j = 0; j < 2; j++)
        {
            for (int k = 0; k < 5; k++) // apenas este laço é encerrado por break
            {
                if (k == 2)
                    break;
                printf("%d%d ", j,k);
            }
        }
    }
```

Saída possível:
```
    2345
    00 01 02 03 04 10 11 12 13 14
    00 01 10 11
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 6.8.6.3 A instrução break (p: 111)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 6.8.6.3 A instrução break (p: 153)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 6.8.6.3 A instrução break (p: 138)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 3.6.6.3 A instrução break

### Veja também

`[[[fallthrough](<#/doc/language/attributes/fallthrough>)]]`(C23) | indica que a passagem (fall-through) do rótulo de caso anterior é intencional e não deve ser diagnosticada por um compilador que avisa sobre fall-through
(especificador de atributo)
[Documentação C++](<#/>) para a instrução `break`