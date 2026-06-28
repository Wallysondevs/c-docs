# Suporte a compiladores C

| Esta página é mantida com o melhor esforço e pode estar desatualizada em relação às versões mais recentes dos compiladores. Se você notar algo desatualizado, por favor, ajude-nos a atualizá-la!

## Recursos do C23

Note que esta lista pode mudar, à medida que o rascunho do padrão C23/2x evolui.

### Recursos da linguagem C23 (core)

| Esta seção está incompleta
Razão: status para Apple Clang e outros compiladores que suportam C2x
Recurso C23

| Documento(s)

| GCC | Clang | MSVC | Apple Clang | EDG eccp | Intel C++ | Nvidia HPC C++ (ex PGI)* | Nvidia nvcc | Cray |
[`static_assert`](<#/doc/language/static_assert>) sem mensagem | [N2265](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2265.pdf>) | 9 | 9 | Yes | Yes | 6.5 | 2021.1.2 (clang based)
`[[[nodiscard](<#/doc/language/attributes/nodiscard>)]]` | [N2267](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2267.pdf>) | 10 | 9 | | Yes | 6.4 | 2021.1.2 (clang based)
`[[[maybe_unused](<#/doc/language/attributes/maybe_unused>)]]` | [N2270](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2270.pdf>) | 10 | 9 | | Yes | 6.4 | 2021.1.2 (clang based)
`[[[deprecated](<#/doc/language/attributes/deprecated>)]]` | [N2334](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2334.pdf>) | 10 | 9 | | Yes | 6.4 | 2021.1.2 (clang based)
[Atributos](<#/doc/language/attributes>) | [N2335](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2335.pdf>)
[N2554](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2554.pdf>) | 10 | 9 | | Yes | 6.4 | 2021.1.2 (clang based)
Tipos de ponto flutuante decimal IEEE 754 | [N2341](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2341.pdf>) | 4.2 (partial)*
12 | | | | | 13.0 (partial)*
`[[[fallthrough](<#/doc/language/attributes/fallthrough>)]]` | [N2408](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2408.pdf>) | 10 | 9 | | Yes | 6.4 | 2021.1.2 (clang based)
[Constantes de caractere `u8`](<#/doc/language/character_constant>) | [N2418](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2418.pdf>) | 10 | 15 | | | 6.5 | 2022.2
Remoção de [definições de função](<#/doc/language/function_definition>) sem protótipo | [N2432](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2432.pdf>) | 10 | 15 | | | | 2022.2
`[[[nodiscard](<#/doc/language/attributes/nodiscard>)]]` com mensagem | [N2448](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2448.pdf>) | 11 | 10 | | Yes | 6.4 | 2021.1.2 (clang based)
Parâmetros sem nome em definições de função | [N2480](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2480.pdf>) | 11 | 11 | | Yes | 6.4 | 2021.1.2 (clang based)
[Rótulos](<#/doc/language/statements>) antes de declarações e fim de blocos | [N2508](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2508.pdf>) | 11 | 16 | Partial* | | 6.5 | 17.0*
[Constantes inteiras binárias](<#/doc/language/integer_constant>) | [N2549](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2549.pdf>) | 4.3*
11 | 2.9*
9 | 19.0 (2015)** | Yes | 6.5 | 11.0*
[`__has_c_attribute`](<#/doc/language/attributes>) em condicionais do pré-processador | [N2553](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2553.pdf>) | 11 | 9 | | Yes | 6.5 | 2021.1.2 (clang based)
Permitir atributos duplicados | [N2557](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2557.pdf>) | 11 | 13 | | Yes | 6.5 | 2021.4 (clang-based
Tipos de intercâmbio e estendidos IEEE 754 | [N2601](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2601.pdf>) | 7 (partial)*
14 | 6 (partial)* | | Partial*
Separadores de dígitos | [N2626](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2626.pdf>) | 12 | 13 | 19.0 (2015)** | Yes | 6.5 | 18.0*
[`#elifdef` e `#elifndef`](<#/doc/preprocessor/conditional>) | [N2645](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2645.pdf>) | 12 | 13 | 19.40* | 13.1.6* | 6.5 | 2021.4
Mudança de tipo de [literais de string `u8`](<#/doc/language/string_literal>) | [N2653](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2653.htm>) | 13
`[[[maybe_unused](<#/doc/language/attributes/maybe_unused>)]]` para rótulos | [N2662](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2662.pdf>) | 11 | 16 | | | 6.5 | 2022.2
[` #warning`](<#/doc/preprocessor/error>) | [N2686](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2686.pdf>) | Yes | Yes | | Yes | 6.5 | Yes
Tipos inteiros de precisão de bit (_BitInt) | [N2763](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2763.pdf>) | 14 (partial)* | 15 | | | 6.5 | 2022.2
`[[[noreturn](<#/doc/language/attributes/noreturn>)]]` | [N2764](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2764.pdf>) | 13 | 15 | | | 6.5 | 2022.2
Sufixos para constantes inteiras de precisão de bit | [N2775](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2775.pdf>) | 14 | 15 | | | | 2022.2
[`__has_include`](<#/doc/preprocessor/include>) em condicionais do pré-processador | [N2799](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2799.pdf>) | 5 | Yes | 19.11* | Yes | 6.5 | 18.0
Sintaxe de Identificador usando o Anexo 31 do Padrão Unicode | [N2836](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2836.pdf>) | 13 | 15 | | | 6.5 | 2022.2
Remoção de [declarações de função](<#/doc/language/function_declaration>) sem protótipo | [N2841](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2841.htm>) | 13 | 15 | | | | 2022.2
[Inicializadores vazios](<#/doc/language/initialization>) | [N2900](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2900.htm>) | Partial*
13 | Partial* | | Partial* | Partial* | Partial*
[`typeof`](<#/doc/language/typeof_unqual>) e [`typeof_unqual`](<#/doc/language/typeof_unqual>) | [N2927](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2927.htm>)
[N2930](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2930.pdf>) | Partial*
13 | Partial*
16 | 19.39* | Partial* | Partial* | Partial* | | | Partial*
Nova grafia de palavras-chave | [N2934](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2934.pdf>) | 13 | 16 | | | 6.5
[true e false predefinidos](<#/doc/language/bool_constant>) | [N2935](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2935.pdf>) | 13 | 15 | | | | 2022.2
`[[[unsequenced](<#/doc/language/attributes/reproducible>)]]` e `[[[reproducible](<#/doc/language/attributes/reproducible>)]]` | [N2956](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2956.htm>) | 15
Relaxar requisitos para [lista de parâmetros variádicos](<#/doc/language/variadic>) | [N2975](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2975.pdf>) | 13 | 16 | | | 6.5 | 2023.1
Inferência de tipo em definições de objeto | [N3007](<https://open-std.org/JTC1/SC22/WG14/www/docs/n3007.htm>) | 13 | 18
[` #embed`](<#/doc/preprocessor/embed>) | [N3017](<https://open-std.org/JTC1/SC22/WG14/www/docs/n3017.htm>) | 15 | 19
[Objetos `constexpr`](<#/doc/language/constexpr>) | [N3018](<https://open-std.org/JTC1/SC22/WG14/www/docs/n3018.htm>) | 13 | 19
Enumerações Normais Aprimoradas | [N3029](<https://open-std.org/JTC1/SC22/WG14/www/docs/n3029.htm>) | 13 | 20*
Enumerações com tipos subjacentes fixos | [N3030](<https://open-std.org/JTC1/SC22/WG14/www/docs/n3030.htm>) | 13 | 20*
[`__VA_OPT__`](<#/doc/preprocessor/replace>) | [N3033](<https://open-std.org/JTC1/SC22/WG14/www/docs/n3033.htm>) | 8
13 | 12 | 19.39* | | 6.5
Especificadores de classe de armazenamento para literais compostos | [N3038](<https://open-std.org/JTC1/SC22/WG14/www/docs/n3038.htm>) | 13
[`nullptr`](<#/doc/language/nullptr>) | [N3042](<https://open-std.org/JTC1/SC22/WG14/www/docs/n3042.htm>) | 13 | 16

Recurso C23 |

Documento(s) | GCC | Clang | MSVC | Apple Clang | EDG eccp | Intel C++ | Nvidia HPC C++ (ex PGI)* | Nvidia nvcc | Cray

### Recursos da biblioteca C23

| Esta seção está incompleta
Razão: uma lista diferente para bibliotecas padrão C

## Recursos do C99

### Recursos da linguagem C99 (core)

| Esta seção está incompleta
Razão: precisa listar compiladores C, verificação
Recurso C99

| Documento(s)

| GCC | Clang | MSVC | Apple Clang | EDG eccp | Intel C++ | Nvidia HPC C++ (ex PGI)* | Nvidia nvcc | Cray |
Nomes de caracteres universais em [identificadores](<#/doc/language/identifier>) | | 3.1 | Yes | Yes
[Limites de tradução aumentados](<#/doc/language/identifier>) | [N590](<https://open-std.org/JTC1/SC22/WG14/www/docs/n590.pdf>) | 0.9 | N/A
[Comentários `//`](<#/doc/comment>) | [N644](<https://open-std.org/JTC1/SC22/WG14/www/docs/n644.htm>) | 2.7 | Yes | Yes
[Ponteiros `restrict`](<#/doc/language/restrict>) | [N448](<https://open-std.org/JTC1/SC22/WG14/www/docs/n448.pdf>) | 2.95 | Yes | partial*
[Tipos aritméticos aprimorados](<#/doc/language/arithmetic_types>) | [N815](<https://open-std.org/JTC1/SC22/WG14/www/docs/n815.htm>)
[N601](<https://open-std.org/JTC1/SC22/WG14/www/docs/n601.ps>)
[N620](<https://open-std.org/JTC1/SC22/WG14/www/docs/n620.ps>)
[N638](<https://open-std.org/JTC1/SC22/WG14/www/docs/n638.ps>)
[N657](<https://open-std.org/JTC1/SC22/WG14/www/docs/n657.ps>)
[N694](<https://open-std.org/JTC1/SC22/WG14/www/docs/n694.ps>)
[N809](<https://open-std.org/JTC1/SC22/WG14/www/docs/n809.ps>) | Yes | partial | Maybe
Membros de array flexíveis | | 3.0 | Yes | Yes
[Tipos de array de tamanho variável (VLA)](<#/doc/language/array>) | [N683](<https://open-std.org/JTC1/SC22/WG14/www/docs/n683.htm>) | 0.9 | Yes
Tipos variably-modified (VM) | [N2778](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2778.pdf>) | N/A | Yes
Inicializadores designados | [N494](<https://open-std.org/JTC1/SC22/WG14/www/docs/n494.pdf>) | 3.0 | Yes | Yes
Inicializadores não constantes | | 1.21 | N/A
Qualificadores cvr idempotentes | [N505](<https://open-std.org/JTC1/SC22/WG14/www/docs/n505.pdf>) | 3.0 | N/A
Vírgula final em [enumerator-list](<#/doc/language/enum>) | | 0.9 | Yes | Yes
[Constantes de ponto flutuante hexadecimais](<#/doc/language/floating_constant>) | [N308](<https://open-std.org/JTC1/SC22/WG14/www/docs/n308.pdf>) | 2.8 | Yes | Yes
[Literais compostos](<#/doc/language/compound_literal>) | [N716](<https://open-std.org/JTC1/SC22/WG14/www/docs/n716.htm>) | 3.1 | Yes | Yes
Ambiente de ponto flutuante | | partial | partial
Exigindo truncamento para divisões de tipos inteiros com sinal | [N617](<https://open-std.org/JTC1/SC22/WG14/www/docs/n617.htm>) | 0.9 | N/A
Retorno implícito 0; na [função `main()`](<#/doc/language/main_function>) | | Yes | Yes | Yes
Declarações e instruções em ordem mista | [N740](<https://open-std.org/JTC1/SC22/WG14/www/docs/n740.htm>) | 3.0 | Yes | Yes
`init-statement` em laços [`for`](<#/doc/language/for>) | | Yes | Yes | Yes
[Funções `inline`](<#/doc/language/inline>) | [N741](<https://open-std.org/JTC1/SC22/WG14/www/docs/n741.htm>) | 4.3 | Yes | Yes
Variável predefinida [`__func__`](<#/doc/language/function_definition>) | [N611](<https://open-std.org/JTC1/SC22/WG14/www/docs/n611.ps>) | 2.95 | Yes | Yes
Qualificadores cvr e static em [] dentro de declarações de função | | 3.1 | Yes
[Macros variádicas](<#/doc/preprocessor/replace>) | [N707](<https://open-std.org/JTC1/SC22/WG14/www/docs/n707.htm>) | 2.95 | Yes | Yes
Operador de pré-processador [`_Pragma`](<#/doc/preprocessor/impl>) | [N634](<https://open-std.org/JTC1/SC22/WG14/www/docs/n634.ps>) | 3.0 | Yes | partial*
Pragmas padrão para avaliação de ponto flutuante | [N631](<https://open-std.org/JTC1/SC22/WG14/www/docs/n631.htm>)
[N696](<https://open-std.org/JTC1/SC22/WG14/www/docs/n696.ps>) | No | No

Recurso C99 |

Documento(s) | GCC | Clang | MSVC | Apple Clang | EDG eccp | Intel C++ | Nvidia HPC C++ (ex PGI)* | Nvidia nvcc | Cray

### Veja também

[documentação C++](<#/>) para suporte a compiladores
---