# operador sizeof

Consulta o tamanho do objeto ou tipo.

Usado quando o tamanho real do objeto precisa ser conhecido.

### Sintaxe

---
`sizeof(` type `)` | (1) |
`sizeof` expression ` | (2) |

Ambas as versões retornam um valor do tipo [size_t](<#/doc/types/size_t>).

### Explicação

1) Retorna o tamanho, em bytes, da [representação do objeto](<#/doc/language/object>) do tipo

2) Retorna o tamanho, em bytes, da representação do objeto do tipo da expressão. Nenhuma conversão implícita é aplicada à expressão.

### Notas

Dependendo da arquitetura do computador, um [byte](<https://en.wikipedia.org/wiki/byte> "enwiki:byte") pode consistir em 8 ou mais bits, o número exato fornecido como [CHAR_BIT](<#/doc/types/limits>).

sizeof(char), sizeof(signed char) e sizeof(unsigned char) sempre retornam 1.

sizeof não pode ser usado com tipos de função, tipos incompletos (incluindo void), ou lvalues de [campo de bits](<#/doc/language/bit_field>).

Quando aplicado a um operando que possui tipo [struct](<#/doc/language/struct>) ou [union](<#/doc/language/union>), o resultado é o número total de bytes em tal objeto, incluindo preenchimento interno e final. O preenchimento final é tal que, se o objeto fosse um elemento de um array, o requisito de alinhamento do próximo elemento deste array seria satisfeito, em outras palavras, sizeof(T) retorna o tamanho de um elemento de um array T[].

Se o tipo for um tipo [VLA](<#/doc/language/array>) e a alteração do valor de sua expressão de tamanho não afetaria o resultado de `sizeof`, é não especificado se a expressão de tamanho é avaliada ou não. | (desde C99)
Exceto se o tipo da expressão for um [VLA](<#/doc/language/array>),(desde C99) a expressão não é avaliada e o operador `sizeof` pode ser usado em uma [expressão constante](<#/doc/language/constant_expression>) inteira.

Se o tipo da expressão for um tipo de [array de tamanho variável](<#/doc/language/array>), a expressão é avaliada e o tamanho do array ao qual ela se avalia é calculado em tempo de execução. | (desde C99)
O número de elementos em qualquer [array](<#/doc/language/array>) a, incluindo VLA (desde C99), pode ser determinado com a expressão sizeof a / sizeof a[0]. Note que se a tiver tipo ponteiro (como após a conversão de array para ponteiro ou ajuste de tipo de parâmetro de função), esta expressão simplesmente dividiria o número de bytes em um tipo ponteiro pelo número de bytes no tipo apontado.

### Palavras-chave

[`sizeof`](<#/doc/keyword/sizeof>)

### Exemplo

A saída de exemplo corresponde a uma plataforma com ponteiros de 64 bits e int de 32 bits

Execute este código
```c
    #include <stdio.h>
    
    int main(void)
    {
        short x;
        // type argument:
        printf("sizeof(float)          = %zu\n", sizeof(float));
        printf("sizeof(void(*)(void))  = %zu\n", sizeof(void(*)(void)));
        printf("sizeof(char[10])       = %zu\n", sizeof(char[10]));
    //  printf("sizeof(void(void))     = %zu\n", sizeof(void(void))); // Error: function type
    //  printf("sizeof(char[])         = %zu\n", sizeof(char[])); // Error: incomplete type
    
        // expression argument:
        printf("sizeof 'a'             = %zu\n", sizeof 'a'); // type of 'a' is int
    //  printf("sizeof main            = %zu\n", sizeof main); // Error: Function type
        printf("sizeof &main           = %zu\n", sizeof &main);
        printf("sizeof "hello"         = %zu\n", sizeof "hello"); // type is char[6]
        printf("sizeof x               = %zu\n", sizeof x); // type of x is short
        printf("sizeof (x+1)           = %zu\n", sizeof(x + 1)); // type of x+1 is int
    }
```

Saída possível:
```
    sizeof(float)          = 4
    sizeof(void(*)(void))  = 8
    sizeof(char[10])       = 10
    sizeof 'a'             = 4
    sizeof &main           = 8
    sizeof "hello"         = 6
    sizeof x               = 2
    sizeof (x+1)           = 4
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 6.5.3.4 Os operadores sizeof e alignof (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 6.5.3.4 Os operadores sizeof e _Alignof (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 6.5.3.4 Os operadores sizeof e _Alignof (p: 90-91)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 6.5.3.4 O operador sizeof (p: 80-81)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 3.3.3.4 O operador sizeof

### Veja também

[Documentação C++](<#/>) para o operador `sizeof`
---