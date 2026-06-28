# char8_t

Definido no cabeçalho [`<uchar.h>`](<#/doc/string/multibyte>)

```c
typedef unsigned char char8_t;  // desde C23
```

char8_t é um tipo inteiro sem sinal usado para UTF-8 e é do mesmo tipo que unsigned char.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <uchar.h>
     
    int main(void)
    {
        char8_t str[] = u8"zß水🍌"; // or "z\u00df\u6c34\U0001f34c"
        size_t str_sz = sizeof str; // sizeof *str == 1 by definition
        printf("%zu UTF-8 code units: [ ", str_sz);
        for (size_t n = 0; n < str_sz; ++n)
            printf("%02X ", str[n]);
        printf("]\n");
    }
```

Saída possível:
```
    11 UTF-8 code units: [ 7A C3 9F E6 B0 B4 F0 9F 8D 8C 00 ]
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.30 Utilitários Unicode <uchar.h> (p: 410)

### Veja também

[Documentação C++](<#/>) para Tipos Fundamentais
---