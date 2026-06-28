# Constante inteira

Permite que valores de tipo inteiro sejam usados diretamente em expressões.

### Sintaxe

Uma constante inteira é uma expressão [não-lvalue](<#/doc/language/value_category>) da forma

---
constante-decimal sufixo-inteiro ﻿(opcional) | (1) |
constante-octal sufixo-inteiro ﻿(opcional) | (2) |
constante-hexadecimal sufixo-inteiro ﻿(opcional) | (3) |
constante-binária sufixo-inteiro ﻿(opcional) | (4) | (desde C23)

onde

  * constante-decimal é um dígito decimal não-zero (`1`, `2`, `3`, `4`, `5`, `6`, `7`, `8`, `9`), seguido por zero ou mais dígitos decimais (`0`, `1`, `2`, `3`, `4`, `5`, `6`, `7`, `8`, `9`)
  * constante-octal é o dígito zero (`0`) seguido por zero ou mais dígitos octais (`0`, `1`, `2`, `3`, `4`, `5`, `6`, `7`)
  * constante-hexadecimal é a sequência de caracteres `0x` ou a sequência de caracteres `0X` seguida por um ou mais dígitos hexadecimais (`0`, `1`, `2`, `3`, `4`, `5`, `6`, `7`, `8`, `9`, `a`, `A`, `b`, `B`, `c`, `C`, `d`, `D`, `e`, `E`, `f`, `F`)
  * constante-binária é a sequência de caracteres `0b` ou a sequência de caracteres `0B` seguida por um ou mais dígitos binários (`0`, `1`)
  * sufixo-inteiro, se fornecido, pode conter um dos seguintes (exceto que o prefixo unsigned pode ser combinado com um dos outros; se dois sufixos forem usados, eles podem aparecer em qualquer ordem):

    

  * sufixo-unsigned (o caractere `u` ou o caractere `U`)
  * sufixo-long (o caractere `l` ou o caractere `L`) ou o sufixo-long-long (a sequência de caracteres `ll` ou a sequência de caracteres `LL`) (desde C99)
  * sufixo-bit-precise-int (a sequência de caracteres `wb` ou a sequência de caracteres `WB`) (desde C23)

Aspas simples opcionais (`'`) podem ser inseridas entre os dígitos como um separador. Elas são ignoradas pelo compilador. | (desde C23)

### Explicação

1) Constante inteira decimal (base 10, o primeiro dígito é o mais significativo).

2) Constante inteira octal (base 8, o primeiro dígito é o mais significativo).

3) Constante inteira hexadecimal (base 16, o primeiro dígito é o mais significativo, as letras `a` a `f` representam os valores decimais de 10 a 15).

4) Constante inteira binária (base 2, o primeiro dígito é o mais significativo).

As seguintes variáveis são inicializadas com o mesmo valor:
```c
    int d = 42;
    int o = 052;
    int x = 0x2a;
    int X = 0X2A;
    int b = 0b101010; // C23
```

As seguintes variáveis também são inicializadas com o mesmo valor:
```c
    unsigned long long l1 = 18446744073709550592ull; // C99
    unsigned long long l2 = 18'446'744'073'709'550'592llu; // C23
    unsigned long long l3 = 1844'6744'0737'0955'0592uLL; // C23
    unsigned long long l4 = 184467'440737'0'95505'92LLU; // C23
```

### O tipo da constante inteira

O tipo da constante inteira é o primeiro tipo no qual o valor pode se encaixar, da lista de tipos que depende da base numérica e do sufixo inteiro utilizados.

Tipos permitidos para constantes inteiras sufixo | bases decimais | outras bases
sem sufixo | int long int unsigned long int (até C99) long long int (desde C99) | int unsigned int long int unsigned long int long long int (desde C99) unsigned long long int (desde C99)
`u` ou `U` | unsigned int unsigned long int unsigned long long int (desde C99) | unsigned int unsigned long int unsigned long long int (desde C99)
`l` ou `L` | long int unsigned long int (até C99) long long int (desde C99) | long int unsigned long int long long int (desde C99) unsigned long long int (desde C99)
ambos `l`/`L` e `u`/`U` | unsigned long int unsigned long long int (desde C99) | unsigned long int unsigned long long int (desde C99)
`ll` ou `LL` | long long int (desde C99) | long long int (desde C99) unsigned long long int (desde C99)
ambos `ll`/`LL` e `u`/`U` | unsigned long long int (desde C99) | unsigned long long int (desde C99)
`wb` ou `WB` | _BitInt(N) onde a largura N é o menor N maior que 1 que pode acomodar o valor e o bit de sinal (desde C23) | _BitInt(N) onde a largura N é o menor N maior que 1 que pode acomodar o valor e o bit de sinal (desde C23)
ambos `wb`/`WB` e `u`/`U` | unsigned _BitInt(N) onde a largura N é o menor N maior que 0 que pode acomodar o valor (desde C23) | unsigned _BitInt(N) onde a largura N é o menor N maior que 0 que pode acomodar o valor (desde C23)

