# Suporte a Tipos

Veja também [visão geral do sistema de tipos](<#/doc/language/types>) e [tipos aritméticos definidos pela linguagem](<#/doc/language/arithmetic_types>).

### Tipos básicos

#### Tipos básicos adicionais e macros de conveniência

Definido no cabeçalho `<stddef.h>`
---
[ size_t](<#/doc/types/size_t>) | tipo inteiro sem sinal retornado pelo operador [`sizeof`](<#/doc/language/sizeof>)
(typedef)
[ ptrdiff_t](<#/doc/types/ptrdiff_t>) | tipo inteiro com sinal retornado ao subtrair dois ponteiros
(typedef)
[ nullptr_t](<#/doc/types/nullptr_t>)(C23) | o tipo da constante de ponteiro nulo predefinida [`nullptr`](<#/doc/language/nullptr>)
(typedef)
[ NULL](<#/doc/types/NULL>) | constante de ponteiro nulo definida pela implementação
(macro constante)
[ max_align_t](<#/doc/types/max_align_t>)(C11) | um tipo com requisito de alinhamento tão grande quanto qualquer outro tipo escalar
(typedef)
[ offsetof](<#/doc/types/offsetof>) | deslocamento em bytes do início de um tipo struct para o membro especificado
(macro de função)
Definido no cabeçalho `<stdbool.h>`
bool(C99)(removido em C23) | macro de conveniência, expande para [`_Bool`](<#/doc/keyword/_Bool>)
(macro de palavra-chave)
true(C99)(removido em C23) | expande para a constante inteira 1
(macro constante)
false(C99)(removido em C23) | expande para a constante inteira ​0​
(macro constante)
__bool_true_false_are_defined(C99)(obsoleto em C23) | expande para a constante inteira 1
(macro constante)
Definido no cabeçalho `<stdalign.h>`
alignas(C11)(removido em C23) | macro de conveniência, expande para a palavra-chave [`_Alignas`](<#/doc/keyword/_Alignas>)
(macro de palavra-chave)
alignof(C11)(removido em C23) | macro de conveniência, expande para a palavra-chave [`_Alignof`](<#/doc/keyword/_Alignof>)
(macro de palavra-chave)
__alignas_is_defined(C11)(removido em C23) | expande para a constante inteira 1
(macro constante)
__alignof_is_defined(C11)(removido em C23) | expande para a constante inteira 1
(macro constante)
Definido no cabeçalho `[`<stdnoreturn.h>`](<#/doc/language/_Noreturn>)`
noreturn(C11)(obsoleto em C23) | macro de conveniência, expande para [`_Noreturn`](<#/doc/keyword/_Noreturn>)
(macro de palavra-chave)

#### [Tipos inteiros de largura fixa](<#/doc/types/integer>) (desde C99)

#### [Limites numéricos](<#/doc/types/limits>)

### Notas

O tipo de true e false é int em vez de _Bool. Um programa pode indefinir e talvez redefinir as macros bool, true e false. No entanto, tal capacidade é um recurso obsoleto. | (desde C99)
(até C23)
O tipo de true e false é bool. Não é especificado se qualquer um de bool, _Bool, true ou false é implementado como uma macro predefinida. Se bool, true ou false (mas não _Bool) for definido como uma macro predefinida, um programa pode indefinir e talvez redefini-lo. | (desde C23)

### Exemplo

Execute este código
```c
    #include <stdalign.h>
    #include <stdbool.h>
    #include <stdio.h>
    
    int main(void)
    {
        printf("%d %d %d\n", true && false, true || false, !false);
        printf("%d %d\n", true ^ true, true + true);
        printf("%zu\n", alignof(short));
    }
```

Saída possível:
```
    0 1 1
    0 2
    2
```

### Referências

  * C23 standard (ISO/IEC 9899:2024):

    

  * 7.15 Alignment <stdalign.h> (p: TBD)

    

  * 7.18 Boolean type and values <stdbool.h> (p: TBD)

    

  * 7.19 Common definitions <stddef.h> (p: TBD)

    

  * 7.23 _Noreturn <stdnoreturn.h> (p: TBD)

    

  * 7.31.9 Boolean type and values <stdbool.h> (p: TBD)

  * C17 standard (ISO/IEC 9899:2018):

    

  * 7.15 Alignment <stdalign.h> (p: 196)

    

  * 7.18 Boolean type and values <stdbool.h> (p: 210)

    

  * 7.19 Common definitions <stddef.h> (p: 211)

    

  * 7.23 _Noreturn <stdnoreturn.h> (p: 263)

    

  * 7.31.9 Boolean type and values <stdbool.h> (p: 332)

  * C11 standard (ISO/IEC 9899:2011):

    

  * 7.15 Alignment <stdalign.h> (p: 268)

    

  * 7.18 Boolean type and values <stdbool.h> (p: 287)

    

  * 7.19 Common definitions <stddef.h> (p: 288)

    

  * 7.23 _Noreturn <stdnoreturn.h> (p: 361)

    

  * 7.31.9 Boolean type and values <stdbool.h> (p: 456)

  * C99 standard (ISO/IEC 9899:1999):

    

  * 7.18 Boolean type and values <stdbool.h> (p: 253)

    

  * 7.19 Common definitions <stddef.h> (p: 254)

    

  * 7.26.7 Boolean type and values <stdbool.h> (p: 401)

  * C89/C90 standard (ISO/IEC 9899:1990):

    

  * 4.1.5 Common definitions <stddef.h>

### Veja também

[Documentação C++](<#/>) para a biblioteca de suporte a tipos
---