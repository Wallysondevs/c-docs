# Tipos inteiros de largura fixa (desde C99)

### Tipos
  
Definido no cabeçalho `<stdint.h>`  
---  
`int8_t`  
`int16_t`  
`int32_t`  
`int64_t` | tipo inteiro com sinal com largura de  
exatamente 8, 16, 32 e 64 bits, respectivamente,  
sem bits de preenchimento e usando complemento de 2 para valores negativos  
(fornecido apenas se a implementação suportar diretamente o tipo)   
`int_fast8_t`  
`int_fast16_t`  
`int_fast32_t`  
`int_fast64_t` | tipo inteiro com sinal mais rápido com largura de  
pelo menos 8, 16, 32 e 64 bits, respectivamente   
`int_least8_t`  
`int_least16_t`  
`int_least32_t`  
`int_least64_t` | menor tipo inteiro com sinal com largura de  
pelo menos 8, 16, 32 e 64 bits, respectivamente   
`intmax_t` | tipo inteiro de largura máxima   
`intptr_t` | tipo inteiro capaz de armazenar um ponteiro   
`uint8_t`  
`uint16_t`  
`uint32_t`  
`uint64_t` | tipo inteiro sem sinal com largura de  
exatamente 8, 16, 32 e 64 bits, respectivamente   
(fornecido apenas se a implementação suportar diretamente o tipo)   
`uint_fast8_t`  
`uint_fast16_t`  
`uint_fast32_t`  
`uint_fast64_t` | tipo inteiro sem sinal mais rápido com largura de  
pelo menos 8, 16, 32 e 64 bits, respectivamente   
`uint_least8_t`  
`uint_least16_t`  
`uint_least32_t`  
`uint_least64_t` | menor tipo inteiro sem sinal com largura de  
pelo menos 8, 16, 32 e 64 bits, respectivamente   
`uintmax_t` | tipo inteiro sem sinal de largura máxima   
`uintptr_t` | tipo inteiro sem sinal capaz de armazenar um ponteiro   
  
A implementação pode definir nomes de typedef `int _N_ _t`, `int_fast _N_ _t`, `int_least _N_ _t`, `uint _N_ _t`, `uint_fast _N_ _t` e `uint_least _N_ _t` quando _N_ não for 8, 16, 32 ou 64. Nomes de typedef na forma `int _N_ _t` só podem ser definidos se a implementação suportar um tipo inteiro dessa largura sem preenchimento. Assim, `uint24_t` denota um tipo inteiro sem sinal com uma largura de exatamente 24 bits. 

Cada uma das macros listadas abaixo é definida se e somente se a implementação definir o nome de typedef correspondente. As macros `INT _N_ _C` e `UINT _N_ _C` correspondem aos nomes de typedef `int_least _N_ _t` e `uint_least _N_ _t`, respectivamente. 

### Constantes de macro

Definido no cabeçalho `<stdint.h>`  
---  
  
##### Inteiros com sinal: largura   
  
INT8_WIDTHINT16_WIDTHINT32_WIDTHINT64_WIDTH(C23)(opcional) | largura em bits de um objeto do tipo int8_t, int16_t, int32_t, int64_t (exatamente 8, 16, 32, 64)   
(constante de macro)  
INT_FAST8_WIDTHINT_FAST16_WIDTHINT_FAST32_WIDTHINT_FAST64_WIDTH(C23) | largura em bits de um objeto do tipo int_fast8_t, int_fast16_t, int_fast32_t, int_fast64_t   
(constante de macro)  
INT_LEAST8_WIDTHINT_LEAST16_WIDTHINT_LEAST32_WIDTHINT_LEAST64_WIDTH(C23) | largura em bits de um objeto do tipo int_least8_t, int_least16_t, int_least32_t, int_least64_t   
(constante de macro)  
INTPTR_WIDTH(C23)(opcional) | largura em bits de um objeto do tipo intptr_t   
(constante de macro)  
INTMAX_WIDTH(C23) | largura em bits de um objeto do tipo intmax_t   
(constante de macro)  
  
##### Inteiros com sinal: valor mínimo   
  
INT8_MININT16_MININT32_MININT64_MIN | valor mínimo de um objeto do tipo int8_t, int16_t, int32_t, int64_t   
(constante de macro)  
INT_FAST8_MININT_FAST16_MININT_FAST32_MININT_FAST64_MIN | valor mínimo de um objeto do tipo int_fast8_t, int_fast16_t, int_fast32_t, int_fast64_t   
(constante de macro)  
INT_LEAST8_MININT_LEAST16_MININT_LEAST32_MININT_LEAST64_MIN | valor mínimo de um objeto do tipo int_least8_t, int_least16_t, int_least32_t, int_least64_t   
(constante de macro)  
INTPTR_MIN | valor mínimo de um objeto do tipo intptr_t   
(constante de macro)  
INTMAX_MIN | valor mínimo de um objeto do tipo intmax_t   
(constante de macro)  
  
