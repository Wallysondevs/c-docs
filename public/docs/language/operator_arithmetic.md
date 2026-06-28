# Operadores aritméticos

Operadores aritméticos aplicam operações matemáticas padrão aos seus operandos.

| Esta seção está incompleta
Motivo: considerar um sumário mais genérico para esta e outras tabelas que cobrem múltiplos tópicos
Operador | Nome do operador | Exemplo | Resultado
+ | mais unário | +a | o valor de **a** após as promoções
- | menos unário | -a | o negativo de **a**
+ | adição | a + b | a adição de **a** e **b**
- | subtração | a - b | a subtração de **b** de **a**
* | produto | a * b | o produto de **a** e **b**
/ | divisão | a / b | a divisão de **a** por **b**
% | resto | a % b | o resto de **a** dividido por **b**
~ | NOT bit a bit | ~a | o NOT bit a bit de **a**
& | AND bit a bit | a & b | o AND bit a bit de **a** e **b**
| | OR bit a bit | a | b | o OR bit a bit de **a** e **b**
^ | XOR bit a bit | a ^ b | o XOR bit a bit de **a** e **b**
<< | deslocamento à esquerda bit a bit | a << b | **a** deslocado à esquerda por **b**
>> | deslocamento à direita bit a bit | a >> b | **a** deslocado à direita por **b**

### Overflows

