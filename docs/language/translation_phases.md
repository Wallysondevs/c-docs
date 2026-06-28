# Fases de tradução

O arquivo fonte C é processado pelo compilador _como se_ as seguintes fases ocorressem, nesta ordem exata. A implementação real pode combinar essas ações ou processá-las de forma diferente, desde que o comportamento seja o mesmo.

### Fase 1

1) Os bytes individuais do arquivo de código fonte (que geralmente é um arquivo de texto em alguma codificação multibyte, como UTF-8) são mapeados, de maneira definida pela implementação, para os caracteres do _conjunto de caracteres fonte_. Em particular, os indicadores de fim de linha dependentes do sistema operacional são substituídos por caracteres de nova linha.

    O _conjunto de caracteres fonte_ é um conjunto de caracteres multibyte que inclui o _conjunto de caracteres fonte básico_ como um subconjunto de byte único, consistindo dos seguintes 96 caracteres:

a) 5 caracteres de espaço em branco (espaço, tabulação horizontal, tabulação vertical, avanço de página, nova linha)

b) 10 caracteres de dígito de '0' a '9'

c) 52 letras de 'a' a 'z' e de 'A' a 'Z'

d) 29 caracteres de pontuação: _ { } [ ] # ( ) < > % : ; . ? * + - / ^ & | ~ ! = , \ " '

2) [Sequências de trigrafos](<#/doc/language/operator_alternative>) são substituídas por representações de caractere único correspondentes.(ate C23)

### Fase 2

1) Sempre que uma barra invertida aparece no final de uma linha (imediatamente seguida pelo caractere de nova linha), tanto a barra invertida quanto a nova linha são excluídas, combinando duas linhas físicas de código fonte em uma linha lógica de código fonte. Esta é uma operação de passagem única: uma linha terminada em duas barras invertidas seguida por uma linha vazia não combina três linhas em uma.

Execute este código
```c
    #include <stdio.h>
     
    #define PUTS p\
    u\
    t\
    s
    /* A junção de linhas está na fase 2, enquanto as macros
     * são tokenizadas na fase 3 e expandidas na fase 4,
     * então o acima é equivalente a #define PUTS puts
     */
     
    int main(void)
    {
     /* Use a junção de linhas para chamar puts */ PUT\
    S\
    ("Output ends here\\
    0Not printed" /* Após a junção de linhas, a barra invertida restante
                   * escapa o 0, terminando a string prematuramente.
                   */
    );
    }
```

2) Se um arquivo fonte não vazio não terminar com um caractere de nova linha após esta etapa (seja porque não tinha nova linha originalmente, ou porque terminou com uma barra invertida), o comportamento é indefinido.

### Fase 3

1) O arquivo fonte é decomposto em [comentários](<#/doc/comment>), sequências de caracteres de espaço em branco (espaço, tabulação horizontal, nova linha, tabulação vertical e avanço de página) e _tokens de pré-processamento_, que são os seguintes

a) nomes de cabeçalho: <stdio.h> ou "myfile.h"

b) [identificadores](<#/doc/language/identifier>)

c) números de pré-processamento, que abrangem [constantes inteiras](<#/doc/language/integer_constant>) e [constantes de ponto flutuante](<#/doc/language/floating_constant>), mas também cobrem alguns tokens inválidos como 1..E+3.foo ou 0JBK

d) [constantes de caractere](<#/doc/language/character_constant>) e [literais de string](<#/doc/language/string_literal>)

e) operadores e pontuadores, como +, <<=, <%, ou ##.

f) caracteres individuais não-espaço em branco que não se encaixam em nenhuma outra categoria

2) Cada comentário é substituído por um caractere de espaço

3) Novas linhas são mantidas, e é definido pela implementação se sequências de espaço em branco que não são novas linhas podem ser colapsadas em caracteres de espaço único.

