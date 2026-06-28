# Expressões

Uma expressão é uma sequência de _operadores_ e seus _operandos_, que especifica um cálculo.

A avaliação de uma expressão pode produzir um resultado (por exemplo, a avaliação de 2 + 2 produz o resultado 4), pode gerar efeitos colaterais (por exemplo, a avaliação de [printf](<#/doc/io/fprintf>)("%d", 4) envia o caractere '4' para o fluxo de saída padrão), e pode designar objetos ou funções.

#### Geral

  * [categorias de valor](<#/doc/language/value_category>) (lvalue, objeto não-lvalue, designador de função) classificam expressões por seus valores
  * [ordem de avaliação](<#/doc/language/eval_order>) de argumentos e subexpressões especifica a ordem em que os resultados intermediários são obtidos

### Operadores

Operadores comuns
---
[atribuição](<#/doc/language/operator_assignment>) | [incremento
decremento](<#/doc/language/operator_incdec>) | [aritméticos](<#/doc/language/operator_arithmetic>) | [lógicos](<#/doc/language/operator_logical>) | [comparação](<#/doc/language/operator_comparison>) | [acesso a
membro](<#/doc/language/operator_member_access>) | [outros](<#/doc/language/operator_other>)
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

  * [precedência de operadores](<#/doc/language/operator_precedence>) define a ordem em que os operadores são ligados aos seus argumentos
  * [representações alternativas](<#/doc/language/operator_alternative>) são grafias alternativas para alguns operadores

#### Conversões

  * [Conversões implícitas](<#/doc/language/conversion>) ocorrem quando os tipos dos operandos não correspondem às expectativas dos operadores
  * [Casts](<#/doc/language/cast>) podem ser usados para converter explicitamente valores de um tipo para outro.

#### Outros

  * [expressões constantes](<#/doc/language/constant_expression>) podem ser avaliadas em tempo de compilação e usadas em contexto de tempo de compilação (tamanhos de array não-VLA(desde C99), inicializadores estáticos, etc)

  * [seleções genéricas](<#/doc/language/generic>) podem executar diferentes expressões dependendo dos tipos dos argumentos

| (desde C11)

  * A aritmética de ponto flutuante pode levantar exceções e reportar erros conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>)
  * As [#pragmas](<#/doc/preprocessor/impl>) padrão `FENV_ACCESS`, `FP_CONTRACT` e `CX_LIMITED_RANGE`, bem como a [precisão de avaliação de ponto flutuante](<#/doc/types/limits/FLT_EVAL_METHOD>) e a [direção de arredondamento](<#/doc/numeric/fenv/FE_round>) controlam a forma como a aritmética de ponto flutuante é executada.

| (desde C99)

### Expressões primárias

Os operandos de qualquer operador podem ser outras expressões ou podem ser _expressões primárias_ (por exemplo, em 1 + 2 * 3, os operandos do operador+ são a subexpressão 2 * 3 e a expressão primária 1).

Expressões primárias são qualquer uma das seguintes:

1) Constantes e literais (por exemplo, 2 ou "Hello, world")

2) [Identificadores](<#/doc/language/identifier>) devidamente declarados (por exemplo, n ou [printf](<#/doc/io/fprintf>))

3) [Seleções genéricas](<#/doc/language/generic>) | (desde C11)

Qualquer expressão entre parênteses também é classificada como uma expressão primária: isso garante que os parênteses tenham precedência maior do que qualquer operador.

#### Constantes e literais

Valores constantes de certos tipos podem ser incorporados no código-fonte de um programa C usando expressões especializadas conhecidas como literais (para expressões lvalue) e constantes (para expressões não-lvalue)

  * [constantes inteiras](<#/doc/language/integer_constant>) são números decimais, octais ou hexadecimais de tipo inteiro.
  * [constantes de caractere](<#/doc/language/character_constant>) são caracteres individuais do tipo int adequados para conversão para um tipo de caractere ou do tipo char8_t,(desde C23) char16_t, char32_t, ou(desde C11) wchar_t
  * [constantes de ponto flutuante](<#/doc/language/floating_constant>) são valores do tipo float, double ou long double

  * constantes predefinidas [true/false](<#/doc/language/bool_constant>) são valores do tipo bool
  * a constante predefinida [`nullptr`](<#/doc/language/nullptr>) é um valor do tipo [nullptr_t](<#/doc/types/nullptr_t>)

| (desde C23)

  * [literais de string](<#/doc/language/string_literal>) são sequências de caracteres do tipo char[], char8_t[](desde C23), char16_t[], char32_t[],(desde C11) ou wchar_t[] que representam strings terminadas em nulo

  * [literais compostos](<#/doc/language/compound_literal>) são valores do tipo struct, union ou array diretamente incorporados no código do programa

| (desde C99)

### Expressões não avaliadas

Os operandos do [operador sizeof](<#/doc/language/sizeof>) são expressões que não são avaliadas (a menos que sejam VLAs)(desde C99). Assim, [size_t](<#/doc/types/size_t>) n = sizeof([printf](<#/doc/io/fprintf>)("%d", 4)); não realiza saída no console.

Os operandos do operador [`_Alignof`](<#/doc/language/alignof>)(ate C23)[`alignof`](<#/doc/language/alignof>)(desde C23), a expressão de controle de uma [seleção genérica](<#/doc/language/generic>), e expressões de tamanho de VLAs que são operandos de `_Alignof`(ate C23)alignof(desde C23) também são expressões que não são avaliadas. | (desde C11)

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

  * 6.5 Expressões (p: TBD)

  * 6.6 Expressões constantes (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

  * 6.5 Expressões (p: 55-75)

  * 6.6 Expressões constantes (p: 76-77)

  * Padrão C11 (ISO/IEC 9899:2011):

  * 6.5 Expressões (p: 76-105)

  * 6.6 Expressões constantes (p: 106-107)

  * Padrão C99 (ISO/IEC 9899:1999):

  * 6.5 Expressões (p: 67-94)

  * 6.6 Expressões constantes (p: 95-96)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

  * 3.3 EXPRESSÕES

  * 3.4 EXPRESSÕES CONSTANTES

### Ver também

[Documentação C++](<#/>) para Expressões
---