# Constante de caractere

### Sintaxe  
  
---  
`'` c-char `'` | (1) |   
`u8'` c-char `'` | (2) | (desde C23)  
`u'` c-char `'` | (3) | (desde C11)  
`U'` c-char `'` | (4) | (desde C11)  
`L'` c-char `'` | (5) |   
`'` c-char-sequence `'` | (6) |   
`L'` c-char-sequence `'` | (7) |   
`u'` c-char-sequence `'` | (8) | (desde C11)(removido em C23)  
`U'` c-char-sequence `'` | (9) | (desde C11)(removido em C23)  
  
onde 

  * c-char é um dos seguintes: 

    

  * um caractere do conjunto de caracteres fonte básico, exceto aspas simples (`'`), barra invertida (`\`) ou o caractere de nova linha. 
  * sequência de escape: uma das sequências de escape de caracteres especiais \' \" \? \\\ \a \b \f \n \r \t \v, escapes hexadecimais \x... ou escapes octais \\... conforme definido em [sequências de escape](<#/doc/language/escape>). 

    

  * nome de caractere universal, \u... ou \U... conforme definido em [sequências de escape](<#/doc/language/escape>). 

| (desde C99)  
  
  * c-char-sequence é uma sequência de dois ou mais c-chars. 

1) constante de caractere inteiro de byte único, por exemplo, 'a' ou '\n' ou '\13'. Tal constante tem o tipo int e um valor igual à representação de c-char no conjunto de caracteres de execução como um valor do tipo char mapeado para int. Se c-char não for representável como um único byte no conjunto de caracteres de execução, o valor é definido pela implementação.

2) constante de caractere UTF-8, por exemplo, u8'a'. Tal constante tem o tipo char8_t e o valor igual ao valor do ponto de código ISO 10646 de c-char, desde que o valor do ponto de código seja representável com uma única unidade de código UTF-8 (ou seja, c-char está no intervalo 0x0-0x7F, inclusive). Se c-char não for representável com uma única unidade de código UTF-8, o programa é malformado.

3) constante de caractere largo de 16 bits, por exemplo, u'貓', mas não u'🍌' (u'\U0001f34c'). Tal constante tem o tipo char16_t e um valor igual ao valor de c-char na codificação de 16 bits produzida por [mbrtoc16](<#/doc/string/multibyte/mbrtoc16>) (normalmente UTF-16). Se c-char não for representável ou mapear para mais de um caractere de 16 bits, o valor é definido pela implementação. 4) constante de caractere largo de 32 bits, por exemplo, U'貓' ou U'🍌'. Tal constante tem o tipo char32_t e um valor igual ao valor de c-char na codificação de 32 bits produzida por [mbrtoc32](<#/doc/string/multibyte/mbrtoc32>) (normalmente UTF-32). Se c-char não for representável ou mapear para mais de um caractere de 32 bits, o valor é definido pela implementação.  | (até C23)  
3) constante de caractere UTF-16, por exemplo, u'貓', mas não u'🍌' (u'\U0001f34c'). Tal constante tem o tipo char16_t e o valor igual ao valor do ponto de código ISO 10646 de c-char, desde que o valor do ponto de código seja representável com uma única unidade de código UTF-16 (ou seja, c-char está no intervalo 0x0-0xD7FF ou 0xE000-0xFFFF, inclusive). Se c-char não for representável com uma única unidade de código UTF-16, o programa é malformado. 4) constante de caractere UTF-32, por exemplo, U'貓' ou U'🍌'. Tal constante tem o tipo char32_t e o valor igual ao valor do ponto de código ISO 10646 de c-char, desde que o valor do ponto de código seja representável com uma única unidade de código UTF-32 (ou seja, c-char está no intervalo 0x0-0xD7FF ou 0xE000-0x10FFFF, inclusive). Se c-char não for representável com uma única unidade de código UTF-32, o programa é malformado.  | (desde C23)  
  
5) constante de caractere largo, por exemplo, L'β' ou L'貓. Tal constante tem o tipo wchar_t e um valor igual ao valor de c-char no conjunto de caracteres largos de execução (ou seja, o valor que seria produzido por [mbtowc](<#/doc/string/multibyte/mbtowc>)). Se c-char não for representável ou mapear para mais de um caractere largo (por exemplo, um valor não-BMP no Windows onde wchar_t tem 16 bits), o valor é definido pela implementação.

6) constante de multicaractere, por exemplo, 'AB', tem o tipo int e valor definido pela implementação.

7) constante de multicaractere largo, por exemplo, L'AB', tem o tipo wchar_t e valor definido pela implementação.

8) constante de multicaractere de 16 bits, por exemplo, u'CD', tem o tipo char16_t e valor definido pela implementação.

9) constante de multicaractere de 32 bits, por exemplo, U'XY', tem o tipo char32_t e valor definido pela implementação.

### Notas

Constantes de multicaractere foram herdadas pelo C da linguagem de programação B. Embora não especificadas pelo padrão C, a maioria dos compiladores (MSVC é uma exceção notável) implementa constantes de multicaractere conforme especificado em B: os valores de cada char na constante inicializam bytes sucessivos do inteiro resultante, em ordem big-endian preenchida com zeros e alinhada à direita, por exemplo, o valor de '\1' é 0x00000001 e o valor de '\1\2\3\4' é 0x01020304. 

Em C++, literais de caractere comuns codificáveis têm o tipo char, em vez de int. 

Ao contrário das [constantes inteiras](<#/doc/language/integer_constant>), uma constante de caractere pode ter um valor negativo se char for assinado: em tais implementações, '\xFF' é um int com o valor -1. 

Quando usadas em uma expressão de controle de [` #if`](<#/doc/preprocessor/conditional>) ou [` #elif`](<#/doc/preprocessor/conditional>), as constantes de caractere podem ser interpretadas em termos do conjunto de caracteres fonte, do conjunto de caracteres de execução ou de algum outro conjunto de caracteres definido pela implementação. 

Constantes de multicaractere de 16/32 bits não são amplamente suportadas e foram removidas no C23. Algumas implementações comuns (por exemplo, clang) não as aceitam de forma alguma. 

### Exemplo

Execute este código
```c
    #include <stddef.h>
    #include <stdio.h>
    #include <uchar.h>
     
    int main (void)
    {
        printf("constant value     \n");
        printf("-------- ----------\n");
     
        // integer character constants,
        int c1='a'; printf("'a':\t %#010x\n", c1);
        int c2='🍌'; printf("'🍌':\t %#010x\n\n", c2); // implementation-defined
     
        // multicharacter constant
        int c3='ab'; printf("'ab':\t %#010x\n\n", c3); // implementation-defined
     
        // 16-bit wide character constants
        char16_t uc1 = u'a'; printf("'a':\t %#010x\n", (int)uc1);
        char16_t uc2 = u'¢'; printf("'¢':\t %#010x\n", (int)uc2);
        char16_t uc3 = u'猫'; printf("'猫':\t %#010x\n", (int)uc3);
        // implementation-defined (🍌 maps to two 16-bit characters)
        char16_t uc4 = u'🍌'; printf("'🍌':\t %#010x\n\n", (int)uc4);
     
        // 32-bit wide character constants
        char32_t Uc1 = U'a'; printf("'a':\t %#010x\n", (int)Uc1);
        char32_t Uc2 = U'¢'; printf("'¢':\t %#010x\n", (int)Uc2);
        char32_t Uc3 = U'猫'; printf("'猫':\t %#010x\n", (int)Uc3);
        char32_t Uc4 = U'🍌'; printf("'🍌':\t %#010x\n\n", (int)Uc4);
     
        // wide character constants
        wchar_t wc1 = L'a'; printf("'a':\t %#010x\n", (int)wc1);
        wchar_t wc2 = L'¢'; printf("'¢':\t %#010x\n", (int)wc2);
        wchar_t wc3 = L'猫'; printf("'猫':\t %#010x\n", (int)wc3);
        wchar_t wc4 = L'🍌'; printf("'🍌':\t %#010x\n\n", (int)wc4);
    }
```

Saída possível: 
```
    constant value     
    -------- ----------
    'a':	 0x00000061
    '🍌':	 0xf09f8d8c
     
    'ab':	 0x00006162
     
    'a':	 0x00000061
    '¢':	 0x000000a2
    '猫':	 0x0000732b
    '🍌':	 0x0000df4c
     
    'a':	 0x00000061
    '¢':	 0x000000a2
    '猫':	 0x0000732b
    '🍌':	 0x0001f34c
     
    'a':	 0x00000061
    '¢':	 0x000000a2
    '猫':	 0x0000732b
    '🍌':	 0x0001f34c
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 6.4.4.4 Constantes de caractere (p: 48-50) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 6.4.4.4 Constantes de caractere (p: 67-70) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 6.4.4.4 Constantes de caractere (p: 59-61) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 3.1.3.4 Constantes de caractere 

### Veja também

[documentação C++](<#/>) para literal de caractere  
---