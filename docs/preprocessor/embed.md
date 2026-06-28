# Inclusão de recurso binário (desde C23)

#embed é uma diretiva de pré-processador para incluir recursos (binários) na compilação, onde um recurso é definido como uma fonte de dados acessível a partir do ambiente de tradução.

### Sintaxe

---
`#embed <` h-char-sequence `>` embed-parameter-sequence ﻿(optional) new-line | (1) |
`#embed "` q-char-sequence `"` embed-parameter-sequence ﻿(optional) new-line | (2) |
`#embed` pp-tokens new-line | (3) |
`__has_embed` `(` `"` q-char-sequence `"` embed-parameter-sequence ﻿(optional) `)`
`__has_embed` `(` `<` h-char-sequence `>` embed-parameter-sequence ﻿(optional) `)` | (4) |
`__has_embed` `(` string-literal pp-balanced-token-sequence ﻿(optional) `)`
`__has_embed` `(` `<` h-pp-tokens `>` pp-balanced-token-sequence ﻿(optional) `)` | (5) |

1) Procura por um recurso identificado unicamente por h-char-sequence e substitui a diretiva por uma lista de inteiros separados por vírgula correspondentes aos dados do recurso.

2) Procura por um recurso identificado por q-char-sequence e substitui a diretiva por uma lista de inteiros correspondentes aos dados do recurso. Pode recorrer a (1).

3) Se nem (1) nem (2) for correspondido, pp-tokens passará por substituição de macro. A diretiva após a substituição será tentada novamente para corresponder a (1) ou (2).

4) Verifica se um recurso está disponível para inclusão, se está vazio ou não e se os parâmetros passados são suportados pela implementação.

5) Se (4) não for correspondido, h-pp-tokens e pp-balanced-token-sequence passarão por substituição de macro. A diretiva após a substituição será tentada novamente para corresponder a (4).

