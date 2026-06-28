# Operadores Lógicos

Operadores lógicos aplicam operações padrão de álgebra booleana aos seus operandos.

Operador | Nome do Operador | Exemplo | Resultado
! | NOT lógico | !a | a negação lógica de **a**
&& | AND lógico | a && b | o AND lógico de **a** e **b**
|| | OR lógico | a || b | o OR lógico de **a** e **b**

### NOT Lógico

A expressão NOT lógico tem a forma

---
`!` expression

onde

- **expression** — uma expressão de qualquer [tipo escalar](<#/doc/language/compatible_type>)

O operador NOT lógico tem o tipo int. Seu valor é 0 se a expressão for avaliada para um valor que se compara diferente de zero. Seu valor é 1 se a expressão for avaliada para um valor que se compara igual a zero. (assim !E é o mesmo que (0==E))

Execute este código
```c
    #include <stdbool.h>
    #include <stdio.h>
    #include <ctype.h>
    int main(void)
    {
        bool b = !(2+2 == 4); // não é verdadeiro
        printf("!(2+2==4) = %s\n", b ? "true" : "false");
    
        int n = isspace('a'); // diferente de zero se 'a' for um espaço, zero caso contrário
        int x = !!n; // "bang-bang", um idioma comum em C para mapear inteiros para [0,1]
                     // (todos os valores diferentes de zero se tornam 1)
        char *a[2] = {"non-space", "space"};
        puts(a[x]); // agora x pode ser usado com segurança como um índice para um array de 2 strings
    }
```

Saída:
```
    !(2+2==4) = false
    non-space
```

### AND Lógico

A expressão AND lógico tem a forma

---
lhs `& &` rhs

onde

- **lhs** — uma expressão de qualquer tipo escalar
- **rhs** — uma expressão de qualquer tipo escalar, que é avaliada apenas se lhs não se comparar igual a 0

O operador AND lógico tem o tipo int e o valor 1 se ambos lhs e rhs se compararem diferentes de zero. Ele tem o valor 0 caso contrário (se lhs ou rhs ou ambos se compararem iguais a zero).

Existe um [ponto de sequência](<#/doc/language/eval_order>) após a avaliação de lhs. Se o resultado de lhs se comparar igual a zero, então rhs não é avaliado de forma alguma (a chamada _avaliação de curto-circuito_)

Execute este código
```c
    #include <stdbool.h>
    #include <stdio.h>
    int main(void)
    {
        bool b = 2+2==4 && 2*2==4; // b == verdadeiro
    
        1 > 2 && puts("this won't print");
    
        char *p = "abc";
        if(p && *p) // idioma comum em C: se p não for nulo
                    // E se p não apontar para o final da string
        {           // (note que, graças à avaliação de curto-circuito, isso
                    //  não tentará desreferenciar um ponteiro nulo)
        // ...      // ... então faça algum processamento de string
        }
    }
```

### OR Lógico

A expressão OR lógico tem a forma

---
lhs `||` rhs

onde

- **lhs** — uma expressão de qualquer tipo escalar
- **rhs** — uma expressão de qualquer tipo escalar, que é avaliada apenas se lhs se comparar igual a 0

O operador OR lógico tem o tipo int e o valor 1 se lhs ou rhs se compararem diferentes de zero. Ele tem o valor 0 caso contrário (se ambos lhs e rhs se compararem iguais a zero).

Existe um [ponto de sequência](<#/doc/language/eval_order>) após a avaliação de lhs. Se o resultado de lhs se comparar diferente de zero, então rhs não é avaliado de forma alguma (a chamada _avaliação de curto-circuito_)

Execute este código
```c
    #include <stdbool.h>
    #include <stdio.h>
    #include <string.h>
    #include <errno.h>
    int main(void)
    {
        bool b = 2+2 == 4 || 2+2 == 5; // verdadeiro
        printf("true or false = %s\n", b ? "true" : "false");
    
        // OR lógico pode ser usado de forma semelhante ao "or die" do Perl, desde que rhs tenha tipo escalar
        fopen("test.txt", "r") || printf("could not open test.txt: %s\n", strerror(errno));
    }
```

Saída possível:
```
    true or false = true
    could not open test.txt: No such file or directory
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 6.5.3.3 Operadores aritméticos unários (p: 89)

    

  * 6.5.13 Operador AND lógico (p: 99)

    

  * 6.5.14 Operador OR lógico (p: 99)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 6.5.3.3 Operadores aritméticos unários (p: 79)

    

  * 6.5.13 Operador AND lógico (p: 89)

    

  * 6.5.14 Operador OR lógico (p: 89)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 3.3.3.3 Operadores aritméticos unários

    

  * 3.3.13 Operador AND lógico

    

  * 3.3.14 Operador OR lógico

### Veja Também

[ Precedência de operadores](<#/doc/language/operator_precedence>)

Operadores comuns
---
[atribuição](<#/doc/language/operator_assignment>) | [incremento
decremento](<#/doc/language/operator_incdec>) | [aritméticos](<#/doc/language/operator_arithmetic>) | **lógicos** | [comparação](<#/doc/language/operator_comparison>) | [acesso a membro](<#/doc/language/operator_member_access>) | [outros](<#/doc/language/operator_other>)
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

### Veja também

[Documentação C++](<#/>) para Operadores lógicos
---