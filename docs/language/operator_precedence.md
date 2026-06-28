# Precedência de Operadores C

A tabela a seguir lista a precedência e associatividade dos operadores C. Os operadores são listados de cima para baixo, em ordem decrescente de precedência.

Precedência | Operador | Descrição | Associatividade
1 | `++` `--` | Incremento e decremento sufixo/pós-fixo | Da esquerda para a direita
`()` | Chamada de função
`[]` | Indexação de array
`.` | Acesso a membro de estrutura e união
`->` | Acesso a membro de estrutura e união através de ponteiro
`(_type_){_list_}` | Literal composto (C99)
2 | `++` `--` | Incremento e decremento prefixo[note 1](<#/doc/language/operator_precedence>) | Da direita para a esquerda
`+` `-` | Mais e menos unário
`!` `~` | NOT lógico e NOT bit a bit
`(_type_)` | Cast
`*` | Indireção (desreferência)
`&` | Endereço de
`sizeof` | Tamanho de[note 2](<#/doc/language/operator_precedence>)
`_Alignof` | Requisito de alinhamento (C11)
3 | `*` `/` `%` | Multiplicação, divisão e resto | Da esquerda para a direita
4 | `+` `-` | Adição e subtração
5 | `<<` `>>` | Deslocamento de bits para a esquerda e para a direita
6 | `<` `<=` | Para operadores relacionais < e ≤, respectivamente
`>` `>=` | Para operadores relacionais > e ≥, respectivamente
7 | `==` `!=` | Para operadores relacionais = e ≠, respectivamente
8 | `&` | AND bit a bit
9 | `^` | XOR bit a bit (ou exclusivo)
10 | `|` | OR bit a bit (ou inclusivo)
11 | `&&` | AND lógico
12 | `||` | OR lógico
13 | `?:` | Condicional ternário[note 3](<#/doc/language/operator_precedence>) | Da direita para a esquerda
14[note 4](<#/doc/language/operator_precedence>) | `=` | Atribuição simples
`+=` `-=` | Atribuição por soma e diferença
`*=` `/=` `% =` | Atribuição por produto, quociente e resto
`<<=` `>>=` | Atribuição por deslocamento de bits para a esquerda e para a direita
`&=` `^=` `|=` | Atribuição por AND, XOR e OR bit a bit
15 | `,` | Vírgula | Da esquerda para a direita

1.  [↑](<#/doc/language/operator_precedence>) O operando de prefixo `++` e `--` não pode ser uma conversão de tipo (type cast). Esta regra proíbe gramaticalmente algumas expressões que seriam semanticamente inválidas de qualquer forma. Alguns compiladores ignoram esta regra e detectam a invalidade semanticamente.
2.  [↑](<#/doc/language/operator_precedence>) O operando de `sizeof` não pode ser uma conversão de tipo (type cast): a expressão `sizeof (int) * p` é interpretada inequivocamente como `(sizeof(int)) * p`, mas não `sizeof((int)*p)`.
3.  [↑](<#/doc/language/operator_precedence>) A expressão no meio do operador condicional (entre `?` e `:`) é analisada como se estivesse entre parênteses: sua precedência em relação a `?:` é ignorada.
4.  [↑](<#/doc/language/operator_precedence>) Os operandos esquerdos dos operadores de atribuição devem ser expressões unárias (nível 2, sem conversão de tipo). Esta regra proíbe gramaticalmente algumas expressões que seriam semanticamente inválidas de qualquer forma. Muitos compiladores ignoram esta regra e detectam a invalidade semanticamente. Por exemplo, `e = a < d ? a++ : a = d` é uma expressão que não pode ser analisada por causa desta regra. No entanto, muitos compiladores ignoram esta regra e a analisam como `e = ( ((a < d) ? (a++) : a) = d )`, e então geram um erro porque é semanticamente inválida.

Ao analisar uma expressão, um operador listado em uma linha será ligado mais fortemente (como se por parênteses) aos seus argumentos do que qualquer operador listado em uma linha abaixo dele. Por exemplo, a expressão `*p++` é analisada como `*(p++)`, e não como `(*p)++`.

Operadores que estão na mesma célula (pode haver várias linhas de operadores listados em uma célula) são avaliados com a mesma precedência, na direção dada. Por exemplo, a expressão `a=b=c` é analisada como `a=(b=c)`, e não como `(a=b)=c` por causa da associatividade da direita para a esquerda.

### Observações

Precedência e associatividade são independentes da [ordem de avaliação](<#/doc/language/eval_order>).

O próprio padrão não especifica níveis de precedência. Eles são derivados da gramática.

Em C++, o operador condicional tem a mesma precedência que os operadores de atribuição, e os operadores de prefixo `++` e `--` e os operadores de atribuição não têm as restrições sobre seus operandos.

A especificação de associatividade é redundante para operadores unários e é mostrada apenas para completude: operadores unários prefixos sempre associam da direita para a esquerda (`sizeof ++*p` é `sizeof(++(*p))`) e operadores unários pós-fixos sempre associam da esquerda para a direita (`a[1][2]++` é `((a[1])[2])++`). Note que a associatividade é significativa para operadores de acesso a membros, mesmo que sejam agrupados com operadores unários pós-fixos: `a.b++` é analisado como `(a.b)++` e não `a.(b++)`.

### Referências

*   Padrão C17 (ISO/IEC 9899:2018):
    *   A.2.1 Expressões
*   Padrão C11 (ISO/IEC 9899:2011):
    *   A.2.1 Expressões
*   Padrão C99 (ISO/IEC 9899:1999):
    *   A.2.1 Expressões
*   Padrão C89/C90 (ISO/IEC 9899:1990):
    *   A.1.2.1 Expressões

### Veja também

[Ordem de avaliação](<#/doc/language/eval_order>) dos argumentos do operador em tempo de execução.

Operadores comuns
---
[atribuição](<#/doc/language/operator_assignment>) | [incremento decremento](<#/doc/language/operator_incdec>) | [aritméticos](<#/doc/language/operator_arithmetic>) | [lógicos](<#/doc/language/operator_logical>) | [comparação](<#/doc/language/operator_comparison>) | [acesso a membro](<#/doc/language/operator_member_access>) | [outros](<#/doc/language/operator_other>)
`a = b`
`a += b`
`a -= b`
`a *= b`
`a /= b`
`a %= b`
`a &= b`
`a |= b`
`a ^= b`
`a <<= b`
`a >>= b` | `++a`
`--a`
`a++`
`a--` | `+a`
`-a`
`a + b`
`a - b`
`a * b`
`a / b`
`a % b`
`~a`
`a & b`
`a | b`
`a ^ b`
`a << b`
`a >> b` | `!a`
`a && b`
`a || b` | `a == b`
`a != b`
`a < b`
`a > b`
`a <= b`
`a >= b` | `a[b]`
`*a`
`&a`
`a->b`
`a.b` | `a(...)`
`a, b`
`(type) a`
`a ? b : c`
`sizeof`

`_Alignof`
(desde C11)
(até C23)

`alignof`
(desde C23)
[documentação C++](<#/>) para precedência de operadores C++