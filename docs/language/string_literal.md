# Literais de string

Constrói um objeto sem nome do tipo array de caracteres especificado no local, usado quando uma cadeia de caracteres precisa ser incorporada ao código-fonte.

### Sintaxe

---
`"` s-char-sequence `"` | (1) |
`u8"` s-char-sequence `"` | (2) | (desde C11)
`u"` s-char-sequence `"` | (3) | (desde C11)
`U"` s-char-sequence `"` | (4) | (desde C11)
`L"` s-char-sequence `"` | (5) |

onde

- **s-char-sequence** — zero ou mais caracteres, cada um dos quais é um caractere multibyte do conjunto de caracteres de origem (excluindo (`"`), `\`, e nova linha), ou escape de caractere, escape hexadecimal, escape octal, ou nome de caractere universal (desde C99) conforme definido em [sequências de escape](<#/doc/language/escape>).

1) _literal de string de caractere_ : O tipo do literal é char[N], onde `N` é o tamanho da string em unidades de código da codificação estreita de execução, incluindo o terminador nulo. Cada elemento char no array é inicializado a partir do próximo caractere na s-char-sequence usando o conjunto de caracteres de execução.

2) _literal de string UTF-8_ : O tipo do literal é char[N](ate C23)char8_t[N](desde C23), onde `N` é o tamanho da string em unidades de código UTF-8, incluindo o terminador nulo. Cada elemento char(ate C23)char8_t(desde C23) no array é inicializado a partir do próximo caractere multibyte na s-char-sequence usando a codificação UTF-8.

3) literal de string larga de 16 bits: O tipo do literal é char16_t[N], onde `N` é o tamanho da string em unidades de código de codificação de 16 bits definida pela implementação (tipicamente UTF-16), incluindo o terminador nulo. Cada elemento char16_t no array é inicializado como se executando [mbrtoc16](<#/doc/string/multibyte/mbrtoc16>) em um locale definido pela implementação. 4) literal de string larga de 32 bits: O tipo do literal é char32_t[N], onde `N` é o tamanho da string em unidades de código de codificação de 32 bits definida pela implementação (tipicamente UTF-32), incluindo o terminador nulo. Cada elemento char32_t no array é inicializado como se executando [mbrtoc32](<#/doc/string/multibyte/mbrtoc32>) em um locale definido pela implementação. | (ate C23)
3) _literal de string UTF-16_ : O tipo do literal é char16_t[N], onde `N` é o tamanho da string em unidades de código UTF-16, incluindo o terminador nulo. Cada elemento char16_t no array é inicializado a partir do próximo caractere multibyte na s-char-sequence usando a codificação UTF-16. 4) _literal de string UTF-32_ : O tipo do literal é char32_t[N], onde `N` é o tamanho da string em unidades de código UTF-32, incluindo o terminador nulo. Cada elemento char32_t no array é inicializado a partir do próximo caractere multibyte na s-char-sequence usando a codificação UTF-32. | (desde C23)

5) literal de string larga: O tipo do literal é wchar_t[N], onde `N` é o tamanho da string em unidades de código da codificação larga de execução, incluindo o terminador nulo. Cada elemento wchar_t no array é inicializado como se executando [mbstowcs](<#/doc/string/multibyte/mbstowcs>) em um locale definido pela implementação.

### Explicação

Primeiro, na [fase de tradução 6](<#/doc/language/translation_phases>) (após a expansão de macros), os literais de string adjacentes (isto é, literais de string separados apenas por espaço em branco) são concatenados.

Apenas dois literais de string estreitos ou dois literais de string largos podem ser concatenados. | (ate C99)
Se um literal não tiver prefixo, o literal de string resultante terá a largura/codificação especificada pelo literal prefixado.
```c
    L"Δx = %" PRId16 // at phase 4, PRId16 expands to "d"
                     // at phase 6, L"Δx = %" and "d" form L"Δx = %d"
```

| (desde C99)
Se os dois literais de string tiverem prefixos de codificação diferentes, a concatenação é definida pela implementação, exceto que um literal de string UTF-8 e um literal de string largo não podem ser concatenados. | (desde C11)
(ate C23)
Se os dois literais de string tiverem prefixos de codificação diferentes, a concatenação é malformada. | (desde C23)

Em segundo lugar, na [fase de tradução 7](<#/doc/language/translation_phases>), um caractere nulo terminador é adicionado a cada literal de string, e então cada literal inicializa um array sem nome com [duração de armazenamento](<#/doc/language/storage_duration>) estática e comprimento suficiente para conter o conteúdo do literal de string mais um para o terminador nulo.
```c
    char* p = "\x12" "3"; // cria um array char[3] estático contendo {'\x12', '3', '\0'}
                          // define p para apontar para o primeiro elemento do array
```

Literais de string **não são modificáveis** (e de fato podem ser colocados em memória somente leitura, como `.rodata`). Se um programa tentar modificar o array estático formado por um literal de string, o comportamento é indefinido.
```c
    char* p = "Hello";
    p[1] = 'M'; // Comportamento indefinido
    char a[] = "Hello";
    a[1] = 'M'; // OK: a não é um literal de string
```

Não é exigido nem proibido que literais de string idênticos se refiram ao mesmo local na memória. Além disso, literais de string sobrepostos ou literais de string que são substrings de outros literais de string podem ser combinados.
```c
    "def" == 3+"abcdef"; // pode ser 1 ou 0, definido pela implementação
```

### Notas

Um literal de string não é necessariamente uma string; se um literal de string tiver caracteres nulos embutidos, ele representa um array que contém mais de uma string:
```c
    char* p = "abc\0def"; // strlen(p) == 3, mas o array tem tamanho 8
```

Se um dígito hexadecimal válido seguir um escape hexadecimal em um literal de string, ele falharia na compilação como uma sequência de escape inválida, mas a concatenação de strings pode ser usada como uma solução alternativa:
```c
    //char* p = "\xfff"; // erro: sequência de escape hexadecimal fora do intervalo
    char* p = "\xff""f"; // ok, o literal é char[3] contendo {'\xff', 'f', '\0'}
```

Literais de string podem ser usados para [inicializar arrays](<#/doc/language/array_initialization>), e se o tamanho do array for um a menos que o tamanho do literal de string, o terminador nulo é ignorado:
```c
    char a1[] = "abc"; // a1 é char[4] contendo {'a', 'b', 'c', '\0'}
    char a2[4] = "abc"; // a2 é char[4] contendo {'a', 'b', 'c', '\0'}
    char a3[3] = "abc"; // a3 é char[3] contendo {'a', 'b', 'c'}
```

A codificação dos literais de string de caractere (1) e literais de string largos (5) é definida pela implementação. Por exemplo, o gcc os seleciona com as [opções de linha de comando](<https://gcc.gnu.org/onlinedocs/cpp/Invocation.html>) -fexec-charset e -fwide-exec-charset.

Embora a concatenação mista de literais de string largos seja permitida em C11, quase todos os compiladores rejeitam tal concatenação (a única exceção conhecida é [SDCC](<http://sdcc.sourceforge.net/>)), e sua experiência de uso é desconhecida. Como resultado, a permissão de concatenação mista de literais de string largos é removida em C23.

### Exemplo

Execute este código
```c
    #include <inttypes.h>
    #include <locale.h>
    #include <stddef.h>
    #include <stdio.h>
    #include <stdlib.h>
    #include <uchar.h>
    
    int main(void)
    {
        char s1[] = "a猫🍌"; // or "a\u732B\U0001F34C"
    #if __STDC_VERSION__ >= 202311L
        char8_t
    #else
        char
    #endif
        s2[] = u8"a猫🍌";
        char16_t s3[] = u"a猫🍌";
        char32_t s4[] = U"a猫🍌";
        wchar_t s5[] = L"a猫🍌";
    
        setlocale(LC_ALL, "en_US.utf8");
        printf("  \"%s\" is a char[%zu] holding     { ", s1, sizeof s1 / sizeof *s1);
        for(size_t n = 0; n < sizeof s1 / sizeof *s1; ++n)
            printf("0x%02X ", +(unsigned char)s1[n]);
        puts("}");
        printf(
    #if __STDC_VERSION__ >= 202311L
        "u8\"%s\" is a char8_t[%zu] holding  { "
    #else
        "u8\"%s\" is a char[%zu] holding     { "
    #endif
    , s2, sizeof s2 / sizeof *s2);
        for(size_t n = 0; n < sizeof s2 / sizeof *s2; ++n)
    #if __STDC_VERSION__ >= 202311L
           printf("0x%02X ", s2[n]);
    #else
           printf("0x%02X ", +(unsigned char)s2[n]);
    #endif
        puts("}");
        printf(" u\"a猫🍌\" is a char16_t[%zu] holding { ", sizeof s3 / sizeof *s3);
        for(size_t n = 0; n < sizeof s3 / sizeof *s3; ++n)
           printf("0x%04" PRIXLEAST16" ", s3[n]);
        puts("}");
        printf(" U\"a猫🍌\" is a char32_t[%zu] holding { ", sizeof s4 / sizeof *s4);
        for(size_t n = 0; n < sizeof s4 / sizeof *s4; ++n)
           printf("0x%08" PRIXLEAST32" ", s4[n]);
        puts("}");
        printf(" L\"%ls\" is a wchar_t[%zu] holding  { ", s5, sizeof s5 / sizeof *s5);
        for(size_t n = 0; n < sizeof s5 / sizeof *s5; ++n)
           printf("0x%08X ", (unsigned)s5[n]);
        puts("}");
    }
```

Saída possível:
```
      "a猫🍌" is a char[9] holding     { 0x61 0xE7 0x8C 0xAB 0xF0 0x9F 0x8D 0x8C 0x00 }
    u8"a猫🍌" is a char[9] holding     { 0x61 0xE7 0x8C 0xAB 0xF0 0x9F 0x8D 0x8C 0x00 }
     u"a猫🍌" is a char16_t[5] holding { 0x0061 0x732B 0xD83C 0xDF4C 0x0000 }
     U"a猫🍌" is a char32_t[4] holding { 0x00000061 0x0000732B 0x0001F34C 0x00000000 }
     L"a猫🍌" is a wchar_t[4] holding  { 0x00000061 0x0000732B 0x0001F34C 0x00000000 }
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 6.4.5 Literais de string (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 6.4.5 Literais de string (p: 50-52)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 6.4.5 Literais de string (p: 70-72)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 6.4.5 Literais de string (p: 62-63)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 3.1.4 Literais de string

### Veja também

[documentação C++](<#/>) para literal de string
---