##### Inteiros com sinal: valor máximo   
  
INT8_MAXINT16_MAXINT32_MAXINT64_MAX | valor máximo de um objeto do tipo int8_t, int16_t, int32_t, int64_t   
(constante de macro)  
INT_FAST8_MAXINT_FAST16_MAXINT_FAST32_MAXINT_FAST64_MAX | valor máximo de um objeto do tipo int_fast8_t, int_fast16_t, int_fast32_t, int_fast64_t   
(constante de macro)  
INT_LEAST8_MAXINT_LEAST16_MAXINT_LEAST32_MAXINT_LEAST64_MAX | valor máximo de um objeto do tipo int_least8_t, int_least16_t, int_least32_t, int_least64_t   
(constante de macro)  
INTPTR_MAX | valor máximo de um objeto do tipo intptr_t   
(constante de macro)  
INTMAX_MAX | valor máximo de um objeto do tipo intmax_t   
(constante de macro)  
  
##### Inteiros sem sinal: largura   
  
UINT8_WIDTHUINT16_WIDTHUINT32_WIDTHUINT64_WIDTH(C23)(opcional) | largura em bits de um objeto do tipo uint8_t, uint16_t, uint32_t, uint64_t (exatamente 8, 16, 32, 64)   
(constante de macro)  
UINT_FAST8_WIDTHUINT_FAST16_WIDTHUINT_FAST32_WIDTHUINT_FAST64_WIDTH(C23) | largura em bits de um objeto do tipo uint_fast8_t, uint_fast16_t, uint_fast32_t, uint_fast64_t   
(constante de macro)  
UINT_LEAST8_WIDTHUINT_LEAST16_WIDTHUINT_LEAST32_WIDTHUINT_LEAST64_WIDTH(C23) | largura em bits de um objeto do tipo uint_least8_t, uint_least16_t, uint_least32_t, uint_least64_t   
(constante de macro)  
UINTPTR_WIDTH(C23)(opcional) | largura em bits de um objeto do tipo uintptr_t   
(constante de macro)  
UINTMAX_WIDTH(C23) | largura em bits de um objeto do tipo uintmax_t   
(constante de macro)  
  
##### Inteiros sem sinal: valor máximo   
  
UINT8_MAXUINT16_MAXUINT32_MAXUINT64_MAX | valor máximo de um objeto do tipo uint8_t, uint16_t, uint32_t, uint64_t   
(constante de macro)  
UINT_FAST8_MAXUINT_FAST16_MAXUINT_FAST32_MAXUINT_FAST64_MAX | valor máximo de um objeto do tipo uint_fast8_t, uint_fast16_t, uint_fast32_t, uint_fast64_t   
(constante de macro)  
UINT_LEAST8_MAXUINT_LEAST16_MAXUINT_LEAST32_MAXUINT_LEAST64_MAX | valor máximo de um objeto do tipo uint_least8_t, uint_least16_t, uint_least32_t, uint_least64_t   
(constante de macro)  
UINTPTR_MAX | valor máximo de um objeto do tipo uintptr_t   
(constante de macro)  
UINTMAX_MAX | valor máximo de um objeto do tipo uintmax_t   
(constante de macro)  
  
### Macros de função para constantes inteiras de largura mínima

INT8_CINT16_CINT32_CINT64_C | expande para uma expressão constante inteira com o valor especificado por seu argumento e o tipo int_least8_t, int_least16_t, int_least32_t, int_least64_t, respectivamente   
(macro de função)  
INTMAX_C | expande para uma expressão constante inteira com o valor especificado por seu argumento e o tipo intmax_t   
(macro de função)  
UINT8_CUINT16_CUINT32_CUINT64_C | expande para uma expressão constante inteira com o valor especificado por seu argumento e o tipo uint_least8_t, uint_least16_t, uint_least32_t, uint_least64_t, respectivamente   
(macro de função)  
UINTMAX_C | expande para uma expressão constante inteira com o valor especificado por seu argumento e o tipo uintmax_t   
(macro de função)
```c
    #include <stdint.h>
    UINT64_C(0x123) // might expand to 0x123ULL or 0x123UL
```  
  
### Constantes de macro de formato

Definido no cabeçalho `<inttypes.h>`  
---  
  
#### Constantes de formato para a família de funções [fprintf](<#/doc/io/fprintf>)

