# Pontuação

Estes são os símbolos de pontuação em C. O significado de cada símbolo é detalhado nas páginas linkadas.

### `{` `}`

  * Em uma definição de [struct](<#/doc/language/struct>) ou [union](<#/doc/language/union>), delimita a lista de declarações da struct.
  * Em uma definição de [enum](<#/doc/language/enum>), delimita a lista de enumeradores.
  * Delimita uma [instrução composta](<#/doc/language/statements>). A instrução composta pode fazer parte de uma [definição de função](<#/doc/language/function_definition>).
  * Na [inicialização](<#/doc/language/initialization>), delimita os inicializadores.

### `[` `]`

  * [Operador de subscrito](<#/doc/language/operator_member_access>).
  * Parte do [declarador de array](<#/doc/language/declarations>) em uma [declaração](<#/doc/language/declarations>) ou um [type-id](<#/doc/language/compatible_type>).
  * Na [inicialização](<#/doc/language/initialization>), introduz um designador para um elemento de array. (desde C99)
  * Em um [especificador de atributo](<#/doc/language/attributes>), delimita os atributos. (desde C23)

### `#`

  * Introduz uma [diretiva de pré-processamento](<#/doc/preprocessor>).
  * O [operador de pré-processamento para stringification](<#/doc/preprocessor/replace>).

### `##`

  * O [operador de pré-processamento para colagem de tokens](<#/doc/preprocessor/replace>).

### `(` `)`

  * Em uma expressão, [indica agrupamento](<#/doc/language/expressions>).
  * [Operador de chamada de função](<#/doc/language/operator_other>).
  * Em uma expressão [`sizeof`](<#/doc/language/sizeof>), [`_Alignof`](<#/doc/language/alignof>)(desde C11) , [`typeof`](<#/doc/language/typeof_unqual>) ou [`typeof_unqual`](<#/doc/language/typeof_unqual>)(desde C23), delimita o operando.
  * Em um [cast explícito](<#/doc/language/cast>), delimita o type-id.
  * Em um [literal composto](<#/doc/language/compound_literal>), delimita o type-id. (desde C99)
  * Em uma [declaração](<#/doc/language/declarations>) ou um [type-id](<#/doc/language/compatible_type>), indica agrupamento.
  * Em um [declarador de função](<#/doc/language/function_declaration>) (em uma [declaração](<#/doc/language/declarations>) ou um [type-id](<#/doc/language/compatible_type>)), delimita a lista de parâmetros.
  * Em uma instrução [`if`](<#/doc/language/if>), [`switch`](<#/doc/language/switch>), [`while`](<#/doc/language/while>), [`do-while`](<#/doc/language/do>), ou [`for`](<#/doc/language/for>), delimita a cláusula de controle.
  * Em uma [definição de macro tipo função](<#/doc/preprocessor/replace>), delimita os parâmetros da macro.
  * Em uma [invocação de macro tipo função](<#/doc/preprocessor/replace>), delimita os argumentos da macro ou impede que vírgulas sejam interpretadas como separadores de argumentos.
  * Parte de um operador de pré-processamento `defined`, `__has_include`, `__has_embed` ou `__has_c_attribute`(desde C23).
  * Parte de uma [expressão de seleção genérica](<#/doc/language/generic>). (desde C11)
  * Em um especificador de tipo [`_Atomic`](<#/doc/language/atomic>), delimita o type-id. (desde C11)
  * Em uma [declaração de asserção estática](<#/doc/language/static_assert>), delimita os operandos. (desde C11)
  * Em um especificador [`_Alignas`](<#/doc/language/alignas>), delimita o operando. (desde C11)
  * Em um [atributo](<#/doc/language/attributes>), delimita os argumentos do atributo. (desde C23)
  * Em um nome de tipo inteiro bit-preciso (_BitInt(N)), delimita o tamanho. (desde C23)
  * Parte da substituição de [`__VA_OPT__`](<#/doc/preprocessor/replace>) em uma definição de macro variádica. (desde C23)
  * Em um parâmetro de pré-processador usado em [diretivas #embed](<#/doc/preprocessor/embed>) e expressões de pré-processamento __has_embed, delimita a cláusula de parâmetro do pré-processador. (desde C23)

### `;`

  * Indica o fim de

    

  * uma [instrução](<#/doc/language/statements>) (incluindo a init-statement de uma instrução for)
  * uma [declaração](<#/doc/language/declarations>) ou lista de declarações de struct

  * Separa a segunda e terceira cláusulas de uma [instrução for](<#/doc/language/for>).

### `:`

  * Parte do [operador condicional](<#/doc/language/operator_other>).
  * Parte da [declaração de rótulo](<#/doc/language/statements>).
  * Em uma [declaração de membro bit-field](<#/doc/language/bit_field>), introduz a largura.
  * Introduz uma [base de enum](<#/doc/language/enum>), que especifica o tipo subjacente da enum. (desde C23)
  * Em uma [associação genérica](<#/doc/language/generic>), delimita o type-id ou default e a expressão selecionada. (desde C11)

### `...`

  * Na [lista de parâmetros](<#/doc/language/function_declaration>) de um declarador de função, significa uma [função variádica](<#/doc/language/variadic>).
  * Em uma [definição de macro](<#/doc/preprocessor/replace>), significa uma macro variádica. (desde C99)

### `?`

  * Parte do [operador condicional](<#/doc/language/operator_other>).

### `::`

  * Em um [atributo](<#/doc/language/attributes>), indica o escopo do atributo. (desde C23)
  * Em um parâmetro prefixado de pré-processador (usado por [#embed](<#/doc/preprocessor/embed>) e __has_embed), indica o escopo. (desde C23)

### `.`

  * [Operador de acesso a membro](<#/doc/language/operator_member_access>).
  * Na [inicialização](<#/doc/language/initialization>), introduz um designador para um membro de struct/union. (desde C99)

### `->`

  * [Operador de acesso a membro](<#/doc/language/operator_member_access>).

### `~`

  * [Operador de complemento unário (também conhecido como operador bitwise not)](<#/doc/language/operator_arithmetic>).

### `!`

  * [Operador lógico not](<#/doc/language/operator_logical>).

### `+`

  * [Operador de mais unário](<#/doc/language/operator_arithmetic>).
  * [Operador de mais binário](<#/doc/language/operator_arithmetic>).

### `-`

  * [Operador de menos unário](<#/doc/language/operator_arithmetic>).
  * [Operador de menos binário](<#/doc/language/operator_arithmetic>).

### `*`

  * [Operador de indireção](<#/doc/language/operator_member_access>).
  * [Operador de multiplicação](<#/doc/language/operator_arithmetic>).
  * Operador de ponteiro em um [declarador](<#/doc/language/declarations>) ou em um [type-id](<#/doc/language/compatible_type>).
  * Marcador de posição para o comprimento de um declarador de array de tamanho variável em uma [declaração de função](<#/doc/language/function_declaration>). (desde C99)

### `/`

  * [Operador de divisão](<#/doc/language/operator_arithmetic>).

### `%`

  * [Operador de módulo](<#/doc/language/operator_arithmetic>).

### `^`

  * [Operador bitwise xor](<#/doc/language/operator_arithmetic>).

### `&`

  * [Operador address-of](<#/doc/language/operator_member_access>).
  * [Operador bitwise and](<#/doc/language/operator_arithmetic>).

### `|`

  * [Operador bitwise or](<#/doc/language/operator_arithmetic>).

### `=`

  * [Operador de atribuição simples](<#/doc/language/operator_assignment>).
  * Na [inicialização](<#/doc/language/initialization>), delimita o objeto e a lista de inicializadores.
  * Em uma [definição de enum](<#/doc/language/enum>), introduz o valor da constante de enumeração.

### `+=`

  * [Operador de atribuição composta](<#/doc/language/operator_assignment>).

### `-=`

  * [Operador de atribuição composta](<#/doc/language/operator_assignment>).

### `*=`

  * [Operador de atribuição composta](<#/doc/language/operator_assignment>).

### `/=`

  * [Operador de atribuição composta](<#/doc/language/operator_assignment>).

### `%=`

  * [Operador de atribuição composta](<#/doc/language/operator_assignment>).

### `^=`

  * [Operador de atribuição composta](<#/doc/language/operator_assignment>).

### `&=`

  * [Operador de atribuição composta](<#/doc/language/operator_assignment>).

### `|=`

  * [Operador de atribuição composta](<#/doc/language/operator_assignment>).

### `==`

  * [Operador de igualdade](<#/doc/language/operator_comparison>).

### `!=`

  * [Operador de desigualdade](<#/doc/language/operator_comparison>).

### `<`

  * [Operador menor que](<#/doc/language/operator_comparison>).
  * Introduz um nome de cabeçalho em

    

  * uma [diretiva #include](<#/doc/preprocessor/include>)
  * uma [expressão de pré-processamento __has_include](<#/doc/preprocessor/include>) (desde C23)
  * uma [diretiva #embed](<#/doc/preprocessor/embed>) (desde C23)
  * uma [expressão de pré-processamento __has_embed](<#/doc/preprocessor/embed>) (desde C23)
  * locais definidos pela implementação dentro de uma [diretiva `#pragma`](<#/doc/preprocessor/impl>)

### `>`

  * [Operador maior que](<#/doc/language/operator_comparison>).
  * Indica o fim de um nome de cabeçalho em

    

  * uma [diretiva #include](<#/doc/preprocessor/include>)
  * uma [expressão de pré-processamento __has_include](<#/doc/preprocessor/include>) (desde C23)
  * uma [diretiva #embed](<#/doc/preprocessor/embed>) (desde C23)
  * uma [expressão de pré-processamento __has_embed](<#/doc/preprocessor/embed>) (desde C23)
  * locais definidos pela implementação dentro de uma [diretiva `#pragma`](<#/doc/preprocessor/impl>)

### `<=`

  * [Operador menor ou igual a](<#/doc/language/operator_comparison>).

### `>=`

  * [Operador maior ou igual a](<#/doc/language/operator_comparison>).

### `&&`

  * [Operador lógico and](<#/doc/language/operator_logical>).

### `||`

  * [Operador lógico or](<#/doc/language/operator_logical>).

### `<<`

  * [Operador de deslocamento de bits](<#/doc/language/operator_arithmetic>).

### `>>`

  * [Operador de deslocamento de bits](<#/doc/language/operator_arithmetic>).

### `<<=`

  * [Operador de atribuição composta](<#/doc/language/operator_assignment>).

### `>>=`

  * [Operador de atribuição composta](<#/doc/language/operator_assignment>).

### `++`

  * [Operador de incremento](<#/doc/language/operator_incdec>).

### `--`

  * [Operador de decremento](<#/doc/language/operator_incdec>).

### `,`

  * [Operador vírgula](<#/doc/language/operator_other>).
  * Separador de lista em

    

  * a lista de declaradores em uma [declaração](<#/doc/language/declarations>)
  * lista de inicializadores na [inicialização](<#/doc/language/initialization>), incluindo [literais compostos](<#/doc/language/compound_literal>)(desde C99)
  * a lista de argumentos em uma [expressão de chamada de função](<#/doc/language/operator_other>)
  * a lista de enumeradores em uma declaração de [enum](<#/doc/language/enum>)
  * uma lista de parâmetros de função
  * a lista de parâmetros de macro em uma [definição de macro tipo função](<#/doc/preprocessor/replace>)
  * a lista de argumentos de macro em uma [invocação de macro tipo função](<#/doc/preprocessor/replace>), a menos que encontrada entre um conjunto interno de parênteses
  * a lista de associação genérica em uma [expressão de seleção genérica](<#/doc/language/generic>) (desde C11)
  * uma lista de [atributos](<#/doc/language/attributes>) (desde C23)

  * Em uma [declaração de asserção estática](<#/doc/language/static_assert>), separa os argumentos. (desde C11)
  * Em uma [expressão de seleção genérica](<#/doc/language/generic>), separa a expressão de controle e a lista de associação genérica. (desde C11)

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 6.4.6 Pontuadores (p: 68-69)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 6.4.6 Pontuadores (p: 52-53)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 6.4.6 Pontuadores (p: 72-73)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 6.4.6 Pontuadores (p: 63-64)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 3.1.6 Pontuadores

### Veja também

[ Representações alternativas](<#/doc/language/operator_alternative>) (C95) | grafias alternativas para certos operadores
[Documentação C++](<#/>) para Pontuação