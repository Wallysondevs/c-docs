# Tipos aritméticos

(Veja também [tipo](<#/doc/language/compatible_type>) para uma visão geral do sistema de tipos e [a lista de utilitários relacionados a tipos](<#/doc/types>) fornecidos pela biblioteca C.)

### Tipo booleano

*   `_Bool` (também acessível como a macro [`bool`](<#/doc/types>))(até C23)`bool`(desde C23) — tipo, capaz de armazenar um dos dois valores: 1 e `0` (também acessível como as macros [`true`](<#/doc/types>) e [`false`](<#/doc/types>))(até C23)`true` e `false`(desde C23).

Note que a [conversão](<#/doc/language/conversion>) para `_Bool`(até C23)`bool`(desde C23) não funciona da mesma forma que a conversão para outros tipos inteiros: `(bool)0.5` avalia para `true`, enquanto `(int)0.5` avalia para `0`. | (desde C99)

### Tipos de caracteres

*   `signed char` — tipo para representação de caracteres com sinal.
*   `unsigned char` — tipo para representação de caracteres sem sinal. Também usado para inspecionar [representações de objetos](<#/doc/language/object>) (memória bruta).
*   `char` — tipo para representação de caracteres. Equivalente a `signed char` ou `unsigned char` (qual deles é definido pela implementação e pode ser controlado por uma opção de linha de comando do compilador), mas `char` é um tipo distinto, diferente de `signed char` e `unsigned char`.

Note que a biblioteca padrão também define nomes [typedef](<#/doc/language/typedef>) [`wchar_t`](<#/doc/string/wide>), [`char16_t`](<#/doc/string/multibyte>) e [`char32_t`](<#/doc/string/multibyte>)(desde C11) para representar caracteres largos e [`char8_t`](<#/doc/string/multibyte>) para caracteres UTF-8(desde C23).

### Tipos inteiros

*   `short int` (também acessível como `short`, pode usar a palavra-chave `signed`)
*   `unsigned short int` (também acessível como `unsigned short`)
*   `int` (também acessível como `signed int`)

    Este é o tipo inteiro mais otimizado para a plataforma e tem garantia de ter pelo menos 16 bits. A maioria dos sistemas atuais usa 32 bits (veja Modelos de Dados abaixo).

*   `unsigned int` (também acessível como `unsigned`), a contraparte sem sinal de `int`, implementando aritmética modular. Adequado para manipulações de bits.
*   `long int` (também acessível como `long`)
*   `unsigned long int` (também acessível como `unsigned long`)

*   `long long int` (também acessível como `long long`)
*   `unsigned long long int` (também acessível como `unsigned long long`)

| (desde C99)

*   `_BitInt(n)` (também acessível como `signed _BitInt(n)`), os tipos inteiros com precisão de bit com sinal (onde `n` é substituído por uma expressão constante inteira que denota a largura precisa (incluindo o bit de sinal), que não pode ser maior que `BITINT_MAXWIDTH` de [`<limits.h>`](<#/doc/types/limits>))
*   `unsigned _BitInt(n)`, os tipos inteiros com precisão de bit sem sinal (onde `n` é substituído por uma expressão constante inteira que denota a largura precisa, que não pode ser maior que `BITINT_MAXWIDTH` de [`<limits.h>`](<#/doc/types/limits>))

| (desde C23)

Nota: assim como em todos os especificadores de tipo, qualquer ordem é permitida: `unsigned long long int` e `long int unsigned long` nomeiam o mesmo tipo.

A tabela a seguir resume todos os tipos inteiros disponíveis e suas propriedades:

Especificador de tipo | Tipo equivalente | Largura em bits por modelo de dados
Padrão C | LP32 | ILP32 | LLP64 | LP64
`char` | `char` | pelo menos
**8** | **8** | **8** | **8** | **8**
`signed char` | `signed char`
`unsigned char` | `unsigned char`
`short` | `short int` | pelo menos
**16** | **16** | **16** | **16** | **16**
`short int`
`signed short`
`signed short int`
`unsigned short` | `unsigned short int`
`unsigned short int`
`int` | `int` | pelo menos
**16** | **16** | **32** | **32** | **32**
`signed`
`signed int`
`unsigned` | `unsigned int`
`unsigned int`
`long` | `long int` | pelo menos
**32** | **32** | **32** | **32** | **64**
`long int`
`signed long`
`signed long int`
`unsigned long` | `unsigned long int`
`unsigned long int`
`long long` | `long long int`
(C99) | pelo menos
**64** | **64** | **64** | **64** | **64**
`long long int`
`signed long long`
`signed long long int`
`unsigned long long` | `unsigned long long int`
(C99)
`unsigned long long int`

Além das contagens mínimas de bits, o Padrão C garante que

`1 == sizeof(char) ≤ sizeof(short) ≤ sizeof(int) ≤ sizeof(long) ≤ sizeof(long long).`

Nota: isso permite o caso extremo em que [bytes](<https://en.wikipedia.org/wiki/byte> "enwiki:byte") têm 64 bits, todos os tipos (incluindo `char`) têm 64 bits de largura, e `sizeof` retorna 1 para cada tipo.

Nota: a aritmética de inteiros é definida de forma diferente para os tipos inteiros com e sem sinal. Veja [operadores aritméticos](<#/doc/language/operator_arithmetic>), em particular [overflows de inteiros](<#/doc/language/operator_arithmetic>).

#### Modelos de Dados

As escolhas feitas por cada implementação sobre os tamanhos dos tipos fundamentais são coletivamente conhecidas como _modelo de dados_. Quatro modelos de dados encontraram ampla aceitação:

Sistemas de 32 bits:

*   **LP32** ou **2/4/4** (`int` é de 16 bits, `long` e `pointer` são de 32 bits)

    *   Win16 API

*   **ILP32** ou **4/4/4** (`int`, `long` e `pointer` são de 32 bits);

    *   Win32 API
    *   Sistemas Unix e semelhantes a Unix (Linux, Mac OS X)

Sistemas de 64 bits:

*   **LLP64** ou **4/4/8** (`int` e `long` são de 32 bits, `pointer` é de 64 bits)

    *   Win64 API

*   **LP64** ou **4/8/8** (`int` é de 32 bits, `long` e `pointer` são de 64 bits)

    *   Sistemas Unix e semelhantes a Unix (Linux, Mac OS X)

Outros modelos são muito raros. Por exemplo, **ILP64** (**8/8/8** : `int`, `long` e `pointer` são de 64 bits) apareceu apenas em alguns sistemas Unix de 64 bits antigos (por exemplo, [Unicos em Cray](<https://en.wikipedia.org/wiki/UNICOS> "enwiki:UNICOS")).

Note que tipos inteiros de largura exata estão disponíveis em [`<stdint.h>`](<#/doc/types/integer>) desde C99.

### Tipos de ponto flutuante reais

C possui três ou seis(desde C23) tipos para representar valores de ponto flutuante reais:

*   `float` — tipo de ponto flutuante de precisão simples. Corresponde ao [formato IEEE-754 binary32](<https://en.wikipedia.org/wiki/Single-precision_floating-point_format> "enwiki:Single-precision floating-point format") se suportado.
*   `double` — tipo de ponto flutuante de precisão dupla. Corresponde ao [formato IEEE-754 binary64](<https://en.wikipedia.org/wiki/Double-precision_floating-point_format> "enwiki:Double-precision floating-point format") se suportado.
*   `long double` — tipo de ponto flutuante de precisão estendida. Corresponde ao [formato IEEE-754 binary128](<https://en.wikipedia.org/wiki/Quadruple-precision_floating-point_format> "enwiki:Quadruple-precision floating-point format") se suportado, caso contrário, corresponde ao [formato IEEE-754 binary64-extended](<https://en.wikipedia.org/wiki/Extended_precision> "enwiki:Extended precision") se suportado, caso contrário, corresponde a algum formato de ponto flutuante estendido não-IEEE-754, desde que sua precisão seja melhor que binary64 e o intervalo seja pelo menos tão bom quanto binary64, caso contrário, corresponde ao formato IEEE-754 binary64.
    *   O formato binary128 é usado por algumas implementações HP-UX, SPARC, MIPS, ARM64 e z/OS.
    *   O formato IEEE-754 binary64-extended mais conhecido é o formato de precisão estendida x87 de 80 bits. Ele é usado por muitas implementações x86 e x86-64 (uma exceção notável é o MSVC, que implementa `long double` no mesmo formato que `double`, ou seja, binary64).

    Se a implementação predefinir a macro constante `__STDC_IEC_60559_DFP__`, os seguintes tipos de ponto flutuante decimais também são suportados.

*   `_Decimal32` — Representa o [formato IEEE-754 decimal32](<https://en.wikipedia.org/wiki/decimal32_floating-point_format> "enwiki:decimal32 floating-point format").
*   `_Decimal64` — Representa o [formato IEEE-754 decimal64](<https://en.wikipedia.org/wiki/decimal64_floating-point_format> "enwiki:decimal64 floating-point format").
*   `_Decimal128` — Representa o [formato IEEE-754 decimal128](<https://en.wikipedia.org/wiki/decimal128_floating-point_format> "enwiki:decimal128 floating-point format").

    Caso contrário, esses tipos de ponto flutuante decimais não são suportados.
| (desde C23)

Tipos de ponto flutuante podem suportar valores especiais:

*   _infinito_ (positivo e negativo), veja [`INFINITY`](<#/doc/numeric/math/INFINITY>)
*   o _zero negativo_ , -0.0. Ele se compara como igual ao zero positivo, mas é significativo em algumas operações aritméticas, por exemplo, `1.0 / 0.0 == INFINITY`, mas `1.0 / -0.0 == -INFINITY`)
*   _não-é-um-número_ (NaN), que não se compara como igual a nada (incluindo a si mesmo). Múltiplos padrões de bits representam NaNs, veja [nan](<#/doc/numeric/math/nan.2>), [`NAN`](<#/doc/numeric/math/NAN>). Note que C não dá atenção especial aos NaNs sinalizadores (especificados por IEEE-754), e trata todos os NaNs como silenciosos.

Números de ponto flutuante reais podem ser usados com [operadores aritméticos](<#/doc/language/operator_arithmetic>) `+` `-` `/` `*` e várias funções matemáticas de [`<math.h>`](<#/doc/numeric/math>). Tanto os operadores embutidos quanto as funções da biblioteca podem levantar exceções de ponto flutuante e definir [errno](<#/doc/error/errno>) conforme descrito em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Expressões de ponto flutuante podem ter maior intervalo e precisão do que o indicado por seus tipos, veja [FLT_EVAL_METHOD](<#/doc/types/limits/FLT_EVAL_METHOD>). [Atribuição](<#/doc/language/operator_assignment>), [retorno](<#/doc/language/return>) e [conversão explícita (cast)](<#/doc/language/cast>) forçam o intervalo e a precisão para aqueles associados ao tipo declarado.

Expressões de ponto flutuante também podem ser _contraídas_ , ou seja, calculadas como se todos os valores intermediários tivessem intervalo e precisão infinitos, veja [` #pragma STDC FP_CONTRACT`](<#/doc/preprocessor/impl>).

Algumas operações em números de ponto flutuante são afetadas e modificam o estado do [ambiente de ponto flutuante](<#/doc/numeric/fenv>) (mais notavelmente, a direção de arredondamento).

[Conversões implícitas](<#/doc/language/conversion>) são definidas entre tipos de ponto flutuante reais e tipos inteiros, complexos e imaginários.

Veja [Limites dos tipos de ponto flutuante](<#/doc/types/limits>) e a biblioteca [`<math.h>`](<#/doc/numeric/math>) para detalhes adicionais, limites e propriedades dos tipos de ponto flutuante.

### Tipos de ponto flutuante complexos

Tipos de ponto flutuante complexos modelam o [número complexo](<https://en.wikipedia.org/wiki/complex_number> "enwiki:complex number") matemático, ou seja, os números que podem ser escritos como a soma de um número real e um número real multiplicado pela unidade imaginária: a + bi Os três tipos complexos são

*   `float _Complex` (também disponível como `float [complex](<#/doc/numeric/complex/complex>)` se [`<complex.h>`](<#/doc/numeric/complex>) for incluído)
*   `double _Complex` (também disponível como `double [complex](<#/doc/numeric/complex/complex>)` se [`<complex.h>`](<#/doc/numeric/complex>) for incluído)
*   `long double _Complex` (também disponível como `long double [complex](<#/doc/numeric/complex/complex>)` se [`<complex.h>`](<#/doc/numeric/complex>) for incluído)

Nota: assim como em todos os especificadores de tipo, qualquer ordem é permitida: `long double [complex](<#/doc/numeric/complex/complex>)`, `[complex](<#/doc/numeric/complex/complex>) long double`, e até mesmo `double [complex](<#/doc/numeric/complex/complex>) long` nomeiam o mesmo tipo. Execute este código
```c
#include <complex.h>
#include <stdio.h>
 
int main(void)
{
    double complex z = 1 + 2*I;
    z = 1 / z;
    printf("1/(1.0+2.0i) = %.1f%+.1fi\n", creal(z), cimag(z));
}
```

Saída:
```
1/(1.0+2.0i) = 0.2-0.4i
```

| Se a macro constante `__STDC_NO_COMPLEX__` for definida pela implementação, os tipos complexos (bem como o cabeçalho da biblioteca [`<complex.h>`](<#/doc/numeric/complex>)) não são fornecidos. | (desde C11)

Cada tipo complexo tem a mesma [representação de objeto](<#/doc/language/object>) e [requisitos de alinhamento](<#/doc/language/object>) que um [array](<#/doc/language/array>) de dois elementos do tipo real correspondente (`float` para `float [complex](<#/doc/numeric/complex/complex>)`, `double` para `double [complex](<#/doc/numeric/complex/complex>)`, `long double` para `long double [complex](<#/doc/numeric/complex/complex>)`). O primeiro elemento do array contém a parte real, e o segundo elemento do array contém o componente imaginário.
```c
float a[4] = {1, 2, 3, 4};
float complex z1, z2;
memcpy(&z1, a, sizeof z1); // z1 becomes 1.0 + 2.0i
memcpy(&z2, a+2, sizeof z2); // z2 becomes 3.0 + 4.0i
```

Números complexos podem ser usados com [operadores aritméticos](<#/doc/language/operator_arithmetic>) `+` `-` `*` e `/`, possivelmente misturados com números imaginários e reais. Existem muitas funções matemáticas definidas para números complexos em [`<complex.h>`](<#/doc/numeric/complex>). Tanto os operadores embutidos quanto as funções da biblioteca podem levantar exceções de ponto flutuante e definir [errno](<#/doc/error/errno>) conforme descrito em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Incremento e decremento não são definidos para tipos complexos.

Operadores relacionais não são definidos para tipos complexos (não há noção de "menor que").

| Esta seção está incompleta
Razão: revisar outras operações, linkar biblioteca |
[Conversões implícitas](<#/doc/language/conversion>) são definidas entre tipos complexos e outros tipos aritméticos.

A fim de suportar o modelo de um-infinito da aritmética de números complexos, C considera qualquer valor complexo com pelo menos uma parte infinita como um infinito, mesmo que sua outra parte seja um NaN, garante que todos os operadores e funções honrem as propriedades básicas dos infinitos e fornece [cproj](<#/doc/numeric/complex/cproj>) para mapear todos os infinitos para o canônico (veja [operadores aritméticos](<#/doc/language/operator_arithmetic>) para as regras exatas).

Execute este código
```c
#include <complex.h>
#include <math.h>
#include <stdio.h>
 
int main(void)
{
    double complex z = (1 + 0*I) * (INFINITY + I*INFINITY);
//  textbook formula would give
//  (1+i0)(∞+i∞) ⇒ (1×∞ – 0×∞) + i(0×∞+1×∞) ⇒ NaN + I*NaN
//  but C gives a complex infinity
    printf("%f%+f*i\n", creal(z), cimag(z));
 
//  textbook formula would give
//  cexp(∞+iNaN) ⇒ exp(∞)×(cis(NaN)) ⇒ NaN + I*NaN
//  but C gives  ±∞+i*nan
    double complex y = cexp(INFINITY + I*NAN);
    printf("%f%+f*i\n", creal(y), cimag(y));
}
```

Saída possível:
```
inf+inf*i 
inf+nan*i
```

C também trata múltiplos infinitos de forma a preservar informações direcionais sempre que possível, apesar das limitações inerentes da representação cartesiana:

multiplicar a unidade imaginária por infinito real resulta no infinito imaginário com o sinal correto: i × ∞ = i∞. Além disso, i × (∞ – i∞) = ∞ + i∞ indica o quadrante razoável.

| Esta seção está incompleta
Razão: redação |

### Tipos de ponto flutuante imaginários

Tipos de ponto flutuante imaginários modelam os [números imaginários](<https://en.wikipedia.org/wiki/imaginary_numbers> "enwiki:imaginary numbers") matemáticos, ou seja, números que podem ser escritos como um número real multiplicado pela unidade imaginária: bi Os três tipos imaginários são

*   `float _Imaginary` (também disponível como `float [imaginary](<#/doc/numeric/complex/imaginary>)` se [`<complex.h>`](<#/doc/numeric/complex>) for incluído)
*   `double _Imaginary` (também disponível como `double [imaginary](<#/doc/numeric/complex/imaginary>)` se [`<complex.h>`](<#/doc/numeric/complex>) for incluído)
*   `long double _Imaginary` (também disponível como `long double [imaginary](<#/doc/numeric/complex/imaginary>)` se [`<complex.h>`](<#/doc/numeric/complex>) for incluído)

Nota: assim como em todos os especificadores de tipo, qualquer ordem é permitida: `long double [imaginary](<#/doc/numeric/complex/imaginary>)`, `[imaginary](<#/doc/numeric/complex/imaginary>) long double`, e até mesmo `double [imaginary](<#/doc/numeric/complex/imaginary>) long` nomeiam o mesmo tipo.

Execute este código
```c
#include <complex.h>
#include <stdio.h>
 
int main(void)
{
    double imaginary z = 3*I;
    z = 1 / z;
    printf("1/(3.0i) = %+.1fi\n", cimag(z));
}
```

Saída:
```
1/(3.0i) = -0.3i
```

Uma implementação que define `__STDC_IEC_559_COMPLEX__` é recomendada, mas não é obrigada a suportar números imaginários. POSIX recomenda verificar se a macro `_Imaginary_I` está definida para identificar o suporte a números imaginários. | (até C11)
Números imaginários são suportados se `__STDC_IEC_559_COMPLEX__`(até C23)`__STDC_IEC_60559_COMPLEX__`(desde C23) for definido. | (desde C11)

Cada um dos três tipos imaginários tem a mesma [representação de objeto](<#/doc/language/object>) e [requisito de alinhamento](<#/doc/language/object>) que seu _tipo real correspondente_ (`float` para `float [imaginary](<#/doc/numeric/complex/imaginary>)`, `double` para `double [imaginary](<#/doc/numeric/complex/imaginary>)`, `long double` para `long double [imaginary](<#/doc/numeric/complex/imaginary>)`).

Nota: apesar disso, os tipos imaginários são distintos e [não compatíveis](<#/doc/language/compatible_type>) com seus tipos reais correspondentes, o que proíbe o aliasing.

Números imaginários podem ser usados com [operadores aritméticos](<#/doc/language/operator_arithmetic>) `+` `-` `*` e `/`, possivelmente misturados com números complexos e reais. Existem muitas funções matemáticas definidas para números imaginários em [`<complex.h>`](<#/doc/numeric/complex>). Tanto os operadores embutidos quanto as funções da biblioteca podem levantar exceções de ponto flutuante e definir [errno](<#/doc/error/errno>) conforme descrito em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Incremento e decremento não são definidos para tipos imaginários.

| Esta seção está incompleta
Razão: revisar outras operações, linkar biblioteca |
[Conversões implícitas](<#/doc/language/conversion>) são definidas entre tipos imaginários e outros tipos aritméticos.

Os números imaginários tornam possível expressar todos os números complexos usando a notação natural `x + I*y` (onde `I` é definido como `_Imaginary_I`). Sem os tipos imaginários, certos valores complexos especiais não podem ser criados naturalmente. Por exemplo, se `I` for definido como `_Complex_I`, então escrever `0.0 + I*INFINITY` resulta em `NaN` como a parte real, e `CMPLX(0.0, INFINITY)` deve ser usado em vez disso. O mesmo vale para os números com o componente imaginário zero negativo, que são significativos ao trabalhar com as funções da biblioteca com cortes de ramo, como `csqrt`: `1.0 - 0.0*I` resulta no componente imaginário zero positivo se `I` for definido como `_Complex_I` e a parte imaginária zero negativa requer o uso de `CMPLX` ou `conj`.

Tipos imaginários também simplificam implementações; a multiplicação de um imaginário por um complexo pode ser implementada diretamente com duas multiplicações se os tipos imaginários forem suportados, em vez de quatro multiplicações e duas adições.

(desde C99)

### Palavras-chave

*   [`bool`](<#/doc/keyword/bool>), [`true`](<#/doc/keyword/true>), [`false`](<#/doc/keyword/false>), [`char`](<#/doc/keyword/char>), [`int`](<#/doc/keyword/int>), [`short`](<#/doc/keyword/short>), [`long`](<#/doc/keyword/long>), [`signed`](<#/doc/keyword/signed>), [`unsigned`](<#/doc/keyword/unsigned>), [`float`](<#/doc/keyword/float>), [`double`](<#/doc/keyword/double>).
*   [`_Bool`](<#/doc/keyword/_Bool>), [`_BitInt`](<https://en.cppreference.com/mwiki/index.php?title=c/keyword/_BitInt&action=edit&redlink=1> "c/keyword/ BitInt \(page does not exist\)"), [`_Complex`](<#/doc/keyword/_Complex>), [`_Imaginary`](<#/doc/keyword/_Imaginary>), [`_Decimal32`](<#/doc/keyword/_Decimal32>), [`_Decimal64`](<#/doc/keyword/_Decimal64>), [`_Decimal128`](<#/doc/keyword/_Decimal128>).

### Intervalo de valores

A tabela a seguir fornece uma referência para os limites das representações numéricas comuns.

Antes de C23, o Padrão C permitia qualquer representação de inteiro com sinal, e o intervalo mínimo garantido de inteiros com sinal de N bits era de \\(\scriptsize -(2^{N-1}-1)\\)-(2N-1 -1) a \\(\scriptsize +2^{N-1}-1\\)+2N-1 -1 (por exemplo, **-127** a **127** para um tipo de 8 bits com sinal), o que corresponde aos limites do [complemento de um](<https://en.wikipedia.org/wiki/one%27s_complement> "enwiki:one's complement") ou [sinal e magnitude](<https://en.wikipedia.org/wiki/Signed_number_representations#Sign-and-magnitude_method> "enwiki:Signed number representations").

No entanto, todos os modelos de dados populares (incluindo todos os ILP32, LP32, LP64, LLP64) e quase todos os compiladores C usam a representação de [complemento de dois](<https://en.wikipedia.org/wiki/two%27s_complement> "enwiki:two's complement") (as únicas exceções conhecidas são alguns compiladores para UNISYS), e a partir de C23, é a única representação permitida pelo padrão, com o intervalo garantido de \\(\scriptsize -2^{N-1}\\)-2N-1 a \\(\scriptsize +2^{N-1}-1\\)+2N-1 -1 (por exemplo, **-128** a **127** para um tipo de 8 bits com sinal).

Tipo | Tamanho em bits | Formato | Intervalo de valores
 | | | Aproximado | Exato
caractere | 8 | com sinal | | **−128** a **127**
 | | sem sinal | | **0** a **255**
 | 16 | UTF-16 | | **0** a **65535**
 | 32 | UTF-32 | | **0** a **1114111** (**0x10ffff**)
inteiro | 16 | com sinal | **± 3.27 · 10 4** | **−32768** a **32767**
 | | sem sinal | **0** a **6.55 · 10 4** | **0** a **65535**
 | 32 | com sinal | **± 2.14 · 10 9** | **−2,147,483,648** a **2,147,483,647**
 | | sem sinal | **0** a **4.29 · 10 9** | **0** a **4,294,967,295**
 | 64 | com sinal | **± 9.22 · 10 18** | **−9,223,372,036,854,775,808** a **9,223,372,036,854,775,807**
 | | sem sinal | **0** a **1.84 · 10 19** | **0** a **18,446,744,073,709,551,615**
ponto flutuante binário | 32 | [IEEE-754](<https://en.wikipedia.org/wiki/Single-precision_floating-point_format> "enwiki:Single-precision floating-point format") |
  * mínimo subnormal:
**± 1.401,298,4 · 10 −45**
  * mínimo normal:
**± 1.175,494,3 · 10 −38**
  * máximo:
**± 3.402,823,4 · 10 38**

|
  * mínimo subnormal:
**±0x1p−149**
  * mínimo normal:
**±0x1p−126**
  * máximo:
**±0x1.fffffep+127**

|
 | 64 | [IEEE-754](<https://en.wikipedia.org/wiki/Double-precision_floating-point_format> "enwiki:Double-precision floating-point format") |
  * mínimo subnormal:
**± 4.940,656,458,412 · 10 −324**
  * mínimo normal:
**± 2.225,073,858,507,201,4 · 10 −﻿308**
  * máximo:
**± 1.797,693,134,862,315,7 · 10 308**

|
  * mínimo subnormal:
**±0x1p−1074**
  * mínimo normal:
**±0x1p−1022**
  * máximo:
**±0x1.fffffffffffffp+1023**

|
 | 80[note 1](<#/doc/language/arithmetic_types>) | [x86](<https://en.wikipedia.org/wiki/Extended_precision> "enwiki:Extended precision") |
  * mínimo subnormal:
**± 3.645,199,531,882,474,602,528
· 10−4951**
  * mínimo normal:
**± 3.362,103,143,112,093,506,263
· 10−4932**
  * máximo:
**± 1.189,731,495,357,231,765,021
· 104932**

|
  * mínimo subnormal:
**±0x1p−16445**
  * mínimo normal:
**±0x1p−16382**
  * máximo:
**±0x1.fffffffffffffffep+16383**

|
 | 128 | [IEEE-754](<https://en.wikipedia.org/wiki/Quadruple-precision_floating-point_format> "enwiki:Quadruple-precision floating-point format") |
  * mínimo subnormal:
**± 6.475,175,119,438,025,110,924,
438,958,227,646,552,5 · 10−4966**
  * mínimo normal:
**± 3.362,103,143,112,093,506,262,
677,817,321,752,602,6 · 10−4932**
  * máximo:
**± 1.189,731,495,357,231,765,085,
759,326,628,007,016,2 · 104932**

|
  * mínimo subnormal:
**±0x1p−16494**
  * mínimo normal:
**±0x1p−16382**
  * máximo:
**±0x1.ffffffffffffffffffffffffffff
p+16383**

|
ponto flutuante decimal | 32 | [IEEE-754](<https://en.wikipedia.org/wiki/decimal32_floating-point_format> "enwiki:decimal32 floating-point format")
  * mínimo subnormal:
**± 1 · 10 -101**
  * mínimo normal:
**± 1 · 10 -95**
  * máximo:
**± 9.999'999 · 10 96**

|
 | 64 | [IEEE-754](<https://en.wikipedia.org/wiki/decimal64_floating-point_format> "enwiki:decimal64 floating-point format")
  * mínimo subnormal:
**± 1 · 10 -398**
  * mínimo normal:
**± 1 · 10 -383**
  * máximo:
**± 9.999'999'999'999'999 · 10 384**

|
 | 128 | [IEEE-754](<https://en.wikipedia.org/wiki/decimal128_floating-point_format> "enwiki:decimal128 floating-point format")
  * mínimo subnormal:
**± 1 · 10 -6176**
  * mínimo normal:
**± 1 · 10 -6143**
  * máximo:
**± 9.999'999'999'999'999'999'
999'999'999'999'999 · 106144**

|

1.  [↑](<#/doc/language/arithmetic_types>) A representação do objeto geralmente ocupa 96/128 bits em plataformas de 32/64 bits, respectivamente.

Nota: intervalos reais (em oposição aos mínimos garantidos) estão disponíveis nos cabeçalhos da biblioteca [`<limits.h>`](<#/doc/types/limits>) e [`<float.h>`](<#/doc/types/limits>).

### Veja também

[Documentação C++](<#/>) para Tipos Fundamentais
---