Cada uma das macros `PRI` listadas aqui é definida se e somente se a implementação definir o nome de typedef correspondente. 

Equivalente  
para int ou  
unsigned int | Descrição  | Macros para tipos de dados   
  
  
  
  
`[u]int**x** _t`  
  
  
  
| `[u]int_least**x** _t` | `[u]int_fast**x** _t` | `[u]intmax_t` | `[u]intptr_t`  
`d` | saída de um valor inteiro decimal com sinal  | PRId**x** | PRIdLEAST**x** | PRIdFAST**x** | PRIdMAX  | PRIdPTR   
`i` | PRIi**x** | PRIiLEAST**x** | PRIiFAST**x** | PRIiMAX  | PRIiPTR   
`u` | saída de um valor inteiro decimal sem sinal  | PRIu**x** | PRIuLEAST**x** | PRIuFAST**x** | PRIuMAX  | PRIuPTR   
`o` | saída de um valor inteiro octal sem sinal  | PRIo**x** | PRIoLEAST**x** | PRIoFAST**x** | PRIoMAX  | PRIoPTR   
`x` | saída de um valor inteiro hexadecimal sem sinal em minúsculas  | PRIx**x** | PRIxLEAST**x** | PRIxFAST**x** | PRIxMAX  | PRIxPTR   
`X` | saída de um valor inteiro hexadecimal sem sinal em maiúsculas  | PRIX**x** | PRIXLEAST**x** | PRIXFAST**x** | PRIXMAX  | PRIXPTR   
  
#### Constantes de formato para a família de funções [fscanf](<#/doc/io/fscanf>)

Cada uma das macros `SCN` listadas aqui é definida se e somente se a implementação definir o nome de typedef correspondente e tiver um modificador de comprimento [fscanf](<#/doc/io/fscanf>) adequado para o tipo. 

Equivalente  
para int ou  
unsigned int | Descrição  | Macros para tipos de dados   
  
  
  
  
`[u]int**x** _t`  
  
  
  
| `[u]int_least**x** _t` | `[u]int_fast**x** _t` | `[u]intmax_t` | `[u]intptr_t`  
`d` | entrada de um valor inteiro decimal com sinal  | SCNd**x** | SCNdLEAST**x** | SCNdFAST**x** | SCNdMAX  | SCNdPTR   
`i` | entrada de um valor inteiro com sinal (a base é determinada pelos primeiros caracteres analisados)  | SCNi**x** | SCNiLEAST**x** | SCNiFAST**x** | SCNiMAX  | SCNiPTR   
`u` | entrada de um valor inteiro decimal sem sinal  | SCNu**x** | SCNuLEAST**x** | SCNuFAST**x** | SCNuMAX  | SCNuPTR   
`o` | entrada de um valor inteiro octal sem sinal  | SCNo**x** | SCNoLEAST**x** | SCNoFAST**x** | SCNoMAX  | SCNoPTR   
`x` | entrada de um valor inteiro hexadecimal sem sinal  | SCNx**x** | SCNxLEAST**x** | SCNxFAST**x** | SCNxMAX  | SCNxPTR   
  
### Exemplo

Veja também a [nota de compatibilidade C++](<#/>) sobre espaços antes das [macros de formato](<#/doc/types/integer>) usadas neste exemplo.

Execute este código
```c
    #include <inttypes.h>
    #include <stdio.h>
     
    int main(void)
    {
        printf("%zu\n", sizeof(int64_t));
        printf("%s\n", PRId64);
        printf("%+" PRId64 "\n", INT64_MIN);
        printf("%+" PRId64 "\n", INT64_MAX);
     
        int64_t n = 7;
        printf("%+" PRId64 "\n", n);
    }
```

Saída possível: 
```
    8
    lld
    -9223372036854775808
    +9223372036854775807
    +7
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.8.1 Macros para especificadores de formato (p: TBD) 

    

  * 7.18 Tipos inteiros <stdint.h> (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.8.1 Macros para especificadores de formato (p: 158-159) 

    

  * 7.18 Tipos inteiros <stdint.h> (p: 212-216) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.8.1 Macros para especificadores de formato (p: 217-218) 

    

  * 7.18 Tipos inteiros <stdint.h> (p: 289-295) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.8.1 Macros para especificadores de formato (p: 198-199) 

    

  * 7.18 Tipos inteiros <stdint.h> (p: 255-261) 

### Veja também

  * [Tipos aritméticos](<#/doc/language/arithmetic_types>)

[Documentação C++](<#/>) para Tipos inteiros de largura fixa  
---  
[Documentação C++](<#/>) para Literais definidos pelo usuário ([nota sobre macros de formatação](<#/>))