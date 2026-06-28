# Campos de bits

Declara um membro com largura explícita, em bits. Membros de campo de bits adjacentes podem ser empacotados para compartilhar e atravessar bytes individuais.

Uma declaração de campo de bits é uma declaração de membro de [struct](<#/doc/language/struct>) ou [union](<#/doc/language/union>) que usa o seguinte [declarador](<#/doc/language/declarations>):

---
identifier ﻿(opcional) `:` width
- **identifier** — um nome para o campo de bits que está sendo declarado. O nome é opcional: campos de bits sem nome introduzem o número especificado de bits de preenchimento.
- **width** — uma [expressão constante](<#/doc/language/constant_expression>) inteira com um valor maior ou igual a zero e menor ou igual ao número de bits no tipo subjacente. Quando maior que zero, este é o número de bits que este campo de bits ocupará. O valor zero é permitido apenas para campos de bits sem nome e tem um significado especial: ele especifica que o próximo campo de bits na definição da classe começará no limite de uma unidade de alocação.

### Explicação

Campos de bits podem ter apenas um dos seguintes tipos (possivelmente qualificados com [const](<#/doc/language/const>) ou [volatile](<#/doc/language/volatile>)):

*   `unsigned int`, para campos de bits sem sinal (ex: `unsigned int b : 3;` tem o intervalo `[`​0​`, `7`]`)
*   `signed int`, para campos de bits com sinal (`signed int b : 3;` tem o intervalo `[`-4`, `3`]`)
*   `int`, para campos de bits com sinalização definida pela implementação (note que isso difere do significado da palavra-chave `int` em todos os outros lugares, onde significa "signed int"). Por exemplo, `int b : 3;` pode ter o intervalo de valores `[`​0​`, `7`]` ou `[`-4`, `3`]`.
*   `_Bool`, para campos de bits de um único bit (ex: `bool x : 1;`) tem o intervalo `[`​0​`, `1`]` e as [conversões implícitas](<#/doc/language/conversion>) para e a partir dele seguem as regras de conversão booleana.

| (desde C99)
*   tipos inteiros de precisão de bits (ex: `_BitInt(5) : 4;` tem o intervalo `[`-8`, `7`]` e `unsigned _BitInt(5) : 4;` tem o intervalo `[`​0​`, `15`]`).

| (desde C23)

Tipos adicionais definidos pela implementação podem ser aceitáveis. Também é definido pela implementação se um campo de bits pode ter um tipo [atomic](<#/doc/language/atomic>). (desde C11) O número de bits em um campo de bits (largura) define o limite para o intervalo de valores que ele pode conter:

Run this code
```c
    #include <stdio.h>
    
    struct S
    {
        // campo sem sinal de três bits,
        // valores permitidos são 0...7
        unsigned int b : 3;
    };
    
    int main(void)
    {
        struct S s = {7};
        ++s.b; // estouro de unsigned
        printf("%d\n", s.b); // saída: 0
    }
```

Múltiplos campos de bits adjacentes são permitidos (e geralmente são) empacotados juntos:

Run this code
```c
    #include <stdio.h>
    
    struct S
    {
        // geralmente ocupará 4 bytes:
        // 5 bits: valor de b1
        // 11 bits: não utilizados
        // 6 bits: valor de b2
        // 2 bits: valor de b3
        // 8 bits: não utilizados
        unsigned b1 : 5, : 11, b2 : 6, b3 : 2;
    };
    
    int main(void)
    {
        printf("%zu\n", sizeof(struct S)); // geralmente imprime 4
    }
```

O _campo de bits sem nome_ especial de largura zero quebra o preenchimento: ele especifica que o próximo campo de bits começa no início da próxima unidade de alocação:

Run this code
```c
    #include <stdio.h>
    
    struct S
    {
        // geralmente ocupará 8 bytes:
        // 5 bits: valor de b1
        // 27 bits: não utilizados
        // 6 bits: valor de b2
        // 15 bits: valor de b3
        // 11 bits: não utilizados
        unsigned b1 : 5;
        unsigned    : 0; // inicia um novo unsigned int
        unsigned b2 : 6;
        unsigned b3 : 15;
    };
    
    int main(void)
    {
        printf("%zu\n", sizeof(struct S)); // geralmente imprime 8
    }
```

Como os campos de bits não necessariamente começam no início de um byte, o endereço de um campo de bits não pode ser obtido. Ponteiros para campos de bits não são possíveis. Campos de bits não podem ser usados com [`sizeof`](<#/doc/language/sizeof>) e [`_Alignas`](<#/doc/language/alignas>)(desde C11)(ate C23)[`alignas`](<#/doc/language/alignas>)(desde C23)(desde C11).

### Notas

Os seguintes usos de campos de bits causam _comportamento indefinido_:

*   Chamar [offsetof](<#/doc/types/offsetof>) em um campo de bits.

As seguintes propriedades de campos de bits são _não especificadas_:

*   Alinhamento da unidade de alocação que contém um campo de bits.

As seguintes propriedades de campos de bits são _definidas pela implementação_:

*   Se campos de bits do tipo `int` são tratados como com sinal ou sem sinal.
*   Se tipos diferentes de `int`, `signed int`, `unsigned int`, `_Bool`(desde C99), e (possivelmente `unsigned`) `_BitInt(N)`(desde C23) são permitidos.
*   Se tipos `atomic` são permitidos.

| (desde C11)
*   Se um campo de bits pode atravessar um limite de unidade de alocação.
*   A ordem dos campos de bits dentro de uma unidade de alocação (em algumas plataformas, os campos de bits são empacotados da esquerda para a direita, em outras da direita para a esquerda).

Embora o número de bits na representação de objeto de `_Bool` seja pelo menos [CHAR_BIT](<#/doc/types/limits>), a largura do campo de bits do tipo `_Bool` não pode ser maior que 1. | (desde C99)

Na linguagem de programação C++, a largura de um campo de bits pode exceder a largura do tipo subjacente (mas os bits extras são bits de preenchimento), e campos de bits do tipo `int` são sempre com sinal.

### Referências

*   Padrão C23 (ISO/IEC 9899:2024):

    *   6.7.2.1 Especificadores de estrutura e união
*   Padrão C17 (ISO/IEC 9899:2018):

    *   6.7.2.1 Especificadores de estrutura e união
*   Padrão C11 (ISO/IEC 9899:2011):

    *   6.7.2.1 Especificadores de estrutura e união
*   Padrão C99 (ISO/IEC 9899:1999):

    *   6.7.2.1 Especificadores de estrutura e união
*   Padrão C89/C90 (ISO/IEC 9899:1990):

    *   3.5.2.1 Especificadores de estrutura e união

### Veja também

[Documentação C++](<#/>) para Campo de bits
---