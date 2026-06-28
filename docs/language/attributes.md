# Sequência de especificadores de atributo (desde C23)

Introduz atributos definidos pela implementação para tipos, objetos, expressões, etc.

### Sintaxe

    `[[` attr ﻿`]]` `[[` attr1, attr2, attr3`(` args`)`]]` `[[` attribute-prefix`::` attr ﻿`(` args`)`]]`

Formalmente, a sintaxe é

---
`[[` lista-de-atributos `]]` | | (desde C23)

onde lista-de-atributos é uma sequência separada por vírgulas de zero ou mais tokens-de-atributo

---
atributo-padrão | (1) |
prefixo-de-atributo `::` identificador | (2) |
atributo-padrão `(` lista-de-argumentos ﻿(opcional) `)` | (3) |
prefixo-de-atributo `::` identificador `(` lista-de-argumentos ﻿(opcional) `)` | (4) |

onde prefixo-de-atributo é um identificador e lista-de-argumentos é uma sequência de tokens onde parênteses, colchetes e chaves são balanceados (sequência-de-tokens-balanceada).

1) atributo padrão, como [[fallthrough]]

2) atributo com um namespace, como [[gnu::unused]]

3) atributo padrão com argumentos, como [[deprecated("reason")]]

4) atributo com um namespace e uma lista de argumentos, como [[gnu::nonnull(1)]]

### Explicação

Atributos fornecem a sintaxe padrão unificada para extensões de linguagem definidas pela implementação, como as extensões de linguagem GNU e IBM `__attribute__((...))`, a extensão Microsoft `__declspec()`, etc.

Um atributo pode ser usado em quase todos os lugares no programa C, e pode ser aplicado a quase tudo: a tipos, a variáveis, a funções, a nomes, a blocos de código, a unidades de tradução inteiras, embora cada atributo particular seja válido apenas onde é permitido pela implementação: `[[expect_true]]` poderia ser um atributo que só pode ser usado com um if, e não com uma declaração de class. `[[omp::parallel()]]` poderia ser um atributo que se aplica a um bloco de código ou a um loop for, mas não ao tipo `int`, etc. (note que estes dois atributos são exemplos fictícios, veja abaixo os atributos padrão e alguns não-padrão)

Em declarações, atributos podem aparecer tanto antes da declaração completa quanto diretamente após o nome da entidade que é declarada, caso em que são combinados. Na maioria das outras situações, atributos se aplicam à entidade diretamente precedente.

Dois tokens de colchete esquerdo consecutivos (`[[`) só podem aparecer ao introduzir um especificador de atributo ou dentro de um argumento de atributo.

Além dos atributos padrão listados abaixo, as implementações podem suportar atributos não-padrão arbitrários com comportamento definido pela implementação. Todos os atributos desconhecidos por uma implementação são ignorados sem causar um erro.

Cada atributo-padrão é reservado para padronização. Ou seja, cada atributo não-padrão é prefixado por um prefixo-de-atributo fornecido pela implementação, por exemplo, `[[gnu::may_alias]]` e `[[clang::no_sanitize]]`.

### Atributos padrão

Apenas os seguintes atributos são definidos pelo padrão C. Cada atributo padrão cujo nome é da forma `attr` também pode ser escrito como `__attr__` e seu significado não é alterado.

`[[[deprecated](<#/doc/language/attributes/deprecated>)]]`(C23)
`[[[deprecated](<#/doc/language/attributes/deprecated>)("_reason_ ")]]`(C23) | indica que o uso do nome ou entidade declarada com este atributo é permitido, mas desencorajado por alguma razão
(especificador de atributo)
`[[[fallthrough](<#/doc/language/attributes/fallthrough>)]]`(C23) | indica que a passagem direta do rótulo case anterior é intencional e não deve ser diagnosticada por um compilador que avisa sobre passagens diretas
(especificador de atributo)
`[[[nodiscard](<#/doc/language/attributes/nodiscard>)]]`(C23)
`[[[nodiscard](<#/doc/language/attributes/nodiscard>)("_reason_ ")]]`(C23) | incentiva o compilador a emitir um aviso se o valor de retorno for descartado
(especificador de atributo)
`[[[maybe_unused](<#/doc/language/attributes/maybe_unused>)]]`(C23) | suprime avisos do compilador sobre entidades não utilizadas, se houver
(especificador de atributo)
`[[[noreturn](<#/doc/language/attributes/noreturn>)]]`(C23)
`[[[_Noreturn](<#/doc/language/attributes/noreturn>)]]`(C23)(deprecated) | indica que a função não retorna
(especificador de atributo)
`[[[unsequenced](<#/doc/language/attributes/reproducible>)]]`(C23) | indica que uma função é sem estado, sem efeitos, idempotente e independente
(especificador de atributo)
`[[[reproducible](<#/doc/language/attributes/reproducible>)]]`(C23) | indica que uma função é sem efeitos e idempotente
(especificador de atributo)

### Teste de atributos

---
`__has_c_attribute(` attribute-token `)`

Verifica a presença de um token de atributo nomeado por token-de-atributo.

Para atributos padrão, ele se expandirá para o ano e mês em que o atributo foi adicionado ao rascunho de trabalho (veja a tabela abaixo), a presença de atributos específicos do fornecedor é determinada por uma constante inteira não-zero.

`__has_c_attribute` pode ser expandido na expressão de [` #if`](<#/doc/preprocessor/conditional>) e [` #elif`](<#/doc/preprocessor/conditional>). É tratado como uma macro definida por [` #ifdef`](<#/doc/preprocessor/conditional>), [` #ifndef`](<#/doc/preprocessor/conditional>) e [`defined`](<#/doc/preprocessor/conditional>), mas não pode ser usado em nenhum outro lugar.

token-de-atributo | Atributo | Valor | Padrão
`deprecated` | `[[[deprecated](<#/doc/language/attributes/deprecated>)]]` | 201904L | (C23)
`fallthrough` | `[[[fallthrough](<#/doc/language/attributes/fallthrough>)]]` | 201904L | (C23)
`maybe_unused` | `[[[maybe_unused](<#/doc/language/attributes/maybe_unused>)]]` | 201904L | (C23)
`nodiscard` | `[[[nodiscard](<#/doc/language/attributes/nodiscard>)]]` | 202003L | (C23)
`noreturn`
`_Noreturn` | `[[[noreturn](<#/doc/language/attributes/noreturn>)]]`
`[[[_Noreturn](<#/doc/language/attributes/noreturn>)]]` | 202202L | (C23)
`unsequenced` | `[[[unsequenced](<#/doc/language/attributes/reproducible>)]]` | 202207L | (C23)
`reproducible` | `[[[reproducible](<#/doc/language/attributes/reproducible>)]]` | 202207L | (C23)

### Exemplo

Execute este código
```c
    [[gnu::hot]] [[gnu::const]] [[nodiscard]]
    int f(void); // declare f with three attributes
    
    [[gnu::const, gnu::hot, nodiscard]]
    int f(void); // the same as above, but uses a single attr
                 // specifier that contains three attributes
    
    int f(void) { return 0; }
    
    int main(void)
    {
    }
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

  * 6.7.12 Atributos (p: TBD)

### Veja também

[Documentação C++](<#/>) para Sequência de especificadores de atributo
---

### Links externos

1. | [Atributos no GCC](<https://gcc.gnu.org/onlinedocs/gcc/Attribute-Syntax.html#Attribute-Syntax>)
2. | [Atributos no Clang](<https://clang.llvm.org/docs/AttributeReference.html>)