A aritmética de inteiros sem sinal é sempre realizada módulo 2n
onde n é o número de bits naquele inteiro específico. Por exemplo, para unsigned int, adicionar um a [UINT_MAX](<#/doc/types/limits>) resulta em ​0​, e subtrair um de ​0​ resulta em [UINT_MAX](<#/doc/types/limits>).

Quando uma operação aritmética de inteiro com sinal sofre overflow (o resultado não cabe no tipo de resultado), o comportamento é indefinido: pode "dar a volta" (wrap around) de acordo com as regras da representação (tipicamente complemento de 2), pode gerar uma armadilha (trap) em algumas plataformas ou devido a opções do compilador (por exemplo, `-ftrapv` em GCC e Clang), ou pode ser completamente [otimizado pelo compilador](<http://blog.llvm.org/2011/05/what-every-c-programmer-should-know_14.html>).

#### Ambiente de ponto flutuante

Se [` #pragma STDC FENV_ACCESS`](<#/doc/preprocessor/impl>) for definido como `ON`, todos os operadores aritméticos de ponto flutuante obedecem à [direção de arredondamento](<#/doc/numeric/fenv/FE_round>) de ponto flutuante atual e reportam erros aritméticos de ponto flutuante conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>), a menos que façam parte de um [inicializador estático](<#/doc/language/initialization>) (nesse caso, exceções de ponto flutuante não são levantadas e o modo de arredondamento é para o mais próximo).

#### Contração de ponto flutuante

A menos que [` #pragma STDC FP_CONTRACT`](<#/doc/preprocessor/impl>) seja definido como `OFF`, toda a aritmética de ponto flutuante pode ser realizada como se os resultados intermediários tivessem alcance e precisão infinitos, ou seja, otimizações que omitem erros de arredondamento e exceções de ponto flutuante que seriam observadas se a expressão fosse avaliada exatamente como escrita. Por exemplo, permite a implementação de (x*y) + z com uma única instrução de CPU de multiplicação-adição fundida ou a otimização de a = x*x*x*x; como tmp = x*x; a = tmp*tmp.

Independentemente da contração, os resultados intermediários da aritmética de ponto flutuante podem ter alcance e precisão diferentes dos indicados por seu tipo, veja [FLT_EVAL_METHOD](<#/doc/types/limits/FLT_EVAL_METHOD>).

### Aritmética unária

As expressões de operadores aritméticos unários têm a forma

---
`+` expressão | (1)
`-` expressão | (2)

1) mais unário (promoção)

2) menos unário (negação)

- **expressão** — expressão de qualquer [tipo aritmético](<#/doc/language/arithmetic_types>)

Tanto o mais unário quanto o menos unário primeiro aplicam [promoções integrais](<#/doc/language/conversion>) ao seu operando, e então

* o mais unário retorna o valor após a promoção
* o menos unário retorna o negativo do valor após a promoção (exceto que o negativo de um NaN é outro NaN)

O tipo da expressão é o tipo após a promoção, e a [categoria de valor](<#/doc/language/value_category>) é non-lvalue.

#### Notas

O menos unário invoca comportamento indefinido devido a overflow de inteiro com sinal quando aplicado a [INT_MIN](<#/doc/types/limits>), [LONG_MIN](<#/doc/types/limits>) ou [LLONG_MIN](<#/doc/types/limits>), em plataformas típicas (complemento de 2).

Em C++, o operador unário `+` também pode ser usado com outros tipos embutidos, como arrays e funções, o que não ocorre em C.

Execute este código
```c
    #include <stdio.h>
    #include <complex.h>
    #include <limits.h>
    
    int main(void)
    {
        char c = 'a';
        printf("sizeof char: %zu sizeof int: %zu\n", sizeof c, sizeof +c);
    
        printf("-1, where 1 is signed: %d\n", -1);
    
        // Defined behavior since arithmetic is performed for unsigned integer.
        // Hence, the calculation is (-1) modulo (2 raised to n) = UINT_MAX, where n is
        // the number of bits of unsigned int. If unsigned int is 32-bit long, then this
        // gives (-1) modulo (2 raised to 32) = 4294967295
        printf("-1, where 1 is unsigned: %u\n", -1u); 
    
        // Undefined behavior because the mathematical value of -INT_MIN = INT_MAX + 1
        // (i.e. 1 more than the maximum possible value for signed int)
        //
        // printf("%d\n", -INT_MIN);
    
        // Undefined behavior because the mathematical value of -LONG_MIN = LONG_MAX + 1
        // (i.e. 1 more than the maximum possible value for signed long)
        //
        // printf("%ld\n", -LONG_MIN);
    
        // Undefined behavior because the mathematical value of -LLONG_MIN = LLONG_MAX + 1
        // (i.e. 1 more than the maximum possible value for signed long long)
        //
        // printf("%lld\n", -LLONG_MIN);
    
        double complex z = 1 + 2*I;
        printf("-(1+2i) = %.1f%+.1f\n", creal(-z), cimag(-z));
    }
```

Saída possível:
```
    sizeof char: 1 sizeof int: 4
    -1, where 1 is signed: -1
    -1, where 1 is unsigned: 4294967295
    -(1+2i) = -1.0-2.0
```

### Operadores aditivos

As expressões de operadores aritméticos aditivos binários têm a forma

---
lhs `+` rhs | (1)
lhs `-` rhs | (2)

1) adição: lhs e rhs devem ser um dos seguintes

* ambos têm [tipos aritméticos](<#/doc/language/arithmetic_types>), incluindo complexos e imaginários
* um é um ponteiro para um tipo de objeto completo, o outro tem tipo inteiro

2) subtração: lhs e rhs devem ser um dos seguintes

* ambos têm [tipos aritméticos](<#/doc/language/arithmetic_types>), incluindo complexos e imaginários
* lhs tem ponteiro para um tipo de objeto completo, rhs tem tipo inteiro
* ambos são ponteiros para objetos completos de tipos [compatíveis](<#/doc/language/compatible_type>), ignorando qualificadores

#### Adição e subtração aritméticas

Se ambos os operandos têm [tipos aritméticos](<#/doc/language/arithmetic_types>), então

* primeiro, [conversões aritméticas usuais](<#/doc/language/conversion>) são realizadas
* então, os valores dos operandos após as conversões são adicionados ou subtraídos seguindo as regras usuais da matemática (para subtração, rhs é subtraído de lhs), exceto que

* se um operando é NaN, o resultado é NaN
* infinito menos infinito é NaN e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado
* infinito mais infinito negativo é NaN e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado

A adição e subtração de números complexos e imaginários são definidas da seguinte forma (observe que o tipo do resultado é imaginário se ambos os operandos são imaginários e complexo se um operando é real e o outro imaginário, conforme especificado pelas conversões aritméticas usuais):

+ ou - | u | iv | u + iv
x | x ± u | x ± iv | (x ± u) ± iv
iy | ±u + iy | i(y ± v) | ±u + i(y ± v)
x + iy | (x ± u) + iy | x + i(y ± v) | (x ± u) + i(y ± v)

Execute este código
```c
    // work in progress
    // note: take part of the c/language/conversion example
```

#### Aritmética de ponteiros

* Se o ponteiro `P` aponta para um elemento de um array com índice `I`, então

* P+N e N+P são ponteiros que apontam para um elemento do mesmo array com índice `I+N`
* P-N é um ponteiro que aponta para um elemento do mesmo array com índice `I-N`

O comportamento é definido apenas se tanto o ponteiro original quanto o ponteiro resultante apontam para elementos do mesmo array ou para uma posição logo após o final desse array. Note que executar p-1 quando p aponta para o primeiro elemento de um array é comportamento indefinido e pode falhar em algumas plataformas.

* Se o ponteiro `P1` aponta para um elemento de um array com índice `I` (ou uma posição logo após o final) e `P2` aponta para um elemento do mesmo array com índice `J` (ou uma posição logo após o final), então

* P1-P2 tem o valor igual a I-J e o tipo [ptrdiff_t](<#/doc/types/ptrdiff_t>) (que é um tipo inteiro com sinal, tipicamente metade do tamanho do maior objeto que pode ser declarado)

O comportamento é definido apenas se o resultado cabe em [ptrdiff_t](<#/doc/types/ptrdiff_t>).

Para fins de aritmética de ponteiros, um ponteiro para um objeto que não é um elemento de nenhum array é tratado como um ponteiro para o primeiro elemento de um array de tamanho 1.

Execute este código
```c
    // work in progress
    int n = 4, m = 3;
    int a[n][m];     // VLA of 4 VLAs of 3 ints each
    int (*p)[m] = a; // p == &a[0] 
    p = p + 1;       // p == &a[1] (pointer arithmetic works with VLAs just the same)
    (*p)[2] = 99;    // changes a[1][2]
```

### Operadores multiplicativos

As expressões de operadores aritméticos multiplicativos binários têm a forma

---
lhs `*` rhs | (1)
lhs `/` rhs | (2)
lhs `%` rhs | (3)

1) multiplicação. lhs e rhs devem ter [tipos aritméticos](<#/doc/language/arithmetic_types>)

2) divisão. lhs e rhs devem ter [tipos aritméticos](<#/doc/language/arithmetic_types>)

3) resto. lhs e rhs devem ter [tipos inteiros](<#/doc/language/arithmetic_types>)

* primeiro, [conversões aritméticas usuais](<#/doc/language/conversion>) são realizadas. Então...

#### Multiplicação

O operador binário * realiza a multiplicação de seus operandos (após as conversões aritméticas usuais) seguindo as definições aritméticas usuais, exceto que

* se um operando é um NaN, o resultado é um NaN
* a multiplicação de infinito por zero resulta em NaN e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado
* a multiplicação de infinito por um valor não-zero resulta em infinito (mesmo para argumentos complexos)

Como em C, qualquer [valor complexo](<#/doc/language/arithmetic_types>) com pelo menos uma parte infinita é um infinito, mesmo que sua outra parte seja um NaN, as regras aritméticas usuais não se aplicam à multiplicação complexo-complexo. Outras combinações de operandos de ponto flutuante seguem a tabela abaixo:

* | u | iv | u + iv
x | xu | i(xv) | (xu) + i(xv)
iy | i(yu) | −yv | (−yv) + i(yu)
x + iy | (xu) + i(yu) | (−yv) + i(xv) | _special rules_

Além do tratamento de infinito, a multiplicação complexa não pode causar overflow em resultados intermediários, exceto quando [` #pragma STDC CX_LIMITED_RANGE`](<#/doc/preprocessor/impl>) é definido como `ON`, caso em que o valor pode ser calculado como se fosse (x+iy)×(u+iv) = (xu-yv)+i(yu+xv), pois o programador assume a responsabilidade de limitar o alcance dos operandos e lidar com os infinitos.

Apesar de não permitir overflow indevido, a multiplicação complexa pode levantar exceções de ponto flutuante espúrias (caso contrário, é proibitivamente difícil implementar versões que não causem overflow).

Execute este código
```c
    #include <stdio.h>
    #include <stdio.h>
    #include <complex.h>
    #include <math.h>
    int main(void)
    {
    
    
    // TODO simpler cases, take some from C++
    
    
       double complex z = (1 + 0*I) * (INFINITY + I*INFINITY);
    // textbook formula would give
    // (1+i0)(∞+i∞) ⇒ (1×∞ – 0×∞) + i(0×∞+1×∞) ⇒ NaN + I*NaN
    // but C gives a complex infinity
       printf("%f + i*%f\n", creal(z), cimag(z));
    
    // textbook formula would give
    // cexp(∞+iNaN) ⇒ exp(∞)×(cis(NaN)) ⇒ NaN + I*NaN
    // but C gives  ±∞+i*nan
       double complex y = cexp(INFINITY + I*NAN);
       printf("%f + i*%f\n", creal(y), cimag(y));
    
    }
```

Saída possível:
```
    inf + i*inf 
    inf + i*nan
```

#### Divisão

O operador binário `/` divide o primeiro operando pelo segundo (após as conversões aritméticas usuais) seguindo as definições aritméticas usuais, exceto que

* quando o tipo após as conversões aritméticas usuais é um tipo inteiro, o resultado é o quociente algébrico (não uma fração), arredondado em uma direção definida pela implementação (até C99) truncado em direção a zero (desde C99)
* se um operando é um NaN, o resultado é um NaN
* se o primeiro operando é um infinito complexo e o segundo operando é finito, então o resultado do operador `/` é um infinito complexo
* se o primeiro operando é finito e o segundo operando é um infinito complexo, então o resultado do operador `/` é zero.

Como em C, qualquer [valor complexo](<#/doc/language/arithmetic_types>) com pelo menos uma parte infinita é um infinito, mesmo que sua outra parte seja um NaN, as regras aritméticas usuais não se aplicam à divisão complexo-complexo. Outras combinações de operandos de ponto flutuante seguem a tabela abaixo:

/ | u | iv
x | x/u | i(−x/v)
iy | i(y/u) | y/v
x + iy | (x/u) + i(y/u) | (y/v) + i(−x/v)

Além do tratamento de infinito, a divisão complexa não pode causar overflow em resultados intermediários, exceto quando [` #pragma STDC CX_LIMITED_RANGE`](<#/doc/preprocessor/impl>) é definido como `ON`, caso em que o valor pode ser calculado como se fosse (x+iy)/(u+iv) = [(xu+yv)+i(yu-xv)]/(u2
+v2
), pois o programador assume a responsabilidade de limitar o alcance dos operandos e lidar com os infinitos.

Apesar de não permitir overflow indevido, a divisão complexa pode levantar exceções de ponto flutuante espúrias (caso contrário, é proibitivamente difícil implementar versões que não causem overflow).

Se o segundo operando for zero, o comportamento é indefinido, exceto que, se a aritmética de ponto flutuante IEEE for suportada e a divisão de ponto flutuante estiver ocorrendo, então

* Dividir um número não-zero por ±0.0 resulta no infinito com sinal correto e [FE_DIVBYZERO](<#/doc/numeric/fenv/FE_exceptions>) é levantado
* Dividir 0.0 por 0.0 resulta em NaN e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado

#### Resto

O operador binário % retorna o resto da divisão do primeiro operando pelo segundo (após as conversões aritméticas usuais).

O sinal do resto é definido de tal forma que, se o quociente `a/b` for representável no tipo de resultado, então (a/b)*b + a%b == a.

Se o segundo operando for zero, o comportamento é indefinido.

Se o quociente `a/b` não for representável no tipo de resultado, o comportamento de `a/b` e `a%b` é indefinido (isso significa que INT_MIN%-1 é indefinido em sistemas de complemento de 2).

Nota: o operador de resto não funciona em tipos de ponto flutuante; a função de biblioteca [fmod](<#/doc/numeric/math/fmod>) fornece essa funcionalidade.

### Lógica bit a bit

As expressões de operadores aritméticos bit a bit têm a forma

---
`~` rhs | (1)
lhs `&` rhs | (2)
lhs `|` rhs | (3)
lhs `^` rhs | (4)

1) NOT bit a bit

2) AND bit a bit

3) OR bit a bit

4) XOR bit a bit

onde

- **lhs, rhs** — expressões de tipo inteiro

Primeiro, os operadores &, ^ e | realizam [conversões aritméticas usuais](<#/doc/language/conversion>) em ambos os operandos, e o operador ~ realiza [promoções inteiras](<#/doc/language/conversion>) em seu único operando.

Em seguida, os operadores lógicos binários correspondentes são aplicados bit a bit; ou seja, cada bit do resultado é definido ou limpo de acordo com a operação lógica (NOT, AND, OR ou XOR), aplicada aos bits correspondentes dos operandos.

Nota: operadores bit a bit são comumente usados para manipular conjuntos de bits e máscaras de bits.

Nota: para tipos sem sinal (após a promoção), a expressão ~E é equivalente ao valor máximo representável pelo tipo de resultado menos o valor original de E.

Execute este código
```c
    #include <stdio.h>
    #include <stdint.h>
    
    int main(void)
    {
        uint32_t a = 0x12345678;
        uint16_t mask = 0x00f0;
    
        printf("Promoted mask:\t%#010x\n"
               "Value:\t\t%#x\n"
               "Setting bits:\t%#x\n"
               "Clearing bits:\t%#x\n"
               "Selecting bits:\t%#010x\n"
               , mask
               , a
               , a | mask
               , a & ~mask
               , a & mask
        );
    }
```

Saída possível:
```
    Promoted mask:  0x000000f0
    Value:          0x12345678
    Setting bits:   0x123456f8
    Clearing bits:  0x12345608
    Selecting bits: 0x00000070
```

### Operadores de deslocamento

As expressões de operadores de deslocamento bit a bit têm a forma

---
lhs `< <` rhs | (1)
lhs `> >` rhs | (2)

1) deslocamento à esquerda de lhs por rhs bits

2) deslocamento à direita de lhs por rhs bits

onde

- **lhs, rhs** — expressões de tipo inteiro

Primeiro, [promoções inteiras](<#/doc/language/conversion>) são realizadas, individualmente, em cada operando (Nota: isso é diferente de outros operadores aritméticos binários, que todos realizam conversões aritméticas usuais). O tipo do resultado é o tipo de lhs após a promoção.

O comportamento é indefinido se rhs for negativo ou for maior ou igual ao número de bits no lhs promovido.

Para lhs sem sinal, o valor de `LHS << RHS` é o valor de LHS * 2RHS
, reduzido módulo o valor máximo do tipo de retorno mais 1 (ou seja, o deslocamento bit a bit à esquerda é realizado e os bits que são deslocados para fora do tipo de destino são descartados). Para lhs com sinal e valores não negativos, o valor de `LHS << RHS` é LHS * 2RHS
se for representável no tipo promovido de lhs, caso contrário, o comportamento é indefinido.

Para lhs sem sinal e para lhs com sinal e valores não negativos, o valor de `LHS >> RHS` é a parte inteira de LHS / 2RHS
. Para `LHS` negativo, o valor de `LHS >> RHS` é definido pela implementação, onde na maioria das implementações, isso realiza um deslocamento aritmético à direita (para que o resultado permaneça negativo). Assim, na maioria das implementações, deslocar um `LHS` com sinal para a direita preenche os novos bits de ordem superior com o bit de sinal original (ou seja, com 0 se era não negativo e 1 se era negativo).

Execute este código
```c
    #include <stdio.h>
    enum {ONE=1, TWO=2};
    int main(void)
    {
        char c = 0x10;
        unsigned long long ulong_num = 0x123;
        printf("0x123 << 1  = %#llx\n"
               "0x123 << 63 = %#llx\n"   // overflow truncates high bits for unsigned numbers
               "0x10  << 10 = %#x\n",    // char is promoted to int
               ulong_num << 1, ulong_num << 63, c << 10);
        long long long_num = -1000;
        printf("-1000 >> 1 = %lld\n", long_num >> ONE);  // implementation defined
    }
```

Saída possível:
```
    0x123 << 1  = 0x246
    0x123 << 63 = 0x8000000000000000
    0x10  << 10 = 0x4000
    -1000 >> 1 = -500
```

### Referências

* Padrão C17 (ISO/IEC 9899:2018):

* 6.5.3.3 Operadores aritméticos unários (p: 64)

* 6.5.5 Operadores multiplicativos (p: 66)

* 6.5.6 Operadores aditivos (p: 66-68)

* 6.5.7 Operadores de deslocamento bit a bit (p: 68)

* 6.5.10 Operador AND bit a bit (p: 70)

* 6.5.11 Operador OR exclusivo bit a bit (p: 70)

* 6.5.12 Operador OR inclusivo bit a bit (p: 70-71)

* Padrão C11 (ISO/IEC 9899:2011):

* 6.5.3.3 Operadores aritméticos unários (p: 89)

* 6.5.5 Operadores multiplicativos (p: 92)

* 6.5.6 Operadores aditivos (p: 92-94)

* 6.5.7 Operadores de deslocamento bit a bit (p: 94-95)

* 6.5.10 Operador AND bit a bit (p: 97)

* 6.5.11 Operador OR exclusivo bit a bit (p: 98)

* 6.5.12 Operador OR inclusivo bit a bit (p: 98)

* Padrão C99 (ISO/IEC 9899:1999):

* 6.5.3.3 Operadores aritméticos unários (p: 79)

* 6.5.5 Operadores multiplicativos (p: 82)

* 6.5.6 Operadores aditivos (p: 82-84)

* 6.5.7 Operadores de deslocamento bit a bit (p: 84-85)

* 6.5.10 Operador AND bit a bit (p: 87)

* 6.5.11 Operador OR exclusivo bit a bit (p: 88)

* 6.5.12 Operador OR inclusivo bit a bit (p: 88)

* Padrão C89/C90 (ISO/IEC 9899:1990):

* 3.3.3.3 Operadores aritméticos unários

* 3.3.5 Operadores multiplicativos

* 3.3.6 Operadores aditivos

* 3.3.7 Operadores de deslocamento bit a bit

* 3.3.10 Operador AND bit a bit

* 3.3.11 Operador OR exclusivo bit a bit

* 3.3.12 Operador OR inclusivo bit a bit

### Veja também

[Precedência de operadores](<#/doc/language/operator_precedence>)

Operadores comuns
---
[atribuição](<#/doc/language/operator_assignment>) | [incremento
decremento](<#/doc/language/operator_incdec>) | **aritméticos** | [lógicos](<#/doc/language/operator_logical>) | [comparação](<#/doc/language/operator_comparison>) | [acesso a membros](<#/doc/language/operator_member_access>) | [outros](<#/doc/language/operator_other>)
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
[Documentação C++](<#/>) para Operadores aritméticos
---