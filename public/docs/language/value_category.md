# Categorias de valor

Cada [expressão](<#/doc/language/expressions>) em C (um operador com seus argumentos, uma chamada de função, uma constante, um nome de variável, etc) é caracterizada por duas propriedades independentes: um [tipo](<#/doc/language/compatible_type>) e uma [categoria de valor](<#/doc/language/expressions>).

Toda expressão pertence a uma das três categorias de valor: lvalue, objeto não-lvalue (rvalue) e designador de função.

### Expressões lvalue

Uma expressão lvalue é qualquer expressão com [tipo de objeto](<#/doc/language/compatible_type>) diferente do tipo `void`, que potencialmente designa um [objeto](<#/doc/language/object>) (o comportamento é indefinido se um lvalue não designar realmente um objeto quando avaliado). Em outras palavras, uma expressão lvalue avalia para a _identidade do objeto_. O nome desta categoria de valor ("valor esquerdo") é histórico e reflete o uso de expressões lvalue como o operando do lado esquerdo do operador de atribuição na linguagem de programação CPL.

Expressões lvalue podem ser usadas nos seguintes _contextos lvalue_:

*   como o operando do [operador address-of](<#/doc/language/operator_member_access>) (exceto se o lvalue designar um [bit-field](<#/doc/language/bit_field>) ou tiver sido declarado [register](<#/doc/language/storage_duration>)).
*   como o operando dos [operadores de incremento e decremento](<#/doc/language/operator_incdec>) pré/pós.
*   como o operando do lado esquerdo do [operador de acesso a membro](<#/doc/language/operator_member_access>) (ponto).
*   como o operando do lado esquerdo dos [operadores de atribuição e atribuição composta](<#/doc/language/operator_assignment>).

Se uma expressão lvalue for usada em qualquer contexto diferente de [`sizeof`](<#/doc/language/sizeof>), [`_Alignof`](<#/doc/language/alignof>), ou dos operadores listados acima, lvalues não-array de qualquer tipo completo sofrem [conversão lvalue](<#/doc/language/conversion>), que modela o carregamento da memória do valor do objeto de sua localização. Similarmente, lvalues array sofrem [conversão de array para ponteiro](<#/doc/language/conversion>) quando usados em qualquer contexto diferente de `sizeof`, `_Alignof`, operador address-of, ou inicialização de array a partir de um literal de string.

A semântica dos qualificadores [`const`](<#/doc/language/const>)/[`volatile`](<#/doc/language/volatile>)/[`restrict`](<#/doc/language/restrict>) e dos tipos [atômicos](<#/doc/language/atomic>) aplica-se apenas a lvalues (a conversão lvalue remove os qualificadores e a atomicidade).

As seguintes expressões são lvalues:

*   identificadores, incluindo parâmetros nomeados de função, desde que tenham sido declarados como designando objetos (não funções ou constantes de enumeração)
*   [literais de string](<#/doc/language/string_literal>)
*   (desde C99) [literais compostos](<#/doc/language/compound_literal>)
*   expressão entre parênteses se a expressão sem parênteses for um lvalue
*   o resultado de um operador de acesso a membro (ponto) se seu argumento do lado esquerdo for um lvalue
*   o resultado de um acesso a membro através do operador de ponteiro `- >`
*   o resultado do operador de indireção (unário `*`) aplicado a um ponteiro para objeto
*   o resultado do operador de subscrição (`[]`)

#### Expressões lvalue modificáveis

Um _lvalue modificável_ é qualquer expressão lvalue de tipo completo, não-array, que não é qualificada como [const](<#/doc/language/const>), e, se for uma struct/union, não possui membros qualificados como [const](<#/doc/language/const>), recursivamente.

Apenas expressões lvalue modificáveis podem ser usadas como argumentos para incremento/decremento, e como argumentos do lado esquerdo de operadores de atribuição e atribuição composta.

### Expressões de objeto não-lvalue

Conhecidas como _rvalues_, as expressões de objeto não-lvalue são as expressões de tipos de objeto que não designam objetos, mas sim valores que não possuem identidade de objeto ou localização de armazenamento. O endereço de uma expressão de objeto não-lvalue não pode ser obtido.

As seguintes expressões são expressões de objeto não-lvalue:

*   constantes inteiras, de caractere e de ponto flutuante
*   todos os operadores não especificados para retornar lvalues, incluindo

*   qualquer expressão de chamada de função
*   qualquer expressão de cast (note que literais compostos, que parecem similares, são lvalues)
*   operador de acesso a membro (ponto) aplicado a uma struct/union não-lvalue, f().x, (x,s1).a, (s1=s2).m
*   resultados de todos os operadores aritméticos, relacionais, lógicos e bit a bit
*   resultados dos operadores de incremento e decremento (nota: as formas pré são lvalues em C++)
*   resultados dos operadores de atribuição (nota: também são lvalues em C++)
*   o operador condicional (nota: é lvalue em C++ se ambos o segundo e terceiro operandos forem lvalues do mesmo tipo)
*   o operador vírgula (nota: é lvalue em C++ se o segundo operando for)
*   o operador address-of, mesmo que neutralizado pela aplicação ao resultado do operador unário `*`

Como um caso especial, expressões do tipo `void` são consideradas expressões de objeto não-lvalue que produzem um valor que não possui representação e não requer armazenamento.

Note que um rvalue de struct/union que possui um membro (possivelmente aninhado) do tipo array de fato designa um objeto com [tempo de vida temporário](<#/doc/language/lifetime>). Este objeto pode ser acessado através de expressões lvalue que se formam indexando o membro array ou por indireção através do ponteiro obtido pela conversão de array para ponteiro do membro array.

### Expressão designadora de função

Um designador de função (o identificador introduzido por uma [declaração de função](<#/doc/language/function_declaration>)) é uma expressão de tipo de função. Quando usado em qualquer contexto diferente do operador address-of, [`sizeof`](<#/doc/language/sizeof>), e [`_Alignof`](<#/doc/language/alignof>) (os dois últimos geram erros de compilação quando aplicados a funções), o designador de função é sempre convertido para um ponteiro não-lvalue para função. Note que o operador de chamada de função é definido para ponteiros para funções e não para os próprios designadores de função.

### Referências

*   Padrão C17 (ISO/IEC 9899:2018):

*   6.3.2.1 Lvalues, arrays, and function designators (p: 40)

*   Padrão C11 (ISO/IEC 9899:2011):

*   6.3.2.1 Lvalues, arrays, and function designators (p: 54-55)

*   Padrão C99 (ISO/IEC 9899:1999):

*   6.3.2.1 Lvalues, arrays, and function designators (p: 46)

*   Padrão C89/C90 (ISO/IEC 9899:1990):

*   3.2.2.1 Lvalues and function designators

### Veja também

[Documentação C++](<#/>) para Categorias de valor
---