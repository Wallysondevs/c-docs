# Operadores de atribuição

Operadores de atribuição e de atribuição composta são operadores binários que modificam a variável à sua esquerda usando o valor à sua direita.

Operador | Nome do Operador | Exemplo | Descrição | Equivalente a
= | atribuição básica | a = b | **a** torna-se igual a **b** | N/A
+= | atribuição de adição | a += b | **a** torna-se igual à soma de **a** e **b** | a = a + b
-= | atribuição de subtração | a -= b | **a** torna-se igual à subtração de **b** de **a** | a = a - b
*= | atribuição de multiplicação | a *= b | **a** torna-se igual ao produto de **a** e **b** | a = a * b
/= | atribuição de divisão | a /= b | **a** torna-se igual à divisão de **a** por **b** | a = a / b
%= | atribuição de módulo | a %= b | **a** torna-se igual ao resto de **a** dividido por **b** | a = a % b
&= | atribuição AND bit a bit | a &= b | **a** torna-se igual ao AND bit a bit de **a** e **b** | a = a & b
|= | atribuição OR bit a bit | a |= b | **a** torna-se igual ao OR bit a bit de **a** e **b** | a = a | b
^= | atribuição XOR bit a bit | a ^= b | **a** torna-se igual ao XOR bit a bit de **a** e **b** | a = a ^ b
<<= | atribuição de deslocamento à esquerda bit a bit | a <<= b | **a** torna-se igual a **a** deslocado à esquerda por **b** | a = a << b
>>= | atribuição de deslocamento à direita bit a bit | a >>= b | **a** torna-se igual a **a** deslocado à direita por **b** | a = a >> b

### Atribuição Simples

As expressões do operador de atribuição simples têm a forma

---
lhs `=` rhs
---

onde

