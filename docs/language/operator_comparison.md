# Operadores de Comparação

Operadores de comparação são operadores binários que testam uma condição e retornam **1** se essa condição for logicamente **verdadeira** e **0** se essa condição for **falsa**.

Operador | Nome do Operador | Exemplo | Descrição
== | igual a | a == b | **a** é igual a **b**
!= | diferente de | a != b | **a** não é igual a **b**
< | menor que | a < b | **a** é menor que **b**
> | maior que | a > b | **a** é maior que **b**
<= | menor ou igual a | a <= b | **a** é menor ou igual a **b**
>= | maior ou igual a | a >= b | **a** é maior ou igual a **b**

### Operadores Relacionais

As expressões de operadores relacionais têm a forma

---
lhs `<` rhs | (1) |
lhs `>` rhs | (2) |
lhs `< =` rhs | (3) |
lhs `> =` rhs | (4) |

1) expressão de menor que

2) expressão de maior que

3) expressão de menor ou igual

4) expressão de maior ou igual

onde

- **lhs, rhs** — expressões que ambas têm tipo real ou ambas têm tipo ponteiro para objeto

O tipo de qualquer expressão de operador relacional é int, e seu valor (que não é um lvalue) é 1 quando a relação especificada é verdadeira e 0 quando a relação especificada não é verdadeira.

