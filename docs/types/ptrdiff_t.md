# ptrdiff_t

Definido no cabeçalho [`<stddef.h>`](<#/doc/types>)

```c
typedef /*implementation-defined*/ ptrdiff_t;
```

`ptrdiff_t` é o tipo inteiro com sinal do resultado da [subtração de dois ponteiros](<#/doc/language/operator_arithmetic>).

A largura em bits de `ptrdiff_t` não é menor que 17. | (desde C99)
(até C23)
A largura em bits de `ptrdiff_t` não é menor que 16. | (desde C23)

### Notas

`ptrdiff_t` é usado para aritmética de ponteiros e indexação de arrays, se valores negativos forem possíveis. Programas que usam outros tipos, como int, podem falhar, por exemplo, em sistemas de 64 bits quando o índice excede [INT_MAX](<#/doc/types/limits>) ou se dependem de aritmética modular de 32 bits.

Apenas ponteiros para elementos do mesmo array (incluindo o ponteiro um após o final do array) podem ser subtraídos um do outro.

Se um array for tão grande (maior que [PTRDIFF_MAX](<#/doc/types/limits>) elementos, mas igual ou menor que [SIZE_MAX](<#/doc/types/limits>) bytes), que a diferença entre dois ponteiros pode não ser representável como `ptrdiff_t`, o resultado da subtração de dois desses ponteiros é comportamento indefinido.

Para arrays de char menores que [PTRDIFF_MAX](<#/doc/types/limits>), `ptrdiff_t` atua como a contraparte com sinal de [size_t](<#/doc/types/size_t>): ele pode armazenar o tamanho do array de qualquer tipo e é, na maioria das plataformas, sinônimo de `intptr_t`).

### Implementação possível
```c
    typedef typeof((int*)nullptr - (int*)nullptr) ptrdiff_t; // valid since C23
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
        const size_t N = 100;
        int numbers[N];
    
        printf("PTRDIFF_MAX = %ld\n", PTRDIFF_MAX);
        int *p1 = &numbers[18], *p2 = &numbers[23];
        ptrdiff_t diff = p2 - p1;
        printf("p2-p1 = %td\n", diff);
    }
```

Saída possível:
```
    PTRDIFF_MAX = 9223372036854775807
    p2-p1 = 5
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

[ size_t](<#/doc/types/size_t>) | tipo inteiro sem sinal retornado pelo operador [`sizeof`](<#/doc/language/sizeof>)
(typedef)
[ offsetof](<#/doc/types/offsetof>) | deslocamento em bytes do início de um tipo struct para o membro especificado
(macro de função)
[Documentação C++](<#/>) para ptrdiff_t