- **new-line** — O caractere de nova linha
- **h-char-sequence** — Uma sequência de um ou mais h-chars, onde a aparição de qualquer um dos seguintes causa comportamento indefinido:

  * o caractere '
  * o caractere "
  * o caractere \
  * a sequência de caracteres //
  * a sequência de caracteres /*

- **h-char** — Qualquer membro do [conjunto de caracteres fonte](<#/doc/language/translation_phases>) exceto nova linha e >
- **q-char-sequence** — Uma sequência de um ou mais q-chars, onde a aparição de qualquer um dos seguintes causa comportamento indefinido:

  * o caractere '
  * o caractere \
  * a sequência de caracteres //
  * a sequência de caracteres /*

- **q-char** — Qualquer membro do [conjunto de caracteres fonte](<#/doc/language/translation_phases>) exceto nova linha e "
- **pp-tokens** — Uma sequência de um ou mais [tokens de pré-processamento](<#/doc/language/translation_phases>)
- **string-literal** — Um [literal de string](<#/doc/language/string_literal>)
- **h-pp-tokens** — Uma sequência de um ou mais [tokens de pré-processamento](<#/doc/language/translation_phases>) exceto >
- **embed-parameter-sequence** — Uma sequência de um ou mais pp-parameter s. Note que, ao contrário de uma lista de atributos, esta sequência não é separada por vírgulas.
- **pp-parameter** — Um attribute-token (veja: [atributos](<#/doc/language/attributes>)) mas composto por tokens de pré-processamento em vez de tokens.
- **pp-balanced-token-sequence** — Uma balanced-token-sequence (veja: [atributos](<#/doc/language/attributes>)) mas composta por tokens de pré-processamento em vez de tokens.

### Explicação

1) Procura pelo recurso identificado por h-char-sequence de maneira definida pela implementação.

2) Procura pelo recurso identificado por q-char-sequence de maneira definida pela implementação. Para (1,2), as implementações tipicamente usam um mecanismo similar, mas distinto, dos caminhos de busca definidos pela implementação usados para [inclusão de arquivo fonte](<#/doc/preprocessor/include>). A construção __has_embed(__FILE__ ... aparece em um dos exemplos no padrão, sugerindo, no caso (2) pelo menos, que o diretório onde o arquivo atual reside é esperado ser pesquisado.

3) Os tokens de pré-processamento após `embed` na diretiva são processados assim como em texto normal (ou seja, cada identificador atualmente definido como um nome de macro é substituído por sua lista de substituição de tokens de pré-processamento). A diretiva resultante após todas as substituições deve corresponder a uma das duas formas anteriores. O método pelo qual uma sequência de tokens de pré-processamento entre um par de tokens de pré-processamento < e > ou um par de caracteres " é combinada em um único token de pré-processamento de nome de cabeçalho é definido pela implementação.

4) O recurso identificado por h-char-sequence ou q-char-sequence é procurado como se essa sequência de tokens de pré-processamento fosse os pp-tokens na sintaxe (3), exceto que nenhuma expansão de macro adicional é realizada. Se tal diretiva não satisfizer os requisitos sintáticos de uma diretiva #embed, o programa é malformado. A expressão `__has__embed` avalia para `__STDC_EMBED_FOUND__` se a busca pelo recurso for bem-sucedida, o recurso não estiver vazio e todos os parâmetros forem suportados, para `__STDC_EMBED_EMPTY__` se o recurso estiver vazio e todos os parâmetros forem suportados, e para `__STDC_EMBED_NOT_FOUND__` se a busca falhar ou um dos parâmetros passados não for suportado pela implementação.

5) Esta forma é considerada apenas se a sintaxe (4) não corresponder, caso em que os tokens de pré-processamento são processados assim como em texto normal.

No caso de o recurso não ser encontrado ou um dos parâmetros não ser suportado pela implementação, o programa é malformado.

`__has_embed` pode ser expandido na expressão de [` #if`](<#/doc/preprocessor/conditional>) e [` #elif`](<#/doc/preprocessor/conditional>). É tratado como uma macro definida por [` #ifdef`](<#/doc/preprocessor/conditional>), [` #ifndef`](<#/doc/preprocessor/conditional>), [` #elifdef`](<#/doc/preprocessor/conditional>), [` #elifndef`](<#/doc/preprocessor/conditional>) e [`defined`](<#/doc/preprocessor/conditional>), mas não pode ser usado em nenhum outro lugar.

Um recurso possui uma _largura de recurso da implementação_ que é o tamanho definido pela implementação em bits do recurso localizado. Sua _largura de recurso_ é a largura de recurso da implementação, a menos que modificada por um parâmetro `limit`. Se a largura de recurso for 0, o recurso é considerado vazio. A _largura do elemento de inclusão_ é igual a [CHAR_BIT](<#/doc/types/limits>), a menos que modificada por um parâmetro definido pela implementação. A largura do recurso deve ser divisível pela largura do elemento de inclusão.

A expansão de uma diretiva #embed é uma sequência de tokens formada a partir da lista de [expressões constantes](<#/doc/language/constant_expression>) inteiras descritas abaixo. O grupo de tokens para cada expressão constante inteira na lista é separado na sequência de tokens do grupo de tokens para a expressão constante inteira anterior na lista por uma vírgula. A sequência não começa nem termina com uma vírgula. Se a lista de expressões constantes inteiras estiver vazia, a sequência de tokens estará vazia. A diretiva é substituída por sua expansão e, com a presença de certos parâmetros de inclusão, sequências de tokens adicionais ou de substituição.

Os valores das expressões constantes inteiras na sequência expandida são determinados por um mapeamento definido pela implementação dos dados do recurso. O valor de cada expressão constante inteira está no intervalo `[`0`, `2embed element width`)`. Se:

  1. A lista de expressões constantes inteiras for usada para inicializar um array de um tipo compatível com unsigned char, ou compatível com char se char não puder conter valores negativos, e
  2. A largura do elemento de inclusão for igual a [CHAR_BIT](<#/doc/types/limits>),

então o conteúdo dos elementos inicializados do array é como se os dados binários do recurso fossem [fread](<#/doc/io/fread>) para o array no tempo de tradução.

As implementações são encorajadas a levar em consideração as ordens de bits e bytes no tempo de tradução, bem como as ordens de bits e bytes no tempo de execução, para representar de forma mais apropriada os dados binários do recurso a partir da diretiva. Isso maximiza a chance de que, se o recurso referenciado no tempo de tradução através da diretiva #embed for o mesmo acessado por meios de tempo de execução, os dados que são, por exemplo, [fread](<#/doc/io/fread>) ou similar em armazenamento contíguo, serão comparados bit a bit como iguais a um array de tipo caractere inicializado a partir do conteúdo expandido de uma diretiva #embed.

### Parâmetros

O padrão define os parâmetros `limit`, `prefix`, `suffix` e `if_empty`. Qualquer outro parâmetro que apareça na diretiva deve ser definido pela implementação, ou o programa é malformado. Parâmetros de inclusão definidos pela implementação podem alterar a semântica da diretiva.

#### limit

---
`limit(` constant-expression `)` | (1) |
`__limit__(` constant-expression `)` | (2) |

O parâmetro de inclusão `limit` pode aparecer no máximo uma vez na sequência de parâmetros de inclusão. Ele deve ter um argumento, que deve ser uma [expressão constante](<#/doc/language/constant_expression>) inteira (de pré-processador) que avalia para um número não negativo e não contém o token defined. A largura do recurso é definida como o mínimo da expressão constante inteira multiplicada pela largura do elemento de inclusão e a largura do recurso da implementação.

#### suffix

---
`suffix(` pp-balanced-token-sequence ﻿(optional) `)` | (1) |
`__suffix__(` pp-balanced-token-sequence ﻿(optional) `)` | (2) |

O parâmetro de inclusão `suffix` pode aparecer no máximo uma vez na sequência de parâmetros de inclusão. Ele deve ter uma cláusula de argumento de pré-processador (possivelmente vazia). Se o recurso não estiver vazio, o conteúdo da cláusula de parâmetro é colocado imediatamente após a expansão da diretiva. Caso contrário, não tem efeito.

#### prefix

---
`prefix(` pp-balanced-token-sequence ﻿(optional) `)` | (1) |
`__prefix__(` pp-balanced-token-sequence ﻿(optional) `)` | (2) |

O parâmetro de inclusão `prefix` pode aparecer no máximo uma vez na sequência de parâmetros de inclusão. Ele deve ter uma cláusula de argumento de pré-processador (possivelmente vazia). Se o recurso não estiver vazio, o conteúdo da cláusula de parâmetro é colocado imediatamente antes da expansão da diretiva. Caso contrário, não tem efeito.

#### if_empty

---
`if_empty(` pp-balanced-token-sequence ﻿(optional) `)` | (1) |
`__if_empty__(` pp-balanced-token-sequence ﻿(optional) `)` | (2) |

O parâmetro de inclusão `if_empty` pode aparecer no máximo uma vez na sequência de parâmetros de inclusão. Ele deve ter uma cláusula de argumento de pré-processador (possivelmente vazia). Se o recurso estiver vazio, o conteúdo da cláusula de parâmetro substitui a diretiva. Caso contrário, não tem efeito.

### Exemplo

Execute este código
```c
    #include <stdint.h>
    #include <stdio.h>
    
    const uint8_t image_data[] = {
    #embed "image.png"
    };
    
    const char message[] = {
    #embed "message.txt" if_empty('M', 'i', 's', 's', 'i', 'n', 'g', '\n')
    ,'\0' // null terminator
    };
    
    void dump(const uint8_t arr[], size_t size)
    {
        for (size_t i = 0; i != size; ++i)
            printf("%02X%c", arr[i], (i + 1) % 16 ? ' ' : '\n');
        puts("");
    }
    
    int main()
    {
        puts("image_data[]:");
        dump(image_data, sizeof image_data);
        puts("message[]:");
        dump((const uint8_t*)message, sizeof message);
    }
```

Saída possível:
```
    image_data[]:
    89 50 4E 47 0D 0A 1A 0A 00 00 00 0D 49 48 44 52
    00 00 00 01 00 00 00 01 01 03 00 00 00 25 DB 56
    ...
    message[]:
    4D 69 73 73 69 6E 67 0A 00
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

  * 6.4.7 Nomes de cabeçalho (p: 69)

  * 6.10.1 Inclusão condicional (p: 165-169)

  * 6.10.2 Inclusão de recurso binário (p: 170-177)