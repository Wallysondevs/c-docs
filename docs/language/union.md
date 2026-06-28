# Declaração de união

Uma união é um tipo que consiste em uma sequência de membros cujo armazenamento se sobrepõe (em contraste com a struct, que é um tipo que consiste em uma sequência de membros cujo armazenamento é alocado em uma sequência ordenada). O valor de no máximo um dos membros pode ser armazenado em uma união a qualquer momento.

O [especificador de tipo](<#/doc/language/declarations>) para uma união é idêntico ao especificador de tipo de [`struct`](<#/doc/language/struct>), exceto pela palavra-chave utilizada:

### Sintaxe

---
`union` attr-spec-seq ﻿(optional) name ﻿(optional) `{` struct-declaration-list `}` | (1) |
`union` attr-spec-seq ﻿(optional) name | (2) |
- **name** — o nome da união que está sendo definida
- **struct-declaration-list** — qualquer número de declarações de variáveis, declarações de [campos de bits](<#/doc/language/bit_field>) e declarações de static assert. Membros de tipo incompleto e membros de tipo de função não são permitidos.
- **attr-spec-seq** — (C23)lista opcional de [atributos](<#/doc/language/attributes>), aplicados ao tipo de união, não permitido para (2) se tal forma não for seguida por um `;` (ou seja, não é uma declaração antecipada).

### Explicação

A união é tão grande quanto o necessário para armazenar seu maior membro (preenchimento adicional não nomeado no final também pode ser adicionado). Os outros membros são alocados nos mesmos bytes como parte desse maior membro.

Um ponteiro para uma união pode ser convertido para um ponteiro para cada um de seus membros (se uma união tiver membros de campo de bits, o ponteiro para uma união pode ser convertido para o ponteiro para o tipo subjacente do campo de bits). Da mesma forma, um ponteiro para qualquer membro de uma união pode ser convertido para um ponteiro para a união que o contém.

Se o membro usado para acessar o conteúdo de uma união não for o mesmo que o membro usado pela última vez para armazenar um valor, a representação do objeto do valor que foi armazenado é reinterpretada como uma representação do objeto do novo tipo (isso é conhecido como _type punning_). Se o tamanho do novo tipo for maior que o tamanho do tipo gravado por último, o conteúdo dos bytes em excesso é não especificado (e pode ser uma representação de armadilha). Antes do C99 TC3 (DR 283), esse comportamento era indefinido, mas comumente implementado dessa forma. | (desde C99)
Semelhante à struct, um membro não nomeado de uma união cujo tipo é uma união sem nome é conhecido como _união anônima_. Cada membro de uma união anônima é considerado um membro da struct ou união que o contém, mantendo seu layout de união. Isso se aplica recursivamente se a struct ou união que o contém também for anônima.
```
    struct v
    {
       union // anonymous union
       {
           struct { int i, j; }; // anonymous structure
           struct { long k, l; } w;
       };
       int m;
    } v1;
    
    v1.i = 2;   // valid
    v1.k = 3;   // invalid: inner structure is not anonymous
    v1.w.k = 5; // valid
```

Semelhante à struct, o comportamento do programa é indefinido se a união for definida sem nenhum membro nomeado (incluindo aqueles obtidos através de structs ou uniões aninhadas anônimas). | (desde C11)

### Palavras-chave

[`union`](<#/doc/keyword/union>)

### Notas

Consulte [inicialização de struct](<#/doc/language/struct_initialization>) para as regras sobre inicialização de structs e uniões.

### Exemplo

Execute este código
```
    #include <assert.h>
    #include <stdint.h>
    #include <stdio.h>
    
    int main(void)
    {
        union S
        {
            uint32_t u32;
            uint16_t u16[2];
            uint8_t  u8;
        } s = {0x12345678}; // s.u32 is now the active member
        printf("Union S has size %zu and holds %x\n", sizeof s, s.u32);
        s.u16[0] = 0x0011;  // s.u16 is now the active member
        // reading from s.u32 or from s.u8 reinterprets the object representation
    //  printf("s.u8 is now %x\n", s.u8); // unspecified, typically 11 or 00
    //  printf("s.u32 is now %x\n", s.u32); // unspecified, typically 12340011 or 00115678
    
        // pointers to all members of a union compare equal to themselves and the union
        assert((uint8_t*)&s == &s.u8);
    
        // this union has 3 bytes of trailing padding
        union pad
        {
            char  c[5]; // occupies 5 bytes
            float f;    // occupies 4 bytes, imposes alignment 4
        } p = { .f = 1.23 }; // the size is 8 to satisfy float's alignment
        printf("size of union of char[5] and float is %zu\n", sizeof p);
    }
```

Saída possível:
```
    Union S has size 4 and holds 12345678
    size of union of char[5] and float is 8
```

### Relatórios de defeitos

Os seguintes relatórios de defeitos que alteram o comportamento foram aplicados retroativamente a padrões C publicados anteriormente.

DR | Aplicado a | Comportamento conforme publicado | Comportamento correto
[DR 499](<https://www.open-std.org/jtc1/sc22/wg14/www/docs/n2396.htm#dr_499>) | C11 | membros de structs/uniões anônimas eram considerados membros da struct/união que os continha | eles retêm seu layout de memória

### Referências

  * C23 standard (ISO/IEC 9899:2024):

    

  * 6.7.2.1 Structure and union specifiers (p: TBD)

  * C17 standard (ISO/IEC 9899:2018):

    

  * 6.7.2.1 Structure and union specifiers (p: 81-84)

  * C11 standard (ISO/IEC 9899:2011):

    

  * 6.7.2.1 Structure and union specifiers (p: 112-117)

  * C99 standard (ISO/IEC 9899:1999):

    

  * 6.7.2.1 Structure and union specifiers (p: 101-104)

  * C89/C90 standard (ISO/IEC 9899:1990):

    

  * 3.5.2.1 Structure and union specifiers

### Veja também

[documentação C++](<#/>) para Declaração de união
---