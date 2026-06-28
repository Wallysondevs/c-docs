# char16_t

Definido no cabeçalho [`<uchar.h>`](<#/doc/string/multibyte>)

```c
typedef uint_least16_t char16_t;  // desde C11
```

char16_t é um tipo inteiro sem sinal usado para caracteres de 16 bits e é o mesmo tipo que [uint_least16_t](<#/doc/types/integer>).

### Notas

Em qualquer plataforma, pela definição de [uint_least16_t](<#/doc/types/integer>), a largura do tipo char16_t pode ser maior que 16 bits, mas os valores reais armazenados em um objeto do tipo char16_t sempre terão uma largura de 16 bits.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <uchar.h>
    
    int main(void)
    {
        const char16_t wcs[] = u"zß水🍌"; // or "z\u00df\u6c34\U0001f34c"
        const size_t wcs_sz = sizeof wcs / sizeof *wcs;
        printf("%zu UTF-16 code units: [ ", wcs_sz);
        for (size_t n = 0; n < wcs_sz; ++n)
            printf("%#x ", wcs[n]);
        printf("]\n");
    }
```

Saída possível:
```
    6 UTF-16 code units: [ 0x7a 0xdf 0x6c34 0xd83c 0xdf4c 0 ]
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

[Documentação C++](<#/>) para Tipos fundamentais 
---