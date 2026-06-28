# Operadores de incremento/decremento

Operadores de incremento/decremento são operadores unários que incrementam/decrementam o valor de uma variável em 1.

Eles podem ter a forma pós-fixada:

---
expr `++`
expr `--`

Assim como a forma pré-fixada:

---
`++` expr
`--` expr

O operando expr de ambos os operadores de incremento ou decremento pré-fixados e pós-fixados deve ser um [lvalue modificável](<#/doc/language/value_category>) de [tipo inteiro](<#/doc/language/compatible_type>) (incluindo `_Bool` e enums), tipo de ponto flutuante real, ou um tipo ponteiro. Ele pode ser cvr-qualificado, não qualificado, ou [atômico](<#/doc/language/atomic>).

O resultado dos operadores de incremento e decremento pós-fixados é o valor de expr.

O resultado do operador de incremento pré-fixado é o resultado da adição do valor `1` ao valor de expr: a expressão ++e é equivalente a e += 1. O resultado do operador de decremento pré-fixado é o resultado da subtração do valor `1` do valor de expr: a expressão --e é equivalente a e -= 1.

Operadores de incremento iniciam o efeito colateral de adicionar o valor `1` do tipo apropriado ao operando. Operadores de decremento iniciam o efeito colateral de subtrair o valor `1` do tipo apropriado do operando. Assim como com quaisquer outros efeitos colaterais, essas operações são concluídas no ou antes do próximo [ponto de sequência](<#/doc/language/eval_order>).
```c
    int a = 1;
    int b = a++; // stores 1+a (which is 2) to a
                 // returns the old value of a (which is 1)
                 // After this line, b == 1 and a == 2
    a = 1;
    int c = ++a; // stores 1+a (which is 2) to a
                 // returns 1+a (which is 2)
                 // after this line, c == 2 and a == 2
```

Pós-incremento ou pós-decremento em qualquer [variável atômica](<#/doc/language/atomic>) é uma operação atômica de leitura-modificação-escrita com ordem de memória [memory_order_seq_cst](<#/doc/atomic/memory_order>). | (desde C11)

Veja [operadores aritméticos](<#/doc/language/operator_arithmetic>) para limitações na aritmética de ponteiros, bem como para conversões implícitas aplicadas aos operandos.

### Notas

Devido aos efeitos colaterais envolvidos, operadores de incremento e decremento devem ser usados com cuidado para evitar comportamento indefinido devido a violações das [regras de sequenciamento](<#/doc/language/eval_order>).

Operadores de incremento/decremento não são definidos para tipos complexos ou imaginários: a definição usual de adicionar/subtrair o número real 1 não teria efeito em tipos imaginários, e fazer com que adicionasse/subtraísse `i` para imaginários, mas `1` para números complexos, faria com que `0+yi` fosse tratado de forma diferente de `yi`.

Ao contrário de C++ (e algumas implementações de C), as expressões de incremento/decremento nunca são lvalues por si mesmas: &++a é inválido.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(void)
    {
        int a = 1;
        int b = 1;
    
        printf("original values: a == %d, b == %d\n", a, b);
        printf("result of postfix operators: a++ == %d, b-- == %d\n", a++, b--);
        printf("after postfix operators applied: a == %d, b == %d\n", a, b);
        printf("\n");
    
        // Reset a and b.
        a = 1;
        b = 1;
    
        printf("original values: a == %d, b == %d\n", a, b);
        printf("result of prefix operators: ++a == %d, --b == %d\n", ++a, --b);
        printf("after prefix operators applied: a == %d, b == %d\n", a, b);
    }
```

Saída:
```
    original values: a == 1, b == 1
    result of postfix operators: a++ == 1, b-- == 1
    after postfix operators applied: a == 2, b == 0
    
    original values: a == 1, b == 1
    result of prefix operators: ++a == 2, --b == 0
    after prefix operators applied: a == 2, b == 0
```

### Referências

  * C23 standard (ISO/IEC 9899:2024):

    

  * 6.5.2.4 Postfix increment and decrement operators (p: TBD)

    

  * 6.5.3.1 Prefix increment and decrement operators (p: TBD)

  * C17 standard (ISO/IEC 9899:2018):

    

  * 6.5.2.4 Postfix increment and decrement operators (p: TBD)

    

  * 6.5.3.1 Prefix increment and decrement operators (p: TBD)

  * C11 standard (ISO/IEC 9899:2011):

    

  * 6.5.2.4 Postfix increment and decrement operators (p: 85)

    

  * 6.5.3.1 Prefix increment and decrement operators (p: 88)

  * C99 standard (ISO/IEC 9899:1999):

    

  * 6.5.2.4 Postfix increment and decrement operators (p: 75)

    

  * 6.5.3.1 Prefix increment and decrement operators (p: 78)

  * C89/C90 standard (ISO/IEC 9899:1990):

    

  * 3.3.2.4 Postfix increment and decrement operators

    

  * 3.3.3.1 Prefix increment and decrement operators

### Veja também

[Precedência de operadores](<#/doc/language/operator_precedence>)

Operadores comuns
---
[atribuição](<#/doc/language/operator_assignment>) | **incremento
decremento** | [aritméticos](<#/doc/language/operator_arithmetic>) | [lógicos](<#/doc/language/operator_logical>) | [comparação](<#/doc/language/operator_comparison>) | [acesso a membros](<#/doc/language/operator_member_access>) | [outros](<#/doc/language/operator_other>)
a = b
a += b
a -= b
a *= b
a /= b
a %= b
a &= b
a |= b
a ^= b
a <<= b
a >>= b | ++a
--a
a++
a-- | +a
-a
a + b
a - b
a * b
a / b
a % b
~a
a & b
a | b
a ^ b
a << b
a >> b | !a
a && b
a || b | a == b
a != b
a < b
a > b
a <= b
a >= b | a[b]
*a
&a
a->b
a.b | a(...)
a, b
(type) a
a ? b : c
sizeof

_Alignof
(desde C11)
(ate C23)

alignof
(desde C23)
[Documentação C++](<#/>) para operadores de incremento/decremento
---