Se lhs e rhs são expressões de qualquer [tipo real](<#/doc/language/types>), então

*   [conversões aritméticas usuais](<#/doc/language/conversion>) são realizadas
*   os valores dos operandos após a conversão são comparados no sentido matemático usual (exceto que zeros positivos e negativos são comparados como iguais e qualquer comparação envolvendo um valor NaN retorna zero)

Note que números complexos e imaginários não podem ser comparados com esses operadores.

Se lhs e rhs são expressões de tipo ponteiro, eles devem ser ambos ponteiros para objetos de [tipos compatíveis](<#/doc/language/types>), exceto que as qualificações dos objetos apontados são ignoradas.

*   um ponteiro para um objeto que não é um elemento de um array é tratado como se estivesse apontando para um elemento de um array com um único elemento
*   se dois ponteiros apontam para o mesmo objeto, ou ambos apontam para uma posição após o final do mesmo array, eles são comparados como iguais
*   se dois ponteiros apontam para elementos diferentes do mesmo array, aquele que aponta para o elemento com o índice maior é comparado como maior.
*   se um ponteiro aponta para o elemento de um array e o outro ponteiro aponta para uma posição após o final do mesmo array, o ponteiro "uma-posição-após-o-final" é comparado como maior
*   se os dois ponteiros apontam para membros da mesma [struct](<#/doc/language/struct>), o ponteiro para o membro declarado posteriormente na definição da struct é comparado como maior do que o ponteiro para o membro declarado anteriormente.
*   ponteiros para membros da mesma union são comparados como iguais
*   todas as outras comparações de ponteiros invocam comportamento indefinido

Execute este código
```c
    #include <assert.h>
    int main(void)
    {
        assert(1 < 2);
        assert(2+2 <= 4.0); // int converts to double, two 4.0's compare equal
    
        struct { int x,y; } s;
        assert(&s.x < &s.y); // struct members compare in order of declaration
    
        double d = 0.0/0.0; // NaN
        assert( !(d < d) );
        assert( !(d > d) );
        assert( !(d <= d) );
        assert( !(d >= d) );
        assert( !(d == d) );
    
        float f = 0.1; // f = 0.100000001490116119384765625
        double g = 0.1; // g = 0.1000000000000000055511151231257827021181583404541015625
        assert(f > g); // different values
    }
```

### Operadores de Igualdade

As expressões de operadores de igualdade têm a forma

---
lhs `==` rhs | (1) |
lhs `!=` rhs | (2) |

1) expressão de igual a

2) expressão de diferente de

onde

- **lhs, rhs** — expressões que
*   ambas têm qualquer [tipo aritmético](<#/doc/language/arithmetic_types>) (incluindo complexos e imaginários)

|
*   ambas têm tipo [nullptr_t](<#/doc/types/nullptr_t>)
*   uma tem tipo [nullptr_t](<#/doc/types/nullptr_t>) e a outra é uma constante de ponteiro nulo

| (desde C23)
*   ambos são ponteiros para objetos ou funções de tipos [compatíveis](<#/doc/language/types>), ignorando qualificadores dos tipos apontados
*   um é um ponteiro para objeto e o outro é um ponteiro para void (possivelmente qualificado)
*   um é um ponteiro para objeto ou função e o outro é uma constante de ponteiro nulo como [NULL](<#/doc/types/NULL>) ou nullptr (desde C23)

O tipo de qualquer expressão de operador de igualdade é int, e seu valor (que não é um lvalue) é 1 quando a relação especificada é verdadeira e 0 quando a relação especificada não é verdadeira.

*   se ambos os operandos têm tipos aritméticos, [conversões aritméticas usuais](<#/doc/language/conversion>) são realizadas e os valores resultantes são comparados no sentido matemático usual (exceto que zeros positivos e negativos são comparados como iguais e qualquer comparação envolvendo um valor NaN, incluindo a igualdade consigo mesmo, retorna zero). Em particular, valores de tipo complexo são iguais se suas partes reais são comparadas como iguais e suas partes imaginárias são comparadas como iguais.

*   dois valores [nullptr_t](<#/doc/types/nullptr_t>) ou um valor [nullptr_t](<#/doc/types/nullptr_t>) e uma constante de ponteiro nulo são comparados como iguais

| (desde C23)
*   se um operando é um ponteiro e o outro é uma constante de ponteiro nulo, a constante de ponteiro nulo é primeiro [convertida](<#/doc/language/conversion>) para o tipo do ponteiro (o que resulta em um valor de ponteiro nulo), e os dois ponteiros são comparados conforme descrito abaixo
*   se um operando é um ponteiro e o outro é um ponteiro para void, o ponteiro não-void é [convertido](<#/doc/language/conversion>) para o ponteiro para void e os dois ponteiros são comparados conforme descrito abaixo
*   dois ponteiros são comparados como iguais se qualquer uma das seguintes condições for verdadeira:

    *   ambos são valores de ponteiro nulo de seu tipo
    *   ambos são ponteiros para o mesmo objeto ou função
    *   um ponteiro é para um objeto struct/union/array e o outro é para seu primeiro membro/qualquer membro/primeiro elemento
    *   ambos apontam para uma posição após o último elemento do mesmo array
    *   um está uma posição após o final de um array, e o outro está no início de um array diferente (do mesmo tipo) que segue o primeiro em um array maior ou em uma struct sem preenchimento (padding)

(assim como com operadores relacionais, ponteiros para objetos que não são elementos de nenhum array se comportam como ponteiros para elementos de arrays de tamanho 1)

#### Notas

Objetos do tipo struct não são comparados como iguais automaticamente, e compará-los com [memcmp](<#/doc/string/byte/memcmp>) não é confiável porque os bytes de preenchimento (padding) podem ter quaisquer valores.

Como a comparação de ponteiros funciona com ponteiros para void, a macro [NULL](<#/doc/types/NULL>) pode ser definida como (void*)0 em C, embora isso seria inválido em C++ onde ponteiros void não se convertem implicitamente para ponteiros tipados.

Deve-se ter cuidado ao comparar valores de ponto flutuante para igualdade, porque os resultados de muitas operações não podem ser representados exatamente e devem ser arredondados. Na prática, números de ponto flutuante são geralmente comparados permitindo a diferença de uma ou mais unidades do último lugar.

Execute este código
```c
    #include <assert.h>
    int main(void)
    {
        assert(2+2 == 4.0); // int converts to double, two 4.0's compare equal
    
        int n[2][3] = {1,2,3,4,5,6};
        int* p1 = &n[0][2]; // last element in the first row
        int* p2 = &n[1][0]; // start of second row
        assert(p1+1 == p2); // compare equal
    
        double d = 0.0/0.0; // NaN
        assert( d != d ); // NaN does not equal itself
    
        float f = 0.1; // f = 0.100000001490116119384765625
        double g = 0.1; // g = 0.1000000000000000055511151231257827021181583404541015625
        assert(f != g); // different values
    }
```

### Referências

*   Padrão C17 (ISO/IEC 9899:2018):

    *   6.5.8 Operadores Relacionais (p: 68-69)

    *   6.5.9 Operadores de Igualdade (p: 69-70)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   6.5.8 Operadores Relacionais (p: 95-96)

    *   6.5.9 Operadores de Igualdade (p: 96-97)

*   Padrão C99 (ISO/IEC 9899:1999):

    *   6.5.8 Operadores Relacionais (p: 85-86)

    *   6.5.9 Operadores de Igualdade (p: 86-87)

*   Padrão C89/C90 (ISO/IEC 9899:1990):

    *   3.3.8 Operadores Relacionais

    *   3.3.9 Operadores de Igualdade

### Veja também

[ Precedência de operadores](<#/doc/language/operator_precedence>)

Operadores comuns
---
[atribuição](<#/doc/language/operator_assignment>) | [incremento
decremento](<#/doc/language/operator_incdec>) | [aritméticos](<#/doc/language/operator_arithmetic>) | [lógicos](<#/doc/language/operator_logical>) | **comparação** | [acesso a membro](<#/doc/language/operator_member_access>) | [outros](<#/doc/language/operator_other>)
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
(até C23)

alignof
(desde C23)
[documentação C++](<#/>) para Operadores de comparação
---