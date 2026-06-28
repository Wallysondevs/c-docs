# NULL

Definido no cabeçalho [`<locale.h>`](<#/doc/locale>)

```c
Definido no cabeçalho ``<stddef.h>``
Definido no cabeçalho ``<stdio.h>``
Definido no cabeçalho ``<stdlib.h>``
Definido no cabeçalho ``<string.h>``
Definido no cabeçalho ``<time.h>``
Definido no cabeçalho ``<wchar.h>``
#define NULL /*implementation-defined*/
```

A macro `NULL` é uma constante de ponteiro nulo definida pela implementação, que pode ser

*   uma [expressão constante](<#/doc/language/constant_expression>) inteira com o valor ​0​
*   uma expressão constante inteira com o valor ​0​ [convertida para o tipo](<#/doc/language/conversion>) void*
*   constante pré-definida [`nullptr`](<#/doc/language/nullptr>)

| (desde C23)

Uma constante de ponteiro nulo pode ser [convertida](<#/doc/language/conversion>) para qualquer tipo de ponteiro; tal conversão resulta no valor de ponteiro nulo desse tipo.

### Notas

[POSIX exige](<https://pubs.opengroup.org/onlinepubs/9699919799/basedefs/stddef.h.html>) que `NULL` seja definido como uma expressão constante inteira com o valor ​0​ convertida para void*.

### Possível implementação
```
    // Compatível com C++:
    #define NULL 0
    // Incompatível com C++:
    #define NULL (10*2 - 20)
    #define NULL ((void*)0)
    // desde C23 (compatível com C++11 e posterior)
    #define NULL nullptr
```

---

### Exemplo

Execute este código
```
    #include <inttypes.h>
    #include <stdint.h>
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(void)
    {
        // qualquer tipo de ponteiro pode ser definido como NULL
        int* p = NULL;
        struct S *s = NULL;
        void(*f)(int, double) = NULL;
        printf("%p %p %p\n", (void*)p, (void*)s, (void*)(long)f);
    
        // muitas funções que retornam ponteiros usam ponteiros nulos para indicar erro
        char *ptr = malloc(0xFULL);
        if (ptr == NULL)
            printf("Sem memória");
        else
            printf("ptr = %#"PRIxPTR"\n", (uintptr_t)ptr);
        free(ptr);
    }
```

Saída possível:
```
    (nil) (nil) (nil)
    ptr = 0xc001cafe
```

### Veja também

[ nullptr_t](<#/doc/types/nullptr_t>)(C23) | o tipo da constante de ponteiro nulo pré-definida [`nullptr`](<#/doc/language/nullptr>)
(typedef)
[Documentação C++](<#/>) para NULL