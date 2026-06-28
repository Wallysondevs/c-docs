# char32_t

Definido no cabeçalho [`<uchar.h>`](<#/doc/string/multibyte>)

```c
typedef uint_least32_t char32_t;  // desde C11
```

  
char32_t é um tipo inteiro sem sinal usado para caracteres de 32 bits de largura e é do mesmo tipo que [uint_least32_t](<#/doc/types/integer>). 

### Notas

Em qualquer plataforma, pela definição de [uint_least32_t](<#/doc/types/integer>), a largura do tipo char32_t pode ser maior que 32 bits, mas os valores reais armazenados em um objeto do tipo char32_t sempre terão uma largura de 32 bits. 

### Exemplo

Execute este código
```
    #include <stdio.h>
    #include <uchar.h>
     
    int main(void)
    {
        const char32_t wc[] = U"zß水🍌"; // or "z\u00df\u6c34\U0001f34c"
        const size_t wc_sz = sizeof wc / sizeof *wc;
        printf("%zu UTF-32 code units: [ ", wc_sz);
        for (size_t n = 0; n < wc_sz; ++n)
            printf("%#x ", wc[n]);
        printf("]\n");
    }
```

Saída possível: 
```
    5 UTF-32 code units: [ 0x7a 0xdf 0x6c34 0x1f34c 0 ]
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.28 Utilitários Unicode <uchar.h> (p: 292) 

    

  * 7.20.1.2 Tipos inteiros de largura mínima (p: 212-213) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.28 Utilitários Unicode <uchar.h> (p: 398) 

    

  * 7.20.1.2 Tipos inteiros de largura mínima (p: 290) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.18.1.2 Tipos inteiros de largura mínima (p: 256) 

### Veja também

[documentação C++](<#/>) para Tipos Fundamentais  
---