# Sequências de escape

Sequências de escape são usadas para representar certos caracteres especiais dentro de [literais de string](<#/doc/language/string_literal>) e [constantes de caractere](<#/doc/language/character_constant>).

As seguintes sequências de escape estão disponíveis. O ISO C exige um diagnóstico se a barra invertida for seguida por qualquer caractere não listado aqui:

Escape
sequência | Descrição | Representação
Sequências de escape simples
`\'` | aspas simples | byte `0x27` na codificação ASCII
`\"` | aspas duplas | byte `0x22` na codificação ASCII
`\?` | ponto de interrogação | byte `0x3f` na codificação ASCII
`\\` | barra invertida | byte `0x5c` na codificação ASCII
`\a` | sinal sonoro | byte `0x07` na codificação ASCII
`\b` | retrocesso | byte `0x08` na codificação ASCII
`\f` | salto de página - nova página | byte `0x0c` na codificação ASCII
`\n` | avanço de linha - nova linha | byte `0x0a` na codificação ASCII
`\r` | retorno de carro | byte `0x0d` na codificação ASCII
`\t` | tabulação horizontal | byte `0x09` na codificação ASCII
`\v` | tabulação vertical | byte `0x0b` na codificação ASCII
Sequências de escape numéricas
`\_nnn_` | valor octal arbitrário | unidade de código `_nnn_`
`\x _n..._` | valor hexadecimal arbitrário | unidade de código `_n..._` (número arbitrário de dígitos hexadecimais)
Nomes de caracteres universais
`\u _nnnn_` (desde C99) | valor [ Unicode](<https://en.wikipedia.org/wiki/Unicode> "enwiki:Unicode") no intervalo permitido;
pode resultar em várias unidades de código | ponto de código `U+_nnnn_`
`\U _nnnnnnnn_` (desde C99) | valor [ Unicode](<https://en.wikipedia.org/wiki/Unicode> "enwiki:Unicode") no intervalo permitido;
pode resultar em várias unidades de código | ponto de código `U+_nnnnnnnn_`

### Intervalo de nomes de caracteres universais

Se um nome de caractere universal corresponder a um ponto de código que não seja `0x24` ('$'), `0x40` ('@'), nem `0x60` ('`') e menor que `0xA0`, ou um ponto de código substituto (o intervalo `0xD800-0xDFFF`, inclusive), ou maior que `0x10FFFF`, ou seja, não um ponto de código Unicode (desde C23), o programa é malformado. Em outras palavras, membros do [conjunto básico de caracteres fonte](<#/doc/language/translation_phases>) e caracteres de controle (nos intervalos `0x0-0x1F` e `0x7F-0x9F`) não podem ser expressos em nomes de caracteres universais. | (desde C99)

### Notas

`\0` é a sequência de escape octal mais comumente usada, porque representa o caractere nulo terminador em strings terminadas em nulo.

O caractere de nova linha `\n` tem um significado especial quando usado em [E/S em modo texto](<#/doc/io>): ele é convertido para o byte ou sequência de bytes de nova linha específico do sistema operacional.

Sequências de escape octais têm um limite de comprimento de três dígitos octais, mas terminam no primeiro caractere que não é um dígito octal válido, se encontrado antes.

Sequências de escape hexadecimais não têm limite de comprimento e terminam no primeiro caractere que não é um dígito hexadecimal válido. Se o valor representado por uma única sequência de escape hexadecimal não se encaixar no intervalo de valores representados pelo tipo de caractere usado neste literal de string ou constante de caractere (`char`, `char8_t`(desde C23), `char16_t`, `char32_t`(desde C11), ou `wchar_t`), o resultado é não especificado.

Um nome de caractere universal em um literal de string estreito ou um literal de string de 16 bits (desde C11) pode mapear para mais de uma unidade de código, por exemplo, `\U0001f34c` são 4 unidades de código `char` em UTF-8 (`\xF0\x9F\x8D\x8C`) e 2 unidades de código `char16_t` em UTF-16 (`\xD83C\xDF4C`)(desde C11). | (desde C99)
Um nome de caractere universal correspondente a um ponteiro de código maior que `0x10FFFF` (que é indefinido em ISO/ISC 10646) pode ser usado em [constantes de caractere](<#/doc/language/character_constant>) e [literais de string](<#/doc/language/string_literal>). Tal uso não é permitido em C++20. | (desde C99)
(até C23)
A sequência de escape de ponto de interrogação `\?` é usada para evitar que [trígrafos](<#/doc/language/operator_alternative>) sejam interpretados dentro de literais de string: uma string como "`??/`" é compilada como "`\`", mas se o segundo ponto de interrogação for escapado, como em "`?\?/`", ela se torna "`??/`" | (até C23)

### Exemplo

Execute este código
```c
    #include <stdio.h>
     
    int main(void)
    {
        printf("This\nis\na\ntest\n\nShe said, \"How are you?\"\n");
    }
```

Saída:
```
    This
    is
    a
    test
     
    She said, "How are you?"
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 5.2.2 Semântica de exibição de caracteres (p: 18-19)

    

  * 6.4.3 Nomes de Caracteres Universais (p: 44)

    

  * 6.4.4.4 Constantes de caracteres (p: 48-50)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 5.2.2 Semântica de exibição de caracteres (p: 24-25)

    

  * 6.4.3 Nomes de Caracteres Universais (p: 61)

    

  * 6.4.4.4 Constantes de caracteres (p: 67-70)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 5.2.2 Semântica de exibição de caracteres (p: 19-20)

    

  * 6.4.3 Nomes de Caracteres Universais (p: 53)

    

  * 6.4.4.4 Constantes de caracteres (p: 59-61)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 2.2.2 Semântica de exibição de caracteres

    

  * 3.1.3.4 Constantes de caracteres

### Veja também

  * [Tabela ASCII](<#/doc/language/ascii>)

[Documentação C++](<#/>) para Sequências de escape
---