# _Alignas (desde C11)(obsoleto em C23), alignas (desde C23)

Aparece na sintaxe de [declaração](<#/doc/language/declarations>) como um dos especificadores de tipo para modificar o [requisito de alinhamento](<#/doc/language/object>) do objeto que está sendo declarado.

### Sintaxe

---
`_Alignas` `(` expression `)` | (1) | (desde C11)
`alignas` `(` expression `)` | (2) | (desde C23)
`_Alignas` `(` type `)` | (3) | (desde C11)
`alignas` `(` type `)` | (4) | (desde C23)
- **expression** — qualquer [expressão constante inteira](<#/doc/language/constant_expression>) cujo valor seja um [alinhamento](<#/doc/language/object>) válido ou zero
- **type** — qualquer [nome de tipo](<#/doc/language/compatible_type>)
A palavra-chave `_Alignas` também está disponível como a macro de conveniência [`alignas`](<#/doc/types>), disponível no cabeçalho [`<stdalign.h>`](<#/doc/types>). | (até C23)

### Explicação

O especificador `_Alignas`(até C23)`alignas`(desde C23) só pode ser usado ao declarar objetos que não são [campos de bits](<#/doc/language/bit_field>) e não possuem a classe de armazenamento [register](<#/doc/language/storage_duration>). Ele não pode ser usado em declarações de parâmetros de função e não pode ser usado em um typedef.

Quando usado em uma declaração, o objeto declarado terá seu [requisito de alinhamento](<#/doc/language/object>) definido para

1,2) o resultado da expressão, a menos que seja zero

3,4) o requisito de alinhamento do tipo, ou seja, para _Alignof(type)(até C23)alignof(type)(desde C23)

exceto quando isso enfraqueceria o alinhamento que o tipo teria naturalmente.

Se a expressão for avaliada como zero, este especificador não terá efeito.

Quando múltiplos especificadores `_Alignas`(até C23)`alignas`(desde C23) aparecem na mesma declaração, o mais rigoroso é usado.

O especificador `_Alignas`(até C23)`alignas`(desde C23) só precisa aparecer na [definição](<#/doc/language/declarations>) de um objeto, mas se qualquer declaração usar `_Alignas`(até C23)`alignas`(desde C23), ela deve especificar o mesmo alinhamento que o `_Alignas`(até C23)`alignas`(desde C23) na definição. O comportamento é indefinido se diferentes unidades de tradução especificarem alinhamentos diferentes para o mesmo objeto.

### Notas

Em C++, o especificador `alignas` também pode ser aplicado às declarações de tipos de classe/struct/union e enumerações. Isso não é suportado em C, mas o alinhamento de um tipo struct pode ser controlado usando `_Alignas`(até C23)`alignas`(desde C23) em uma declaração de membro.

### Palavras-chave

[`alignas`](<#/doc/keyword/alignas>), [`_Alignas`](<#/doc/keyword/_Alignas>)

### Exemplo

Execute este código
```c
    #include <stdalign.h>
    #include <stdio.h>
    
    // cada objeto do tipo struct sse_t será alinhado a um limite de 16 bytes
    // (nota: requer suporte para DR 444)
    struct sse_t
    {
        alignas(16) float sse_data[4];
    };
    
    // cada objeto do tipo struct data será alinhado a um limite de 128 bytes
    struct data
    {
        char x;
        alignas(128) char cacheline[128]; // array de char super-alinhado,
                                          // não um array de chars super-alinhados
    };
    
    int main(void)
    {
        printf("sizeof(data) = %zu (1 byte + 127 bytes padding + 128-byte array)\n",
               sizeof(struct data));
    
        printf("alignment of sse_t is %zu\n", alignof(struct sse_t));
    
        alignas(2048) struct data d; // esta instância de data é alinhada de forma ainda mais rigorosa
        (void)d; // suprime o aviso "talvez não usado"
    }
```

Saída:
```
    sizeof(data) = 256 (1 byte + 127 bytes padding + 128-byte array)
    alignment of sse_t is 16
```

### Relatórios de defeito

Os seguintes relatórios de defeito que alteram o comportamento foram aplicados retroativamente a padrões C publicados anteriormente.

DR | Aplicado a | Comportamento conforme publicado | Comportamento correto
[DR 444](<https://www.open-std.org/jtc1/sc22/wg14/www/docs/n2396.htm#dr_444>) | C11 | `_Alignas` não era permitido em membros de struct e union | permitido

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 6.7.5 Especificador de alinhamento (p: TBD)

    

  * 6.2.8 Alinhamento de objetos (p: TBD)

    

  * 7.15 Alinhamento <stdalign.h> (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 6.7.5 Especificador de alinhamento (p: 92)

    

  * 6.2.8 Alinhamento de objetos (p: 36-37)

    

  * 7.15 Alinhamento <stdalign.h> (p: 196)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 6.7.5 Especificador de alinhamento (p: 127-128)

    

  * 6.2.8 Alinhamento de objetos (p: 48-49)

    

  * 7.15 Alinhamento <stdalign.h> (p: 268)

### Veja também

[`max_align_t`](<#/doc/types/max_align_t>)(C11) | um tipo com requisito de alinhamento tão grande quanto qualquer outro tipo escalar
(typedef)
[`_Alignof`](<#/doc/language/alignof>)(até C23)[`alignof`](<#/doc/language/alignof>)(desde C23) | consulta os requisitos de alinhamento de um objeto
(operador)
[Documentação C++](<#/>) para o especificador `alignas`