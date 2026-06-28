# Conjuntos de caracteres e codificações

### Conjunto de caracteres básico
  
O _conjunto de caracteres básico_ consiste nos seguintes 95 caracteres: 

Unidade de código | Caractere | Glifo   
U+0009 | Tabulação de caractere |   
U+000B | Tabulação de linha |   
U+000C | Salto de página (FF) |   
U+0020 | Espaço |   
U+0021 | Ponto de exclamação | `!`  
U+0022 | Aspas | `"`  
U+0023 | Sinal de número | `#`  
U+0025 | Sinal de porcentagem | `%`  
U+0026 | E comercial | `&`  
U+0027 | Apóstrofo | `'`  
U+0028 | Parêntese esquerdo | `(`  
U+0029 | Parêntese direito | `)`  
U+002A | Asterisco | `*`  
U+002B | Sinal de mais | `+`  
U+002C | Vírgula | `,`  
U+002D | Hífen-menos | `-`  
U+002E | Ponto final | `.`  
U+002F | Barra | `/`  
U+0030 .. U+0039 | Dígito zero .. nove | `0 1 2 3 4 5 6 7 8 9`  
U+003A | Dois pontos | `:`  
U+003B | Ponto e vírgula | `;`  
U+003C | Sinal de menor que | `<`  
U+003D | Sinal de igual | `=`  
U+003E | Sinal de maior que | `>`  
U+003F | Ponto de interrogação | `?`  
U+0041 .. U+005A | Letra latina maiúscula A .. Z | `A B C D E F G H I J K L M` `N O P Q R S T U V W X Y Z`  
U+005B | Colchete esquerdo | `[`  
U+005C | Barra invertida | `\`  
U+005D | Colchete direito | `]`  
U+005E | Acento circunflexo | `^`  
U+005F | Sublinhado | `_`  
U+0061 .. U+007A | Letra latina minúscula a .. z | `a b c d e f g h i j k l m` `n o p q r s t u v w x y z`  
U+007B | Chave esquerda | `{`  
U+007C | Barra vertical | `|`  
U+007D | Chave direita | `}`  
U+007E | Til | `~`  
  
Ao contrário de C++, o caractere U+000A LINE FEED (LF) não está incluído no conjunto de caracteres básico. Em vez disso, deve haver alguma forma de indicar o fim de cada linha de texto no arquivo fonte, e o documento trata tal indicador de fim de linha como se fosse um único caractere de nova linha. 

O conjunto de caracteres básico também é conhecido como _conjunto de caracteres fonte básico_. 

### Conjunto de caracteres de execução básico

O _conjunto de caracteres de execução básico_ contém todos os membros do conjunto de caracteres básico, mais os seguintes caracteres: 

Unidade de código | Caractere   
U+0000 | Nulo   
U+0007 | Sinal sonoro   
U+0008 | Retrocesso   
U+000A | Salto de linha (LF)   
U+000D | Retorno de carro (CR)   
  
Para cada conjunto de caracteres de execução básico, os valores dos membros devem ser não negativos e distintos entre si. Tanto nos conjuntos de caracteres fonte quanto de execução básicos, o valor de cada caractere após 0 na lista acima de dígitos decimais deve ser um a mais que o valor do anterior. O caractere U+0000 NULL tem o valor 0. 

A representação de cada membro dos conjuntos de caracteres de execução básicos cabe em um byte. 

Em C++, o conjunto de caracteres de execução básico também é conhecido como _conjunto de caracteres literal básico_ e _conjunto de caracteres largos de execução básico_. 

### Codificações literais

A _codificação literal_ é um mapeamento definido pela implementação dos caracteres do conjunto de caracteres de execução para os valores em uma [constante de caractere](<#/doc/language/character_constant>) ou [literal de string](<#/doc/language/string_literal>) sem prefixo de codificação. Ela suporta um mapeamento de todos os valores do conjunto de caracteres de execução básico para a codificação definida pela implementação. Pode conter sequências de caracteres multibyte. 

Os seguintes caracteres não estão no conjunto de caracteres de execução básico, mas são exigidos para serem codificados como um único byte em uma constante de caractere comum ou literal de string comum.  |  Unidade de código | Caractere | Glifo   
U+0024 | Sinal de dólar | `$`  
U+0040 | Arroba | `@`  
U+0060 | Acento grave | `  
(desde C23)  
  
A _codificação literal larga_ é um mapeamento definido pela implementação dos caracteres do conjunto de caracteres de execução para os valores em uma constante de caractere ou literal de string prefixada com `L`. Ela suporta um mapeamento de todos os valores do conjunto de caracteres de execução básico para a codificação definida pela implementação. Se uma implementação não definir `__STDC_MB_MIGHT_NEQ_WC__`, o mapeamento produzirá valores idênticos à codificação literal para todos os valores do conjunto de caracteres de execução básico. Um ou mais valores podem mapear para um ou mais valores do conjunto de caracteres de execução estendido. 

A codificação UTF-8 é usada para mapear caracteres do conjunto de caracteres de execução para uma constante de caractere ou (desde C23) literal de string prefixada com `u8`. Uma codificação definida pela implementação (até C23) A codificação UTF-16 (desde C23) é usada para mapear caracteres do conjunto de caracteres de execução para uma constante de caractere ou literal de string prefixada com `u`. Uma codificação definida pela implementação (até C23) A codificação UTF-32 (desde C23) é usada para mapear caracteres do conjunto de caracteres de execução para uma constante de caractere ou literal de string prefixada com `U`.  | (desde C11)  
  
### Veja também

[Tabela ASCII](<#/doc/language/ascii>)  
---  
[Documentação C++](<#/>) para Conjuntos de caracteres e codificações