# Constante de ponto flutuante

Permite que valores de tipo de ponto flutuante sejam usados diretamente em expressões.

### Sintaxe

Uma constante de ponto flutuante é uma expressão [não-lvalue](<#/doc/language/value_category>) com a forma:

---
significando expoente ﻿(opcional) sufixo ﻿(opcional)

Onde o significando tem a forma

---
parte-inteira ﻿(opcional) `.`(opcional) parte-fracionária ﻿(opcional)

O expoente tem a forma

---
`e` | `E` sinal-do-expoente ﻿(opcional) sequência-de-dígitos | (1) |
`p` | `P` sinal-do-expoente ﻿(opcional) sequência-de-dígitos | (2) | (desde C99)

1) A sintaxe do expoente para uma constante de ponto flutuante decimal

2) A sintaxe do expoente para uma constante de ponto flutuante hexadecimal

Aspas simples opcionais (`'`) podem ser inseridas entre os dígitos como um separador, elas são ignoradas durante a compilação. | (desde C23)

### Explicação

Se o significando começar com a sequência de caracteres `0x` ou `0X`, a constante de ponto flutuante é uma _constante de ponto flutuante hexadecimal_. Caso contrário, é uma _constante de ponto flutuante decimal_. Para uma _constante de ponto flutuante hexadecimal_, o significando é interpretado como um número racional hexadecimal, e a sequência de dígitos do expoente é interpretada como a potência inteira de 2 pela qual o significando deve ser escalado.
```
    double d = 0x1.2p3; // hex fraction 1.2 (decimal 1.125) scaled by 2^3, that is 9.0
```

| (desde C99)

Para uma _constante de ponto flutuante decimal_, o significando é interpretado como um número racional decimal, e a sequência de dígitos do expoente é interpretada como a potência inteira de 10 pela qual o significando deve ser escalado.
```
    double d = 1.2e3; // decimal fraction 1.2 scaled by 10^3, that is 1200.0
```

#### Sufixos

Uma constante de ponto flutuante sem sufixo tem o tipo double. Se o sufixo for a letra `f` ou `F`, a constante de ponto flutuante tem o tipo float. Se o sufixo for a letra `l` ou `L`, a constante de ponto flutuante tem o tipo long double.

Se a implementação predefinir a macro `__STDC_IEC_60559_BFP__`, os seguintes sufixos e constantes de ponto flutuante correspondentes são adicionalmente suportados:

  * se o sufixo for `df` ou `DF`, a constante de ponto flutuante tem o tipo _Decimal32;
  * se o sufixo for `dd` ou `DD`, a constante de ponto flutuante tem o tipo _Decimal64;
  * se o sufixo for `dl` ou `DL`, a constante de ponto flutuante tem o tipo _Decimal128.

Sufixos para tipos de ponto flutuante decimal não são permitidos em constantes de ponto flutuante hexadecimais. | (desde C23)

#### Partes opcionais

Se o expoente estiver presente e a parte fracionária não for usada, o separador decimal pode ser omitido:
```
    double x = 1e0; // floating-point 1.0 (period not used)
```

Para constantes de ponto flutuante decimais, a parte do expoente é opcional. Se for omitida, o ponto não é opcional, e a parte inteira ou a parte fracionária deve estar presente.
```
    double x = 1.; // floating-point 1.0 (fractional part optional)
    double y = .1; // floating-point 0.1 (whole-number part optional)
```

Para constantes de ponto flutuante hexadecimais, o expoente não é opcional para evitar ambiguidade resultante de um sufixo `f` ser confundido com um dígito hexadecimal. | (desde C99)

#### Valores representáveis

