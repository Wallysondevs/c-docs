# max_align_t

Definido no cabeçalho [`<stddef.h>`](<#/doc/types>)

```c
typedef /*implementation-defined*/ max_align_t;  // desde C11
```

`max_align_t` é um tipo cujo requisito de alinhamento é pelo menos tão rigoroso (tão grande) quanto o de todo tipo escalar.

### Observações

Ponteiros retornados por funções de alocação como [malloc](<#/doc/memory/malloc>) são adequadamente alinhados para qualquer objeto, o que significa que eles são alinhados pelo menos tão rigorosamente quanto `max_align_t`.

### Exemplo

Execute este código
```c
    #include <inttypes.h>
    #include <stdalign.h>
    #include <stddef.h>
    #include <stdint.h>
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(void)
    {
        size_t a = alignof(max_align_t);
        printf("Alignment of max_align_t is %zu (%#zx)\n", a, a);
    
        void *p = malloc(123);
        printf("The address obtained from malloc(123) is %#"PRIxPTR"\n",
                (uintptr_t)p);
        free(p);
    }
```

Saída possível:
```
    Alignment of max_align_t is 16 (0x10)
    The address obtained from malloc(123) is 0x1fa67010
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.19 Definições comuns <stddef.h> (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.19 Definições comuns <stddef.h> (p: 211)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.19 Definições comuns <stddef.h> (p: 288)

### Veja também

Documentação C++ para [max_align_t](<#/>)
---