Se a entrada foi analisada em tokens de pré-processamento até um determinado caractere, o próximo token de pré-processamento é geralmente considerado a sequência mais longa de caracteres que poderia constituir um token de pré-processamento, mesmo que isso causasse falha na análise subsequente. Isso é comumente conhecido como _maximal munch_.
```c
    int foo = 1;
    // int bar = 0xE+foo; // erro: número de pré-processamento inválido 0xE+foo
    int bar = 0xE/*Comentário de salvamento*/+foo; // OK: 0xE + foo
    int baz = 0xE + foo; // OK: 0xE + foo
    int pub = bar+++baz; // OK: bar++ + baz
    int ham = bar++-++baz; // OK: bar++ - ++baz
    // int qux = bar+++++baz; // erro: bar++ ++ +baz, não bar++ + ++baz
    int qux = bar+++/*Comentário de salvamento*/++baz; // OK: bar++ + ++baz
```

A única exceção à regra do maximal munch é:

  * Tokens de pré-processamento de nome de cabeçalho são formados apenas dentro de uma diretiva [` #include`](<#/doc/preprocessor/include>) ou [` #embed`](<#/doc/preprocessor/embed>)(desde C23), em expressões [`__has_include`](<#/doc/preprocessor/include>) e [`__has_embed`](<#/doc/preprocessor/embed>)(desde C23) e em locais definidos pela implementação dentro de uma diretiva [` #pragma`](<#/doc/preprocessor/impl>).

```c
    #define MACRO_1 1
    #define MACRO_2 2
    #define MACRO_3 3
    #define MACRO_EXPR (MACRO_1 <MACRO_2> MACRO_3) // OK: <MACRO_2> não é um nome de cabeçalho
```

### Fase 4

1) [O pré-processador](<#/doc/preprocessor>) é executado.

2) Cada arquivo introduzido com a diretiva [#include](<#/doc/preprocessor/include>) passa pelas fases 1 a 4, recursivamente.

3) Ao final desta fase, todas as diretivas de pré-processador são removidas do código fonte.

### Fase 5

1) Todos os caracteres e [sequências de escape](<#/doc/language/escape>) em [constantes de caractere](<#/doc/language/character_constant>) e [literais de string](<#/doc/language/string_literal>) são convertidos do _conjunto de caracteres fonte_ para o _conjunto de caracteres de execução_ (que pode ser um conjunto de caracteres multibyte como UTF-8, desde que todos os 96 caracteres do _conjunto de caracteres fonte básico_ listados na fase 1 tenham representações de byte único). Se o caractere especificado por uma sequência de escape não for um membro do conjunto de caracteres de execução, o resultado é definido pela implementação, mas é garantido que não seja um caractere nulo (largo).

Nota: a conversão realizada nesta etapa pode ser controlada por opções de linha de comando em algumas implementações: gcc e clang usam -finput-charset para especificar a codificação do conjunto de caracteres fonte, -fexec-charset e -fwide-exec-charset para especificar as codificações do conjunto de caracteres de execução nos literais de string e constantes de caractere que não possuem um prefixo de codificação(desde C11).

### Fase 6

[Literais de string](<#/doc/language/string_literal>) adjacentes são concatenados.

### Fase 7

A compilação ocorre: os tokens são analisados sintaticamente e semanticamente e traduzidos como uma unidade de tradução.

### Fase 8

A ligação ocorre: Unidades de tradução e componentes de biblioteca necessários para satisfazer referências externas são coletados em uma imagem de programa que contém as informações necessárias para a execução em seu ambiente de execução (o SO).

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 5.1.1.2 Fases de tradução (p: TBD)

    

  * 5.2.1 Conjuntos de caracteres (p: TBD)

    

  * 6.4 Elementos lexicais (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 5.1.1.2 Fases de tradução (p: 9-10)

    

  * 5.2.1 Conjuntos de caracteres (p: 17)

    

  * 6.4 Elementos lexicais (p: 41-54)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 5.1.1.2 Fases de tradução (p: 10-11)

    

  * 5.2.1 Conjuntos de caracteres (p: 22-24)

    

  * 6.4 Elementos lexicais (p: 57-75)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 5.1.1.2 Fases de tradução (p: 9-10)

    

  * 5.2.1 Conjuntos de caracteres (p: 17-19)

    

  * 6.4 Elementos lexicais (p: 49-66)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 2.1.1.2 Fases de tradução

    

  * 2.2.1 Conjuntos de caracteres

    

  * 3.1 Elementos lexicais

### Veja também

[Documentação C++](<#/>) para Fases de tradução
---