Se o valor da constante inteira for muito grande para caber em qualquer um dos tipos permitidos pela combinação de sufixo/base, não tiver os sufixos `wb`, `WB`, `uwb` ou `UWB` (desde C23) e o compilador suportar tipos inteiros estendidos (como `__int128`), a constante pode receber o tipo inteiro estendido; caso contrário, o programa é malformado.

### Notas

As letras nas constantes inteiras não diferenciam maiúsculas de minúsculas: `0xDeAdBaBeU` e `0XdeadBABEu` representam o mesmo número (uma exceção é o sufixo long-long, que é `ll` ou `LL`, nunca `lL` ou `Ll`) (desde C99).

Não existem constantes inteiras negativas. Expressões como `-1` aplicam o [operador de menos unário](<#/doc/language/operator_arithmetic>) ao valor representado pela constante.

Quando usadas em uma expressão de controle de [` #if`](<#/doc/preprocessor/conditional>) ou [` #elif`](<#/doc/preprocessor/conditional>), todas as constantes inteiras com sinal agem como se tivessem o tipo [intmax_t](<#/doc/types/integer>) e todas as constantes inteiras sem sinal agem como se tivessem o tipo [uintmax_t](<#/doc/types/integer>). | (desde C99)

Constantes inteiras podem ser usadas em [expressões de constante inteira](<#/doc/language/constant_expression>).

Devido ao [maximal munch](<#/doc/language/translation_phases>), constantes inteiras hexadecimais terminadas em `e` e `E`, quando seguidas pelos operadores `+` ou `-`, devem ser separadas do operador por espaço em branco ou parênteses no código-fonte:
```c
    int x = 0xE+2;   // erro
    int y = 0xa+2;   // OK
    int z = 0xE +2;  // OK
    int q = (0xE)+2; // OK
```

Caso contrário, um único token de número de pré-processamento inválido é formado, o que faz com que a análise subsequente falhe.

### Exemplo

Execute este código
```c
    #include <inttypes.h>
    #include <stdio.h>
    
    int main(void)
    {
        printf("123 = %d\n", 123);
        printf("0123 = %d\n", 0123);
        printf("0x123 = %d\n", 0x123);
        printf("12345678901234567890ull = %llu\n", 12345678901234567890ull);
        // o tipo é um tipo de 64 bits (unsigned long long ou possivelmente unsigned long)
        // mesmo sem um sufixo long
        printf("12345678901234567890u = %"PRIu64"\n", 12345678901234567890u );
    
        // printf("%lld\n", -9223372036854775808); // Erro:
            // o valor 9223372036854775808 não cabe em signed long long, que
            // é o maior tipo permitido para constante inteira decimal sem sufixo
    
        printf("%llu\n", -9223372036854775808ull );
        // o menos unário aplicado a um valor unsigned o subtrai de 2^64,
        // isso resulta em unsigned 9223372036854775808
    
        printf("%lld\n", -9223372036854775807ll - 1);
        // maneira correta de formar o valor assinado -9223372036854775808
    }
```

Saída:
```
    123 = 123
    0123 = 83
    0x123 = 291
    12345678901234567890ull = 12345678901234567890
    12345678901234567890u = 12345678901234567890
    9223372036854775808
    -9223372036854775808
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 6.4.4.1 Constantes inteiras (p: 57-60)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 6.4.4.1 Constantes inteiras (p: 45-46)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 6.4.4.1 Constantes inteiras (p: 62-64)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 6.4.4.1 Constantes inteiras (p: 54-56)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 3.1.3.2 Constantes inteiras

### Veja também

[Documentação C++](<#/>) para Literal inteiro
---