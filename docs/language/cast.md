# operador de cast

Realiza conversão de tipo explícita

### Sintaxe

---
`(` type-name `)` expression
---

onde

- **type-name** — o tipo void ou qualquer [tipo escalar](<#/doc/language/compatible_type>)
- **expression** — qualquer [expressão](<#/doc/language/expressions>) de [tipo escalar](<#/doc/language/compatible_type>) (a menos que type-name seja void, caso em que pode ser qualquer coisa)

### Explicação

Se type-name for void, então expression é avaliada por seus efeitos colaterais e seu valor de retorno é descartado, assim como quando expression é usada por si só, como uma [declaração de expressão](<#/doc/language/statements>).

Caso contrário, se type-name for exatamente o tipo de expression, nada é feito (exceto se expression tiver um tipo de ponto flutuante e for representada com maior alcance e precisão do que seu tipo indica -- veja abaixo)

Caso contrário, o valor de expression é convertido para o tipo nomeado por type-name, da seguinte forma:

Toda [conversão implícita como se por atribuição](<#/doc/language/conversion>) é permitida.

Além das conversões implícitas, as seguintes conversões são permitidas:

*   Qualquer inteiro pode ser convertido (cast) para qualquer tipo de ponteiro. Exceto para as constantes de ponteiro nulo como [NULL](<#/doc/types/NULL>) (que [não precisa de um cast](<#/doc/language/conversion>)), o resultado é definido pela implementação, pode não estar corretamente alinhado, pode não apontar para um objeto do tipo referenciado e pode ser uma [representação de armadilha](<#/doc/language/object>).
*   Qualquer tipo de ponteiro pode ser convertido (cast) para qualquer tipo inteiro. O resultado é definido pela implementação, mesmo para valores de ponteiro nulo (eles não resultam necessariamente no valor zero). Se o resultado não puder ser representado no tipo de destino, o comportamento é indefinido (inteiros sem sinal não implementam aritmética modular em um cast de ponteiro)
*   Qualquer ponteiro para objeto pode ser convertido (cast) para qualquer outro ponteiro para objeto. Se o valor não estiver corretamente alinhado para o tipo de destino, o comportamento é indefinido. Caso contrário, se o valor for convertido de volta para o tipo original, ele se compara como igual ao valor original. Se um ponteiro para objeto for convertido (cast) para um ponteiro para qualquer tipo de caractere, o resultado aponta para o byte mais baixo do objeto e pode ser incrementado até o sizeof do tipo de destino (em outras palavras, pode ser usado para examinar a [representação do objeto](<#/doc/language/object>) ou para fazer uma cópia via [memcpy](<#/doc/string/byte/memcpy>) ou [memmove](<#/doc/string/byte/memmove>)).
*   Qualquer ponteiro para função pode ser convertido (cast) para um ponteiro para qualquer outro tipo de função. Se o ponteiro resultante for convertido de volta para o tipo original, ele se compara como igual ao valor original. Se o ponteiro convertido for usado para fazer uma chamada de função, o comportamento é indefinido (a menos que os tipos de função sejam [compatíveis](<#/doc/language/compatible_type>))
*   Ao fazer cast entre ponteiros (seja de objeto ou função), se o valor original for um valor de ponteiro nulo de seu tipo, o resultado é o valor de ponteiro nulo correto para o tipo de destino.

Em qualquer caso (tanto ao executar uma conversão implícita quanto no cast do mesmo tipo), se expression e type-name forem tipos de ponto flutuante e expression for representada com maior alcance e precisão do que seu tipo indica (veja [FLT_EVAL_METHOD](<#/doc/types/limits/FLT_EVAL_METHOD>)), o alcance e a precisão são removidos para corresponder ao tipo de destino.

A [categoria de valor](<#/doc/language/value_category>) da expressão de cast é sempre não-lvalue.

### Notas

Como os qualificadores [\`const\`](<#/doc/language/const>), [\`volatile\`](<#/doc/language/volatile>), [\`restrict\`](<#/doc/language/restrict>) e [\`_Atomic\`](<#/doc/language/atomic>) afetam apenas [lvalues](<#/doc/language/value_category>), um cast para um tipo cvr-qualificado ou atômico é exatamente equivalente ao cast para o tipo não qualificado correspondente.

O cast para void é às vezes útil para silenciar avisos do compilador sobre resultados não utilizados.

As conversões não listadas aqui não são permitidas. Em particular,

*   não há conversões entre ponteiros e tipos de ponto flutuante
*   não há conversões entre ponteiros para funções e ponteiros para objetos (incluindo void*)

Se a implementação fornecer [intptr_t](<#/doc/types/integer>) e/ou [uintptr_t](<#/doc/types/integer>), então um cast de um ponteiro para um tipo de objeto (incluindo _cv_ void) para esses tipos é sempre bem definido. No entanto, isso não é garantido para um ponteiro de função. | (desde C99)

Note que as conversões entre ponteiros de função e ponteiros de objeto são aceitas como extensões por muitos compiladores, e esperadas por alguns usos da [função \`dlsym()\` do POSIX](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/dlsym.html>).

### Exemplo

Execute este código
```c
    #include <stdio.h>
    
    int main(void)
    {
        // examining object representation is a legitimate use of cast
        double d = 3.14;
        printf("The double %.2f (%a) is: ", d, d);
        for (size_t n = 0; n < sizeof d; ++n)
            printf("0x%02x ", ((unsigned char*)&d)[n]);
    
        // edge cases
        struct S { int x; } s;
    //    (struct S)s; // error; not a scalar type
                       // even though casting to the same type does nothing
        (void)s; // okay to cast any type to void
    }
```

Saída possível:
```
    The double 3.14 (0x1.91eb851eb851fp+1) is: 0x1f 0x85 0xeb 0x51 0xb8 0x1e 0x09 0x40
```

### Referências

*   Padrão C23 (ISO/IEC 9899:2024):

    *   6.5.4 Operadores de cast (p: TBD)

*   Padrão C17 (ISO/IEC 9899:2018):

    *   6.5.4 Operadores de cast (p: 65-66)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   6.5.4 Operadores de cast (p: 91)

*   Padrão C99 (ISO/IEC 9899:1999):

    *   6.5.4 Operadores de cast (p: 81)

*   Padrão C89/C90 (ISO/IEC 9899:1990):

    *   3.3.4 Operadores de cast

### Veja também

[Documentação C++](<#/>) para conversão de tipo explícita
---