- **lhs** — expressão [lvalue modificável](<#/doc/language/value_category>) de qualquer tipo de objeto completo
- **rhs** — expressão de qualquer tipo [implicitamente conversível](<#/doc/language/conversion>) para lhs ou [compatível](<#/doc/language/compatible_type>) com lhs

A atribuição realiza uma [conversão implícita](<#/doc/language/conversion>) do valor de rhs para o tipo de lhs e então substitui o valor no objeto designado por lhs pelo valor convertido de rhs.

A atribuição também retorna o mesmo valor que foi armazenado em `lhs` (para que expressões como a = b = c sejam possíveis). A [categoria de valor](<#/doc/language/value_category>) do operador de atribuição é não-lvalue (para que expressões como (a=b)=c sejam inválidas).

rhs e lhs devem satisfazer uma das seguintes condições:

  * ambos lhs e rhs têm tipo [struct](<#/doc/language/struct>) ou [union](<#/doc/language/union>) [compatível](<#/doc/language/compatible_type>), ou..
  * rhs deve ser [implicitamente conversível](<#/doc/language/conversion>) para lhs, o que implica

    

  * ambos lhs e rhs têm [tipos aritméticos](<#/doc/language/arithmetic_types>), caso em que lhs pode ser qualificado como [volatile](<#/doc/language/volatile>) ou [atomic](<#/doc/language/atomic>) (desde C11)
  * ambos lhs e rhs têm [ponteiro](<#/doc/language/pointer>) para tipos [compatíveis](<#/doc/language/compatible_type>) (ignorando qualificadores), ou um dos ponteiros é um ponteiro para void, e a [conversão](<#/doc/language/conversion>) não adicionaria qualificadores ao tipo apontado. lhs pode ser qualificado como [volatile](<#/doc/language/volatile>) ou [restrict](<#/doc/language/restrict>) (desde C99) ou [atomic](<#/doc/language/atomic>) (desde C11).
  * lhs é um ponteiro (possivelmente qualificado ou [atomic](<#/doc/language/atomic>) (desde C11)) e rhs é uma constante de ponteiro nulo como [NULL](<#/doc/types/NULL>) ou um valor [nullptr_t](<#/doc/types/nullptr_t>) (desde C23)

    

  * lhs tem tipo `_Bool` (possivelmente qualificado ou [atomic](<#/doc/language/atomic>) (desde C11)) e rhs é um ponteiro ou um valor [nullptr_t](<#/doc/types/nullptr_t>) (desde C23)

| (desde C99)
  
    

  * lhs tem tipo [nullptr_t](<#/doc/types/nullptr_t>) (possivelmente qualificado ou atomic) e rhs tem tipo [nullptr_t](<#/doc/types/nullptr_t>)

| (desde C23)
  
#### Notas

Se rhs e lhs se sobrepõem na memória (por exemplo, são membros da mesma union), o comportamento é indefinido, a menos que a sobreposição seja exata e os tipos sejam [compatíveis](<#/doc/language/compatible_type>).

Embora arrays não sejam atribuíveis, um array encapsulado em uma struct é atribuível a outro objeto do mesmo tipo de struct (ou compatível).

O efeito colateral de atualizar lhs é [sequenciado após](<#/doc/language/eval_order>) os cálculos de valor, mas não os efeitos colaterais de lhs e rhs em si, e as avaliações dos operandos são, como de costume, não sequenciadas em relação um ao outro (portanto, expressões como `i=++i;` são indefinidas).

A atribuição remove o alcance e a precisão extras de expressões de ponto flutuante (veja [FLT_EVAL_METHOD](<#/doc/types/limits/FLT_EVAL_METHOD>)).

Em C++, operadores de atribuição são expressões lvalue, o que não ocorre em C.

Execute este código
```c
    #include <stdio.h>
    
    int main(void)
    {
        // inteiros
        int i = 1, j = 2, k = 3; // inicialização, não atribuição
    
        i = j = k;   // os valores de i e j agora são 3
    //  (i = j) = k; // Erro: lvalue requerido
        printf("%d %d %d\n", i, j, k);
    
        // ponteiros
        const char c = 'A'; // inicialização; não atribuição
        const char *p = &c;  // inicialização; não atribuição
        const char **cpp = &p; // inicialização; não atribuição
    
    //  cpp = &p;   // Erro: char** não é conversível para const char**
        *cpp = &c;  // OK, char* é conversível para const char*
        printf("%c \n", **cpp);
        cpp = 0;    // OK, constante de ponteiro nulo é conversível para qualquer ponteiro
    
        // arrays
        int arr1[2] = {1,2}, arr2[2] = {3, 4};
    //  arr1 = arr2; // Erro: não é possível atribuir a um array
        printf("arr1[0]=%d arr1[1]=%d arr2[0]=%d arr2[1]=%d\n",
                arr1[0],   arr1[1],   arr2[0],   arr2[1]);
    
        struct { int arr[2]; } sam1 = { {5, 6} }, sam2 = { {7, 8} };
        sam1 = sam2; // OK: é possível atribuir arrays encapsulados em structs
    
        printf("%d %d \n", sam1.arr[0], sam1.arr[1]);
    }
```

Saída:
```
    3 3 3
    A
    arr1[0]=1 arr1[1]=2 arr2[0]=3 arr2[1]=4
    7 8
```

### Atribuição Composta

As expressões do operador de atribuição composta têm a forma

---
lhs op rhs
---

onde

- **op** — um de `*=`, `/=`, `%=`, `+=`, `-=`, `<<=`, `>>=`, `&=`, `^=`, `|=`
- **lhs, rhs** — expressões com [tipos aritméticos](<#/doc/language/arithmetic_types>) (onde lhs pode ser qualificado ou atomic), exceto quando op é `+=` ou `-=`, que também aceitam tipos de ponteiro com as mesmas restrições que `+` e `-`

A expressão `lhs @= rhs` é exatamente a mesma que `lhs = lhs @ (rhs)`, exceto que lhs é avaliado apenas uma vez.

Se lhs tiver tipo [atomic](<#/doc/language/atomic>), a operação se comporta como uma única operação atômica de leitura-modificação-escrita com ordem de memória [memory_order_seq_cst](<#/doc/atomic/memory_order>). Para tipos atômicos inteiros, a atribuição composta `@=` é equivalente a:
```c
    T1* addr = &lhs;
    T2 val = rhs;
    T1 old = *addr;
    T1 new;
    do { new = old @ val } while (!atomic_compare_exchange_strong(addr, &old, new);
```

| (desde C11)
  
Execute este código
```c
    #include <stdio.h>
    
    int main(void)
    {
        int x = 10; 
        int hundred = 100; 
        int ten = 10; 
        int fifty = 50; 
    
        printf("%d %d %d %d\n", x, hundred, ten, fifty);
    
        hundred *= x; 
        ten     /= x; 
        fifty   %= x; 
    
        printf("%d %d %d %d\n", x, hundred, ten, fifty);
    
        return 0;
    }
```

Saída:
```
    10 100 10 50
    10 1000 1 0
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 6.5.16 Operadores de atribuição (p: 72-73)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 6.5.16 Operadores de atribuição (p: 101-104)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 6.5.16 Operadores de atribuição (p: 91-93)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 3.3.16 Operadores de atribuição

### Veja Também

[Precedência de operadores](<#/doc/language/operator_precedence>)

Operadores comuns
---
**atribuição** | [incremento
decremento](<#/doc/language/operator_incdec>) | [aritméticos](<#/doc/language/operator_arithmetic>) | [lógicos](<#/doc/language/operator_logical>) | [comparação](<#/doc/language/operator_comparison>) | [acesso a membro](<#/doc/language/operator_member_access>) | [outros](<#/doc/language/operator_other>)
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

[Documentação C++](<#/>) para Operadores de atribuição
---