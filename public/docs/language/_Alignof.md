# _Alignof (desde C11)(obsoleto em C23), alignof (desde C23) operador

Consulta o requisito de alinhamento do tipo de seu operando.

### Sintaxe

---
`_Alignof(` type-name `)` | | (desde C11)(obsoleto em C23)
`alignof(` type-name `)` | | (desde C23)
Este operador é tipicamente usado através da macro de conveniência [`alignof`](<#/doc/types>), que é fornecida no cabeçalho [`<stdalign.h>`](<#/doc/types>) | (até C23)

### Explicação

Retorna o [requisito de alinhamento](<#/doc/language/object>) do tipo [nomeado](<#/doc/language/compatible_type>) por type-name. Se type-name for um tipo array, o resultado é o requisito de alinhamento do tipo do elemento do array. O type-name não pode ser um tipo de função ou um tipo incompleto.

O resultado é uma constante inteira do tipo [size_t](<#/doc/types/size_t>).

O operando não é avaliado (portanto, identificadores externos usados no operando não precisam ser definidos).

Se type-name for um tipo [VLA](<#/doc/language/array>), sua expressão de tamanho não é avaliada.

### Notas

O uso de `_Alignof`(até C23)`alignof`(desde C23) com expressões é permitido por alguns compiladores C como uma extensão não padrão.

### Palavras-chave

[`alignof`](<#/doc/keyword/alignof>), [`_Alignof`](<#/doc/keyword/_Alignof>)

### Exemplo

Execute este código
```c
    #include <stdalign.h>
    #include <stddef.h>
    #include <stdio.h>
     
    int main(void)
    {
        printf("Alignment of char = %zu\n", alignof(char));
        printf("Alignment of max_align_t = %zu\n", alignof(max_align_t));
        printf("alignof(float[10]) = %zu\n", alignof(float[10]));
        printf("alignof(struct{char c; int n;}) = %zu\n",
                alignof(struct {char c; int n;}));
    }
```

Saída possível:
```
    Alignment of char = 1
    Alignment of max_align_t = 16
    alignof(float[10]) = 4
    alignof(struct{char c; int n;}) = 4
```

### Relatórios de defeito

Os seguintes relatórios de defeito que alteram o comportamento foram aplicados retroativamente a padrões C publicados anteriormente.

DR | Aplicado a | Comportamento conforme publicado | Comportamento correto
[DR 494](<https://www.open-std.org/jtc1/sc22/wg14/www/docs/n2396.htm#dr_494>) | C11 | se a expressão de tamanho em um VLA é avaliada em `_Alignof` era não especificado | ela não é avaliada

### Referências

  * C23 standard (ISO/IEC 9899:2024): 

    

  * 6.5.3.4 The sizeof and alignof operators (p: TBD) 

  * C17 standard (ISO/IEC 9899:2018): 

    

  * 6.5.3.4 The sizeof and _Alignof operators (p: 64-65) 

  * C11 standard (ISO/IEC 9899:2011): 

    

  * 6.5.3.4 The sizeof and _Alignof operators (p: 90-91) 

### Veja também

[ max_align_t](<#/doc/types/max_align_t>)(C11) | um tipo com requisito de alinhamento tão grande quanto qualquer outro tipo escalar
(typedef)
[`_Alignas`](<#/doc/language/alignas>)(até C23)[`alignas`](<#/doc/language/alignas>)(desde C23) | define os requisitos de alinhamento de um objeto
(especificador)
[Documentação C++](<#/>) para o operador `alignof`