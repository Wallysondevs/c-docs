# Operadores e tokens alternativos

O código-fonte C pode ser escrito em qualquer conjunto de caracteres de 8 bits que inclua o conjunto de caracteres invariantes [ISO 646:1983](<https://en.wikipedia.org/wiki/ISO_646> "enwiki:ISO 646"), mesmo os não-ASCII. No entanto, vários operadores e pontuadores C exigem caracteres que estão fora do conjunto de códigos ISO 646: `{, }, [, ], #, \, ^, |, ~`. Para poder usar codificações de caracteres onde alguns ou todos esses símbolos não existem (como o alemão [DIN 66003](<https://en.wikipedia.org/wiki/DIN_66003> "enwiki:DIN 66003")), existem duas possibilidades: grafias alternativas de operadores que usam esses caracteres ou combinações especiais de dois ou três caracteres compatíveis com ISO 646 que são interpretados como se fossem um único caractere não-ISO 646.

## Macros de operador (C95)

Existem grafias alternativas para os operadores que usam caracteres não-ISO646, definidas em `< iso646.h>` como macros:

Definido no cabeçalho `<iso646.h>`
---
Primário | Alternativo
`&&` | `and`
(macro de operador)
`&=` | `and_eq`
(macro de operador)
`&` | `bitand`
(macro de operador)
`|` | `bitor`
(macro de operador)
`~` | `compl`
(macro de operador)
`!` | `not`
(macro de operador)
`!=` | `not_eq`
(macro de operador)
`||` | `or`
(macro de operador)
`|=` | `or_eq`
(macro de operador)
`^` | `xor`
(macro de operador)
`^=` | `xor_eq`
(macro de operador)

Os caracteres & e ! são invariantes sob ISO-646, mas alternativas são fornecidas para os operadores que usam esses caracteres de qualquer forma para acomodar conjuntos de caracteres históricos ainda mais restritivos.

Não há grafia alternativa (como eq) para o operador de igualdade == porque o caractere = estava presente em todos os conjuntos de caracteres suportados.

## Tokens alternativos (C95)

Os seguintes tokens alternativos fazem parte da linguagem principal e, em todos os aspectos da linguagem, cada token alternativo se comporta exatamente da mesma forma que seu token primário, exceto por sua grafia (o [operador de stringificação](<#/doc/preprocessor/replace>) pode tornar a grafia visível). Os tokens alternativos de duas letras são às vezes chamados de "dígrafos" (embora %:%: tenha quatro letras, também é considerado um dígrafo).

Primário | Alternativo
`{` | `<%`
`}` | `%>`
`[` | `<:`
`]` | `:>`
`#` | `%:`
`##` | `%:%:`

## Trígrafos (removido em C23)

Os seguintes grupos de três caracteres (trígrafos) são [analisados antes que comentários e literais de string sejam reconhecidos](<#/doc/language/translation_phases>), e cada ocorrência de um trígrafo é substituída pelo caractere primário correspondente:

Primário | Trígrafo
`{` | `??<`
`}` | `??>`
`[` | `??(`
`]` | `??)`
`#` | `??=`
`\` | `??/`
`^` | `??'`
`|` | `??!`
`~` | `??-`

Como os trígrafos são processados cedo, um comentário como `// Will the next line be executed?????/` irá efetivamente comentar a linha seguinte, e o literal de string como `"What's going on??!"` é analisado como `"What's going on|"`.

### Exemplo

Demonstra grafias alternativas de operadores do `< iso646.h>`, bem como o uso de dígrafos e trígrafos. Se os argumentos da linha de comando contiverem espaços, eles devem ser envolvidos por aspas, por exemplo, "Third World!".

Execute este código
```c
    %:include <stdio.h>
    %:include <stdlib.h>
    ??=include <iso646.h>
    
    int main(int argc, char** argv)
    ??<
        if (argc > 1 and argv<:1:> not_eq NULL)
        <%
           printf("Hello %s??/n", argv<:1:>);
        %>
        else
        <%
           printf("Hello %s??/n", argc? argv??(42??'42??) : __FILE__);
       %>
    
        return EXIT_SUCCESS;
    ??>
```

Saída possível:
```
    Hello ./a.out
```

### Veja também

[documentação C++](<#/>) para Representações alternativas de operadores
---