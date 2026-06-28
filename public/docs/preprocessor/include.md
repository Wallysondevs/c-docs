# Inclusão de arquivo fonte

Inclui outro arquivo fonte no arquivo fonte atual na linha imediatamente após a diretiva.

### Sintaxe

---
`#include <` h-char-sequence `>` new-line | (1) |
`#include "` q-char-sequence `"` new-line | (2) |
`#include` pp-tokens new-line | (3) |
`__has_include` `(` `"` q-char-sequence `"` `)`
`__has_include` `(` `<` h-char-sequence `>` `)` | (4) | (desde C23)
`__has_include` `(` string-literal `)`
`__has_include` `(` `<` h-pp-tokens `>` `)` | (5) | (desde C23)

1) Procura por um cabeçalho identificado unicamente por h-char-sequence e substitui a diretiva por todo o conteúdo do cabeçalho.

2) Procura por um arquivo fonte identificado por q-char-sequence e substitui a diretiva por todo o conteúdo do arquivo fonte. Pode recorrer a (1) e tratar q-char-sequence como um identificador de cabeçalho.

3) Se nem (1) nem (2) for correspondido, pp-tokens passará por substituição de macro. A diretiva após a substituição será tentada a corresponder com (1) ou (2) novamente.

4) Verifica se um cabeçalho ou arquivo fonte está disponível para inclusão.

5) Se (4) não for correspondido, h-pp-tokens passará por substituição de macro. A diretiva após a substituição será tentada a corresponder com (4) novamente.

- **new-line** — O caractere de nova linha
- **h-char-sequence** — Uma sequência de um ou mais h-chars, onde a aparição de qualquer um dos seguintes causa comportamento indefinido:

  * o caractere '
  * o caractere "
  * o caractere \
  * a sequência de caracteres //
  * a sequência de caracteres /*

- **h-char** — Qualquer membro do [conjunto de caracteres fonte](<#/doc/language/translation_phases>) exceto new-line e >
- **q-char-sequence** — Uma sequência de um ou mais q-chars, onde a aparição de qualquer um dos seguintes causa comportamento indefinido:

  * o caractere '
  * o caractere \
  * a sequência de caracteres //
  * a sequência de caracteres /*

- **q-char** — Qualquer membro do [conjunto de caracteres fonte](<#/doc/language/translation_phases>) exceto new-line e "
- **pp-tokens** — Uma sequência de um ou mais [tokens de pré-processamento](<#/doc/language/translation_phases>)
- **string-literal** — Um [literal de string](<#/doc/language/string_literal>)
- **h-pp-tokens** — Uma sequência de um ou mais [tokens de pré-processamento](<#/doc/language/translation_phases>) exceto >

### Explicação

1) Procura pelo arquivo identificado por h-char-sequence de maneira definida pela implementação. A intenção desta sintaxe é procurar por arquivos sob o controle da implementação. Implementações típicas procuram apenas em diretórios de inclusão padrão. A biblioteca padrão C é implicitamente incluída nesses diretórios de inclusão padrão. Os diretórios de inclusão padrão geralmente podem ser controlados pelo usuário através de opções do compilador.

2) Procura pelo arquivo identificado por q-char-sequence de maneira definida pela implementação. A intenção desta sintaxe é procurar por arquivos que não são controlados pela implementação. Implementações típicas primeiro procuram no diretório onde o arquivo atual reside e, somente se o arquivo não for encontrado, procuram nos diretórios de inclusão padrão como em (1).

3) Os tokens de pré-processamento após `include` na diretiva são processados assim como em texto normal (ou seja, cada identificador atualmente definido como um nome de macro é substituído por sua lista de substituição de tokens de pré-processamento). A diretiva resultante após todas as substituições deve corresponder a uma das duas formas anteriores. O método pelo qual uma sequência de tokens de pré-processamento entre um par de tokens de pré-processamento < e > ou um par de caracteres " é combinada em um único token de pré-processamento de nome de cabeçalho é definido pela implementação.

4) O cabeçalho ou arquivo fonte identificado por h-char-sequence ou q-char-sequence é procurado como se essa sequência de tokens de pré-processamento fosse os pp-tokens na sintaxe (3), exceto que nenhuma expansão de macro adicional é realizada. Se tal diretiva não satisfizer os requisitos sintáticos de uma diretiva #include, o programa estará malformado. A expressão `__has_include` avalia para 1 se a busca pelo arquivo fonte for bem-sucedida, e para 0 se a busca falhar.

5) Esta forma é considerada apenas se a sintaxe (4) não corresponder, caso em que os tokens de pré-processamento são processados assim como em texto normal.

No caso de o arquivo não ser encontrado, o programa estará malformado.

`__has_include` pode ser expandido na expressão de [` #if`](<#/doc/preprocessor/conditional>) e [` #elif`](<#/doc/preprocessor/conditional>). É tratado como uma macro definida por [` #ifdef`](<#/doc/preprocessor/conditional>), [` #ifndef`](<#/doc/preprocessor/conditional>), [` #elifdef`](<#/doc/preprocessor/conditional>), [` #elifndef`](<#/doc/preprocessor/conditional>) e [`defined`](<#/doc/preprocessor/conditional>), mas não pode ser usado em nenhum outro lugar. | (desde C23)

### Notas

Implementações típicas procuram apenas em diretórios de inclusão padrão para a sintaxe (1). A biblioteca padrão C é implicitamente incluída nesses diretórios de inclusão padrão. Os diretórios de inclusão padrão geralmente podem ser controlados pelo usuário através de opções do compilador.

A intenção da sintaxe (2) é procurar por arquivos que não são controlados pela implementação. Implementações típicas primeiro procuram no diretório onde o arquivo atual reside e depois recorrem a (1).

Quando um arquivo é incluído, ele é processado pelas [fases de tradução](<#/doc/language/translation_phases>) 1-4, o que pode incluir, recursivamente, a expansão de diretivas `#include` aninhadas, até um limite de aninhamento definido pela implementação. Para evitar a inclusão repetida do mesmo arquivo e recursão infinita quando um arquivo se inclui, talvez transitivamente, _guardas de cabeçalho_ são comumente usadas: o cabeçalho inteiro é envolvido em
```c
    #ifndef FOO_H_INCLUDED /* any name uniquely mapped to file name */
    #define FOO_H_INCLUDED
    // contents of the file are here
    #endif
```

Muitos compiladores também implementam o [pragma](<#/doc/preprocessor/impl>) não padrão #pragma once com efeitos semelhantes: ele desabilita o processamento de um arquivo se o mesmo arquivo (onde a identidade do arquivo é determinada de forma específica do SO) já tiver sido incluído.

Um resultado de 1 para `__has_include` significa apenas que um cabeçalho ou arquivo fonte com o nome especificado existe. Não significa que o cabeçalho ou arquivo fonte, quando incluído, não causaria um erro ou conteria algo útil.

### Exemplo

| Esta seção está incompleta
Razão: nenhum exemplo

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 6.4.7 Nomes de cabeçalho (p: 69)

    

  * 6.10.1 Inclusão condicional (p: 165-169)

    

  * 6.10.2 Inclusão de arquivo fonte (p: 169-170)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 6.10.2 Inclusão de arquivo fonte (p: 119-120)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 6.10.2 Inclusão de arquivo fonte (p: 164-166)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 6.10.2 Inclusão de arquivo fonte (p: 149-151)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 3.8.2 Inclusão de arquivo fonte

### Veja também

[Uma lista de arquivos de cabeçalho da Biblioteca Padrão C](<#/doc/header>)
---
[Documentação C++](<#/>) para Inclusão de arquivo fonte