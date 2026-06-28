# Controle de comportamento definido pela implementação

O comportamento definido pela implementação é controlado pela diretiva `#pragma`.

### Sintaxe

---
`#pragma` pragma_params | (1) |
`_Pragma` `(` string-literal `)` | (2) | (desde C99)

1) Comporta-se de maneira definida pela implementação (a menos que pragma_params seja uma das pragmas padrão mostradas abaixo).

2) Remove o prefixo de codificação (se houver), as aspas externas e os espaços em branco iniciais/finais do string-literal, substitui cada `\"` por `"` e cada `\\` por `\`, então tokeniza o resultado (como na [fase de tradução 3](<#/doc/language/translation_phases>)), e então usa o resultado como se fosse a entrada para `#pragma` em (1).

### Explicação

A diretiva pragma controla o comportamento específico da implementação do compilador, como desabilitar avisos do compilador ou alterar requisitos de alinhamento. Qualquer pragma que não for reconhecida é ignorada.

### Pragmas padrão

As três pragmas a seguir são definidas pelo padrão da linguagem:

---
`#pragma STDC FENV_ACCESS` arg | (1) | (desde C99)
`#pragma STDC FP_CONTRACT` arg | (2) | (desde C99)
`#pragma STDC CX_LIMITED_RANGE` arg | (3) | (desde C99)

onde arg é `ON` ou `OFF` ou `DEFAULT`.

1) Se definido como `ON`, informa ao compilador que o programa acessará ou modificará o [ambiente de ponto flutuante](<#/doc/numeric/fenv>), o que significa que otimizações que poderiam subverter testes de flags e mudanças de modo (por exemplo, eliminação de subexpressões comuns globais, movimentação de código e folding de constantes) são proibidas. O valor padrão é definido pela implementação, geralmente `OFF`.

2) Permite a _contração_ de expressões de ponto flutuante, ou seja, otimizações que omitem erros de arredondamento e exceções de ponto flutuante que seriam observadas se a expressão fosse avaliada exatamente como escrita. Por exemplo, permite a implementação de (x * y) + z com uma única instrução FMA (fused multiply-add) da CPU. O valor padrão é definido pela implementação, geralmente `ON`.

3) Informa ao compilador que a multiplicação, divisão e valor absoluto de números complexos podem usar fórmulas matemáticas simplificadas (x+iy)×(u+iv) = (xu-yv)+i(yu+xv), (x+iy)/(u+iv) = [(xu+yv)+i(yu-xv)]/(u2
+v2
), e |x+iy| = √x2
+y2
, apesar da possibilidade de overflow intermediário. Em outras palavras, o programador garante que o intervalo dos valores que serão passados para essas funções é limitado. O valor padrão é `OFF`

Nota: compiladores que não suportam essas pragmas podem fornecer opções de tempo de compilação equivalentes, como `-fcx-limited-range` e `-ffp-contract` do gcc.

### Pragmas não padrão

#### #pragma once

#pragma once é uma pragma não padrão que é suportada pela [grande maioria dos compiladores modernos](<https://en.wikipedia.org/wiki/Pragma_once#Portability> "enwiki:Pragma once"). Se ela aparece em um arquivo de cabeçalho, indica que ele deve ser analisado apenas uma vez, mesmo que seja incluído (direta ou indiretamente) várias vezes no mesmo arquivo fonte.