O resultado da avaliação de uma constante de ponto flutuante é o valor representável mais próximo ou o valor representável maior ou menor imediatamente adjacente ao valor representável mais próximo, escolhido de uma maneira definida pela implementação (em outras palavras, a [direção de arredondamento padrão](<#/doc/numeric/fenv/FE_round>) durante a tradução é definida pela implementação).

Todas as constantes de ponto flutuante da mesma forma de origem convertem para o mesmo formato interno com o mesmo valor. Constantes de ponto flutuante de diferentes formas de origem, por exemplo, 1.23 e 1.230, não precisam converter para o mesmo formato interno e valor.

Constantes de ponto flutuante podem converter para mais faixa e precisão do que o indicado por seu tipo, se indicado por [FLT_EVAL_METHOD](<#/doc/types/limits/FLT_EVAL_METHOD>). Por exemplo, a constante 0.1f pode agir como se fosse 0.1L em uma expressão. O resultado da avaliação de uma constante de ponto flutuante hexadecimal, se [FLT_RADIX](<#/doc/types/limits>) for 2, é o valor exato representado pela constante de ponto flutuante, corretamente arredondado para o tipo de destino. | (desde C99)
Constantes de ponto flutuante do tipo de ponto flutuante decimal que têm o mesmo valor numérico \\(\small x\\)x mas diferentes expoentes quânticos, por exemplo, 1230.dd, 1230.0dd e 1.23e3dd, têm representações internas distinguíveis. O expoente quântico \\(\small q\\)q de uma constante de ponto flutuante de um tipo de ponto flutuante decimal é determinado de forma que \\(\small 10^q\\)10q
represente 1 no lugar do último dígito do significando quando possível. Se o expoente quântico \\(\small q\\)q e o coeficiente \\(\small c = x\cdot 10^{-q}\\)c=x·10-q
determinados acima não puderem ser representados exatamente no tipo da constante de ponto flutuante, \\(\small q\\)q é aumentado conforme necessário dentro do limite do tipo, e \\(\small c\\)c é reduzido correspondentemente, com o arredondamento necessário. O arredondamento pode resultar em zero ou infinito. Se (o possivelmente arredondado) \\(\small c\\)c ainda estiver fora do intervalo permitido depois que \\(\small q\\)q atingir o valor máximo, a constante de ponto flutuante resultante terá o valor de infinito positivo. | (desde C23)

### Notas

A [direção de arredondamento](<#/doc/numeric/fenv/FE_round>) e a [precisão](<#/doc/types/limits/FLT_EVAL_METHOD>) padrão estão em vigor quando as constantes de ponto flutuante são convertidas em representações internas, e [exceções de ponto flutuante](<#/doc/numeric/fenv/FE_exceptions>) não são levantadas mesmo que [` #pragma STDC FENV_ACCESS`](<#/doc/preprocessor/impl>) esteja em vigor (para conversão de strings de caracteres em tempo de execução, [strtod](<#/doc/string/byte/strtof>) pode ser usado). Note que isso difere das [expressões constantes aritméticas](<#/doc/language/constant_expression>) de tipo flutuante.

As letras nas constantes de ponto flutuante não diferenciam maiúsculas de minúsculas, exceto que maiúsculas e minúsculas não podem ser usadas juntas em sufixos para tipos de ponto flutuante decimal (desde C23): 0x1.ep+3 e 0X1.EP+3 representam o mesmo valor de ponto flutuante 15.0.

O ponto decimal especificado por [setlocale](<#/doc/locale/setlocale>) não tem efeito na sintaxe das constantes de ponto flutuante: o caractere do ponto decimal é sempre o ponto.

Ao contrário dos inteiros, nem todo valor de ponto flutuante pode ser representado diretamente pela sintaxe de constante decimal ou mesmo hexadecimal (desde C99): macros [`NAN`](<#/doc/numeric/math/NAN>) e [`INFINITY`](<#/doc/numeric/math/INFINITY>), bem como funções como [nan](<#/doc/numeric/math/nan.2>), oferecem maneiras de gerar esses valores especiais (desde C99). Note que 0x1.FFFFFEp128f, que pode parecer ser um NaN de float IEEE, na verdade transborda para um infinito nesse formato.

Não existem constantes de ponto flutuante negativas; uma expressão como -1.2 é o [operador aritmético](<#/doc/language/operator_arithmetic>) menos unário aplicado à constante de ponto flutuante 1.2. Note que o valor especial zero negativo pode ser construído com -0.0.

### Exemplo

Execute este código
```
    #include <stdio.h>
     
    int main(void)
    {
        printf("15.0     = %a\n", 15.0);
        printf("0x1.ep+3 = %f\n", 0x1.ep+3);
     
        // Constants outside the range of type double.
        printf("+2.0e+308 --> %g\n",  2.0e+308);
        printf("+1.0e-324 --> %g\n",  1.0e-324);
        printf("-1.0e-324 --> %g\n", -1.0e-324);
        printf("-2.0e+308 --> %g\n", -2.0e+308);
    }
```

Saída:
```
    15.0     = 0x1.ep+3
    0x1.ep+3 = 15.000000
    +2.0e+308 --> inf
    +1.0e-324 --> 0
    -1.0e-324 --> -0
    -2.0e+308 --> -inf
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 6.4.4.2 Constantes de ponto flutuante (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 6.4.4.2 Constantes de ponto flutuante (p: 47-48)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 6.4.4.2 Constantes de ponto flutuante (p: 65-66)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 6.4.4.2 Constantes de ponto flutuante (p: 57-58)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 3.1.3.1 Constantes de ponto flutuante

### Veja também

[documentação C++](<#/>) para literal de ponto flutuante
---