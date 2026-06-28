# size_t

Definido no cabeçalho [`<stddef.h>`](<#/doc/types>)

```c
Definido no cabeçalho ``<stdio.h>``
Definido no cabeçalho ``<stdlib.h>``
Definido no cabeçalho ``<string.h>``
Definido no cabeçalho ``<time.h>``
Definido no cabeçalho ``<uchar.h>``  // desde C11
Definido no cabeçalho ``<wchar.h>``  // desde C95
typedef /*implementation-defined*/ size_t;
```

  
`size_t` é o tipo inteiro sem sinal do resultado de [`sizeof`](<#/doc/language/sizeof>), [offsetof](<#/doc/types/offsetof>) e _Alignof(até C23)alignof(desde C23), dependendo do [modelo de dados](<#/doc/language/arithmetic_types>). 

A largura em bits de `size_t` não é menor que 16.  | (desde C99)  
  
### Notas

`size_t` pode armazenar o tamanho máximo de um objeto teoricamente possível de qualquer tipo (incluindo array). 

`size_t` é comumente usado para indexação de arrays e contagem de loops. Programas que usam outros tipos, como unsigned int, para indexação de arrays podem falhar em, por exemplo, sistemas de 64 bits quando o índice excede [UINT_MAX](<#/doc/types/limits>) ou se dependem de aritmética modular de 32 bits. 

### Implementação possível
```c
    typedef typeof(sizeof(0)) size_t; // valid since C23
```
  
---  
  
### Exemplo

Execute este código
```c
    #include <stddef.h>
    #include <stdint.h>
    #include <stdio.h>
     
    int main(void)
    {
        const size_t N = 101;
        int numbers[N];
        size_t sum = 0;
        for (size_t ndx = 0; ndx < N; ++ndx)
            sum += numbers[ndx] = ndx;
        size_t size = sizeof numbers;
        printf("sum = %zu\n", sum);
        printf("size = %zu\n", size);
        printf("SIZE_MAX = %zu\n", SIZE_MAX);
    }
```

Saída possível: 
```
    sum = 5050
    size = 404
    SIZE_MAX = 18446744073709551615
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.19 Definições comuns <stddef.h> (p: TBD) 

    

  * 7.20.3 Limites de outros tipos inteiros (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.19 Definições comuns <stddef.h> (p: 211) 

    

  * 7.20.3 Limites de outros tipos inteiros (p: 215) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.19 Definições comuns <stddef.h> (p: 288) 

    

  * 7.20.3 Limites de outros tipos inteiros (p: 293) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.17 Definições comuns <stddef.h> (p: 253) 

    

  * 7.18.3 Limites de outros tipos inteiros (p: 258) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.1.6 Definições comuns <stddef.h>

### Veja também

[ ptrdiff_t](<#/doc/types/ptrdiff_t>) |  tipo inteiro com sinal retornado ao subtrair dois ponteiros   
(typedef)  
[ offsetof](<#/doc/types/offsetof>) |  deslocamento em bytes do início de um tipo struct para o membro especificado   
(macro de função)  
[documentação C++](<#/>) para size_t