A abordagem padrão para evitar a inclusão múltipla do mesmo cabeçalho é usando [include guards](<https://en.wikipedia.org/wiki/Include_guard> "enwiki:Include guard"):
```
    #ifndef LIBRARY_FILENAME_H
    #define LIBRARY_FILENAME_H
    // conteúdo do cabeçalho
    #endif /* LIBRARY_FILENAME_H */
```

De modo que todas as inclusões do cabeçalho, exceto a primeira em qualquer unidade de tradução, são excluídas da compilação. Todos os compiladores modernos registram o fato de que um arquivo de cabeçalho usa um include guard e não reanalisam o arquivo se ele for encontrado novamente, desde que o guard ainda esteja definido (veja, por exemplo, [gcc](<https://gcc.gnu.org/onlinedocs/cpp/Once-Only-Headers.html>)).

Com #pragma once, o mesmo cabeçalho aparece como
```
    #pragma once
    // conteúdo do cabeçalho
```

Ao contrário dos header guards, esta pragma torna impossível usar erroneamente o mesmo nome de macro em mais de um arquivo. Por outro lado, como com #pragma once os arquivos são excluídos com base em sua identidade no nível do sistema de arquivos, isso não pode proteger contra a inclusão de um cabeçalho duas vezes se ele existir em mais de um local em um projeto.

#### #pragma pack

Esta família de pragmas controla o alinhamento máximo para membros de estruturas e uniões definidos subsequentemente.

---
`#pragma pack( arg) ` | (1) |
`#pragma pack()` | (2) |
`#pragma pack(push)` | (3) |
`#pragma pack(push, arg) ` | (4) |
`#pragma pack(pop)` | (5) |

onde arg é uma pequena potência de dois e especifica o novo alinhamento em bytes.

1) Define o alinhamento atual para o valor arg.

2) Define o alinhamento atual para o valor padrão (especificado por uma opção de linha de comando).

3) Empilha o valor do alinhamento atual em uma pilha interna.

4) Empilha o valor do alinhamento atual na pilha interna e então define o alinhamento atual para o valor arg.

5) Desempilha a entrada superior da pilha interna e então define (restaura) o alinhamento atual para esse valor.

#pragma pack pode diminuir o alinhamento de uma estrutura, no entanto, não pode tornar uma estrutura superalinhada.

Veja também detalhes específicos para [GCC](<https://gcc.gnu.org/onlinedocs/gcc/Structure-Layout-Pragmas.html>) e [MSVC](<https://docs.microsoft.com/en-us/cpp/preprocessor/pack>).

| Esta seção está incompleta
Motivo: Explicar os efeitos dessas pragmas em membros de dados e também os prós e contras de usá-las. Fontes para referência:

  * [Stack Overflow](<https://stackoverflow.com/questions/3318410/pragma-pack-effect>)

| Esta seção está incompleta
Motivo: sem exemplo

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 6.10.6 Diretiva Pragma (p: 127)

    

  * 6.10.9 Operador Pragma (p: 129)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 6.10.6 Diretiva Pragma (p: 174)

    

  * 6.10.9 Operador Pragma (p: 178)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 6.10.6 Diretiva Pragma (p: 159)

    

  * 6.10.9 Operador Pragma (p: 161-162)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 3.8.6 Diretiva Pragma

### Veja também

[Documentação C++](<#/>) para Controle de comportamento definido pela implementação
---

### Links externos

1. | [Pragmas C++ no Visual Studio 2019](<https://docs.microsoft.com/en-us/cpp/preprocessor/pragma-directives-and-the-pragma-keyword?view=vs-2019>)
2. | [Pragmas](<https://gcc.gnu.org/onlinedocs/gcc/Pragmas.html>) aceitas pelo GCC
3. | [Descrições de pragma individuais](<https://www.ibm.com/support/knowledgecenter/en/SSGH3R_16.1.0/com.ibm.xlcpp161.aix.doc/compiler_ref/pragma_descriptions.html>) e [Pragmas padrão](<https://www.ibm.com/support/knowledgecenter/en/SSGH3R_16.1.0/com.ibm.xlcpp161.aix.doc/language_ref/std_pragmas.html>) no IBM AIX XL C 16.1
4. | [Apêndice B. Pragmas](<http://download.oracle.com/docs/cd/E19422-01/819-3690/Pragmas_App.html#73499>) no Guia do Usuário do Sun Studio 11 C++
5. | [Pragmas do compilador Intel C++](<https://software.intel.com/content/www/us/en/develop/documentation/cpp-compiler-developer-guide-and-reference/top/compiler-reference/pragmas.html>)
6. | [Pragmas do compilador HP aCC](<http://h21007.www2.hp.com/portal/download/files/unprot/aCxx/Online_Help/pragmas.htm>)