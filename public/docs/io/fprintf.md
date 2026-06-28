# printf, fprintf, sprintf, snprintf, printf_s, fprintf_s, sprintf_s, snprintf_s

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
int printf( const char* format, ... );  // até C99
int printf( const char* restrict format, ... );  // desde C99
int fprintf( FILE* stream, const char* format, ... );  // até C99
int fprintf( FILE* restrict stream, const char* restrict format, ... );  // desde C99
int sprintf( char* buffer, const char* format, ... );  // até C99
int sprintf( char* restrict buffer, const char* restrict format, ... );  // desde C99
int snprintf( char* restrict buffer, size_t bufsz,
const char* restrict format, ... );  // desde C99
int printf_s( const char* restrict format, ... );  // desde C11
int fprintf_s( FILE* restrict stream, const char* restrict format, ... );  // desde C11
int sprintf_s( char* restrict buffer, rsize_t bufsz,
const char* restrict format, ... );  // desde C11
int snprintf_s( char* restrict buffer, rsize_t bufsz,
const char* restrict format, ... );  // desde C11
```

Carrega os dados dos locais fornecidos, converte-os para equivalentes de string de caracteres e escreve os resultados em uma variedade de destinos/fluxos:

1) Escreve os resultados no fluxo de saída [stdout](<#/doc/io/std_streams>).

2) Escreve os resultados no fluxo de saída stream.

3) Escreve os resultados em um buffer de string de caracteres. O comportamento é indefinido se a string a ser escrita (mais o caractere nulo de terminação) exceder o tamanho do array apontado por buffer.

4) Escreve os resultados em um buffer de string de caracteres. No máximo bufsz - 1 caracteres são escritos. A string de caracteres resultante será terminada com um caractere nulo, a menos que bufsz seja zero. Se bufsz for zero, nada é escrito e buffer pode ser um ponteiro nulo; no entanto, o valor de retorno (número de bytes que seriam escritos, não incluindo o terminador nulo) ainda é calculado e retornado.

5-8) O mesmo que (1-4), exceto que os seguintes erros são detectados em tempo de execução e chamam a função [manipulador de restrição](<#/doc/error/set_constraint_handler_s>) atualmente instalada:

* o especificador de conversão `%n` está presente em format
* qualquer um dos argumentos correspondentes a `%s` é um ponteiro nulo
* stream ou format ou buffer é um ponteiro nulo
* bufsz é zero ou maior que RSIZE_MAX
* erros de codificação ocorrem em qualquer um dos especificadores de conversão de string e caractere
* (apenas para `sprintf_s`), a string a ser armazenada em buffer (incluindo o nulo final) excederia bufsz.

Assim como todas as funções com verificação de limites, `printf_s`, `fprintf_s`, `sprintf_s` e `snprintf_s` são garantidas de estarem disponíveis apenas se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir [`<stdio.h>`](<#/doc/io>).

### Parâmetros

- **stream** — fluxo de arquivo de saída para escrever
- **buffer** — ponteiro para uma string de caracteres para escrever
- **bufsz** — até bufsz - 1 caracteres podem ser escritos, mais o terminador nulo
- **format** — ponteiro para uma string de bytes terminada em nulo especificando como interpretar os dados
- **...** — argumentos especificando os dados a serem impressos. Se qualquer argumento após as [promoções de argumento padrão](<#/doc/language/conversion>) não for do tipo esperado pela especificação de conversão correspondente (o tipo esperado é o tipo promovido ou um tipo compatível com o tipo promovido), ou se houver menos argumentos do que o exigido por format, o comportamento é indefinido. Se houver mais argumentos do que o exigido por format, os argumentos extras são avaliados e ignorados.

A string **format** consiste em caracteres de byte comuns (exceto `%`), que são copiados inalterados para o fluxo de saída, e especificações de conversão. Cada especificação de conversão tem o seguinte formato:

* caractere `%` introdutório.

* (opcional) uma ou mais flags que modificam o comportamento da conversão:

* `-`: o resultado da conversão é justificado à esquerda dentro do campo (por padrão, é justificado à direita).
* `+`: o sinal de conversões com sinal é sempre prefixado ao resultado da conversão (por padrão, o resultado é precedido por menos apenas quando é negativo).
* _espaço_ : se o resultado de uma conversão com sinal não começar com um caractere de sinal, ou estiver vazio, um espaço é prefixado ao resultado. É ignorado se a flag `+` estiver presente.
* `#`: _forma alternativa_ da conversão é realizada. Veja a tabela abaixo para os efeitos exatos, caso contrário, o comportamento é indefinido.
* `0`: para conversões de números inteiros e de ponto flutuante, zeros à esquerda são usados para preencher o campo em vez de caracteres de _espaço_. Para números inteiros, é ignorado se a precisão for explicitamente especificada. Para outras conversões, o uso desta flag resulta em comportamento indefinido. É ignorado se a flag `-` estiver presente.

* (opcional) valor inteiro ou `*` que especifica a largura mínima do campo. O resultado é preenchido com caracteres de _espaço_ (por padrão), se necessário, à esquerda quando justificado à direita, ou à direita se justificado à esquerda. No caso em que `*` é usado, a largura é especificada por um argumento adicional do tipo int, que aparece antes do argumento a ser convertido e do argumento que fornece a precisão, se houver. Se o valor do argumento for negativo, resulta na flag `-` especificada e largura de campo positiva (Nota: Esta é a largura mínima: O valor nunca é truncado).

* (opcional) `.` seguido por um número inteiro ou `*`, ou nenhum, que especifica a _precisão_ da conversão. No caso em que `*` é usado, a _precisão_ é especificada por um argumento adicional do tipo int, que aparece antes do argumento a ser convertido, mas depois do argumento que fornece a largura mínima do campo, se houver. Se o valor deste argumento for negativo, ele é ignorado. Se nem um número nem `*` for usado, a precisão é considerada zero. Veja a tabela abaixo para os efeitos exatos da _precisão_.

* (opcional) _modificador de comprimento_ que especifica o tamanho do argumento (em combinação com o especificador de formato de conversão, ele especifica o tipo do argumento correspondente).

* especificador de formato de conversão.

Os seguintes especificadores de formato estão disponíveis:

Especificador de
Conversão | Explicação | Tipo de
Argumento Esperado
**Modificador de
Comprimento****→** | `hh` (C99) | `h` | (nenhum) | `l` | `ll` (C99) | `j` (C99) | `z` (C99) | `t` (C99) | `L`
`%` | Escreve o literal `%`. A especificação de conversão completa deve ser `%%`. | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A
`c` |

    Escreve um **único caractere**.
O argumento é primeiro convertido para unsigned char. Se o modificador **l** for usado, o argumento é primeiro convertido para uma string de caracteres como se por **%ls** com um argumento wchar_t[2]. | N/A | N/A | int | wint_t | N/A | N/A | N/A | N/A | N/A
`s` |

    Escreve uma **string de caracteres**
O argumento deve ser um ponteiro para o elemento inicial de um array de caracteres. A _precisão_ especifica o número máximo de bytes a serem escritos. Se a _precisão_ não for especificada, escreve cada byte até e não incluindo o primeiro terminador nulo. Se o especificador **l** for usado, o argumento deve ser um ponteiro para o elemento inicial de um array de wchar_t, que é convertido para um array de char como se por uma chamada a [wcrtomb](<#/doc/string/multibyte/wcrtomb>) com estado de conversão inicializado com zero. | N/A | N/A | char* | wchar_t* | N/A | N/A | N/A | N/A | N/A
`d`
`i` |

    Converte um **inteiro com sinal** para representação decimal _[-]dddd_.
A _precisão_ especifica o número mínimo de dígitos a aparecer. A precisão padrão é 1.
Se tanto o valor convertido quanto a precisão forem ​0​, a conversão resulta em nenhum caractere. | signed char | short | int | long | long long | [intmax_t](<#/doc/types/integer>) | signed [size_t](<#/doc/types/size_t>) | [ptrdiff_t](<#/doc/types/ptrdiff_t>) | N/A
`o` |

    Converte um **inteiro sem sinal** para representação octal _oooo_.
A _precisão_ especifica o número mínimo de dígitos a aparecer. A precisão padrão é 1. Se tanto o valor convertido quanto a precisão forem ​0​, a conversão resulta em nenhum caractere. Na _implementação alternativa_, a precisão é aumentada se necessário, para escrever um zero à esquerda. Nesse caso, se tanto o valor convertido quanto a precisão forem ​0​, um único ​0​ é escrito. | unsigned char | unsigned short | unsigned int | unsigned long | unsigned long long | [uintmax_t](<#/doc/types/integer>) | [size_t](<#/doc/types/size_t>) | unsigned version of [ptrdiff_t](<#/doc/types/ptrdiff_t>) | N/A
`x`
`X` |

    Converte um **inteiro sem sinal** para representação hexadecimal _hhhh_.
Para a conversão `x`, as letras `abcdef` são usadas.
Para a conversão `X`, as letras `ABCDEF` são usadas.
A _precisão_ especifica o número mínimo de dígitos a aparecer. A precisão padrão é 1. Se tanto o valor convertido quanto a precisão forem ​0​, a conversão resulta em nenhum caractere. Na _implementação alternativa_, `0x` ou `0X` é prefixado aos resultados se o valor convertido for diferente de zero. | N/A
`u` |

    Converte um **inteiro sem sinal** para representação decimal _dddd_.
A _precisão_ especifica o número mínimo de dígitos a aparecer. A precisão padrão é 1. Se tanto o valor convertido quanto a precisão forem ​0​, a conversão resulta em nenhum caractere. | N/A
`f`
`F` |

    Converte um **número de ponto flutuante** para a notação decimal no estilo _[-]ddd.ddd_.
A _precisão_ especifica o número exato de dígitos a aparecer após o caractere de ponto decimal. A precisão padrão é 6. Na _implementação alternativa_, o caractere de ponto decimal é escrito mesmo que nenhum dígito o siga. Para o estilo de conversão de infinito e não-número, veja as notas. | N/A | N/A | double | double(C99) | N/A | N/A | N/A | N/A | long double
`e`
`E` |

    Converte um **número de ponto flutuante** para a notação de expoente decimal.
Para o estilo de conversão `e`, _[-]d.ddd_ ﻿`e` _±dd_ é usado.
Para o estilo de conversão `E`, _[-]d.ddd_ ﻿`E` _±dd_ é usado.
O expoente contém pelo menos dois dígitos; mais dígitos são usados apenas se necessário. Se o valor for ​0​, o expoente também é ​0​. A _precisão_ especifica o número exato de dígitos a aparecer após o caractere de ponto decimal. A precisão padrão é 6. Na _implementação alternativa_, o caractere de ponto decimal é escrito mesmo que nenhum dígito o siga. Para o estilo de conversão de infinito e não-número, veja as notas. | N/A | N/A | N/A | N/A | N/A | N/A
`a`
`A` (C99) |

    Converte um **número de ponto flutuante** para a notação de expoente hexadecimal.
Para o estilo de conversão `a`, _[-]_ ﻿`0x` _h.hhh_ ﻿`p` _±d_ é usado.
Para o estilo de conversão `A`, _[-]_ ﻿`0X` _h.hhh_ ﻿`P` _±d_ é usado.
O primeiro dígito hexadecimal não é `0` se o argumento for um valor de ponto flutuante normalizado. Se o valor for ​0​, o expoente também é ​0​. A _precisão_ especifica o número exato de dígitos a aparecer após o caractere de ponto hexadecimal. A precisão padrão é suficiente para a representação exata do valor. Na _implementação alternativa_, o caractere de ponto decimal é escrito mesmo que nenhum dígito o siga. Para o estilo de conversão de infinito e não-número, veja as notas. | N/A | N/A | N/A | N/A | N/A | N/A
`g`
`G` |

    Converte um **número de ponto flutuante** para notação decimal ou de expoente decimal dependendo do valor e da _precisão_.
Para o estilo de conversão `g`, será realizada uma conversão com estilo `e` ou `f`.
Para o estilo de conversão `G`, será realizada uma conversão com estilo `E` ou `F`.
Seja `P` igual à precisão se não for zero, 6 se a precisão não for especificada, ou 1 se a precisão for ​0​. Então, se uma conversão com estilo `E` tivesse um expoente de `X`:
* se _P > X ≥ −4_, a conversão é com estilo `f` ou `F` e precisão _P − 1 − X_.
* caso contrário, a conversão é com estilo `e` ou `E` e precisão _P − 1_.
A menos que uma _representação alternativa_ seja solicitada, os zeros finais são removidos, e o caractere de ponto decimal também é removido se nenhuma parte fracionária for deixada. Para o estilo de conversão de infinito e não-número, veja as notas. | N/A | N/A | N/A | N/A | N/A | N/A
`n` |

    Retorna o **número de caracteres escritos** até agora por esta chamada à função.
O resultado é _escrito_ no valor apontado pelo argumento. A especificação não pode conter nenhuma _flag_, _largura de campo_ ou _precisão_. | signed char* | short* | int* | long* | long long* | [intmax_t](<#/doc/types/integer>)* | signed [size_t](<#/doc/types/size_t>)* | [ptrdiff_t](<#/doc/types/ptrdiff_t>)* | N/A
`p` | Escreve uma sequência de caracteres definida pela implementação que define um **ponteiro**. | N/A | N/A | void* | N/A | N/A | N/A | N/A | N/A | N/A

As funções de conversão de ponto flutuante convertem infinito para `inf` ou `infinity`. Qual delas é usada é definida pela implementação.

Não-é-um-número é convertido para `nan` ou `nan(_sequência_de_caracteres_)`. Qual delas é usada é definida pela implementação.

As conversões `F`, `E`, `G`, `A` produzem `INF`, `INFINITY`, `NAN` em vez disso.

O especificador de conversão usado para imprimir char, unsigned char, signed char, short e unsigned short espera tipos promovidos das [promoções de argumento padrão](<#/doc/language/conversion>), mas antes de imprimir seu valor será convertido para char, unsigned char, signed char, short e unsigned short. É seguro passar valores desses tipos devido à promoção que ocorre quando uma função variádica é chamada.

As especificações de conversão corretas para os tipos de caracteres de largura fixa ([int8_t](<#/doc/types/integer>), etc) são definidas no cabeçalho [`<inttypes.h>`](<#/doc/types/integer>) (embora [PRIdMAX](<#/doc/types/integer>), [PRIuMAX](<#/doc/types/integer>), etc sejam sinônimos de `%jd`, `%ju`, etc).

O especificador de conversão `%n` que escreve na memória é um alvo comum de exploits de segurança onde as strings de formato dependem da entrada do usuário e não é suportado pela família de funções `printf_s` com verificação de limites.

Existe um [ponto de sequência](<#/doc/language/eval_order>) após a ação de cada especificador de conversão; isso permite armazenar múltiplos resultados de `%n` na mesma variável ou, como um caso extremo, imprimir uma string modificada por um `%n` anterior dentro da mesma chamada.

Se uma especificação de conversão for inválida, o comportamento é indefinido.

### Valor de retorno

1,2) número de caracteres transmitidos para o fluxo de saída ou valor negativo se ocorreu um erro de saída ou um erro de codificação (para especificadores de conversão de string e caractere).

3) número de caracteres escritos no buffer (não contando o caractere nulo de terminação), ou um valor negativo se ocorreu um erro de codificação (para especificadores de conversão de string e caractere).

4) número de caracteres (não incluindo o caractere nulo de terminação) que teriam sido escritos no buffer se bufsz fosse ignorado, ou um valor negativo se ocorreu um erro de codificação (para especificadores de conversão de string e caractere).

5,6) número de caracteres transmitidos para o fluxo de saída ou valor negativo se ocorreu um erro de saída, um erro de violação de restrições em tempo de execução ou um erro de codificação.

7) número de caracteres escritos no buffer, não contando o caractere nulo (que é sempre escrito desde que buffer não seja um ponteiro nulo e bufsz não seja zero e não seja maior que RSIZE_MAX), ou zero em violações de restrição em tempo de execução, e valor negativo em erros de codificação.

8) número de caracteres não incluindo o caractere nulo de terminação (que é sempre escrito desde que buffer não seja um ponteiro nulo e bufsz não seja zero e não seja maior que RSIZE_MAX), que teriam sido escritos no buffer se bufsz fosse ignorado, ou um valor negativo se ocorreu uma violação de restrições em tempo de execução ou um erro de codificação.

### Notas

O padrão C e [POSIX](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/fprintf.html>) especificam que o comportamento de `sprintf` e suas variantes é indefinido quando um argumento se sobrepõe ao buffer de destino. Exemplo:
```c
    sprintf(dst, "%s and %s", dst, t); // <- quebrado: comportamento indefinido
```

[POSIX especifica](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/fprintf.html>) que [errno](<#/doc/error/errno>) é definido em caso de erro. Ele também especifica especificações de conversão adicionais, mais notavelmente o suporte para reordenação de argumentos (n$ imediatamente após % indica o `n`-ésimo argumento).

Chamar `snprintf` com bufsz zero e ponteiro nulo para buffer é útil para determinar o tamanho de buffer necessário para conter a saída:
```c
    const char fmt[] = "sqrt(2) = %f";
    int sz = snprintf(NULL, 0, fmt, sqrt(2));
    char buf[sz + 1]; // nota +1 para o byte nulo de terminação
    snprintf(buf, sizeof buf, fmt, sqrt(2));
```

`snprintf_s`, assim como `snprintf`, mas ao contrário de `sprintf_s`, truncará a saída para caber em bufsz - 1.

### Exemplo

Execute este código
```c
    #include <inttypes.h>
    #include <stdint.h>
    #include <stdio.h>
    
    int main(void)
    {
        const char* s = "Hello";
        printf("Strings:\n"); // same as puts("Strings");
        printf(" padding:\n");
        printf("\t[%10s]\n", s);
        printf("\t[%-10s]\n", s);
        printf("\t[%*s]\n", 10, s);
        printf(" truncating:\n");
        printf("\t%.4s\n", s);
        printf("\t%.*s\n", 3, s);
    
        printf("Characters:\t%c %%\n", 'A');
    
        printf("Integers:\n");
        printf("\tDecimal:\t%i %d %.6i %i %.0i %+i %i\n",
                             1, 2,   3, 0,   0,  4,-4);
        printf("\tHexadecimal:\t%x %x %X %#x\n", 5, 10, 10, 6);
        printf("\tOctal:\t\t%o %#o %#o\n", 10, 10, 4);
    
        printf("Floating-point:\n");
        printf("\tRounding:\t%f %.0f %.32f\n", 1.5, 1.5, 1.3);
        printf("\tPadding:\t%05.2f %.2f %5.2f\n", 1.5, 1.5, 1.5);
        printf("\tScientific:\t%E %e\n", 1.5, 1.5);
        printf("\tHexadecimal:\t%a %A\n", 1.5, 1.5);
        printf("\tSpecial values:\t0/0=%g 1/0=%g\n", 0.0 / 0.0, 1.0 / 0.0);
    
        printf("Fixed-width types:\n");
        printf("\tLargest 32-bit value is %" PRIu32 " or %#"PRIx32 "\n",
                                         UINT32_MAX,     UINT32_MAX );
    }
```

Saída possível:
```
    Strings:
     padding:
            [     Hello]
            [Hello     ]
            [     Hello]
     truncating:
            Hell
            Hel
    Characters:     A %
    Integers:
            Decimal:        1 2 000003 0  +4 -4
            Hexadecimal:    5 a A 0x6
            Octal:          12 012 04
    Floating-point:
            Rounding:       1.500000 2 1.30000000000000004440892098500626
            Padding:        01.50 1.50  1.50
            Scientific:     1.500000E+00 1.500000e+00
            Hexadecimal:    0x1.8p+0 0X1.8P+0
            Special values: 0/0=-nan 1/0=inf
    Fixed-width types:
            Largest 32-bit value is 4294967295 or 0xffffffff
```

### Referências

* C23 standard (ISO/IEC 9899:2024):

* 7.21.6.1 The fprintf function (p: A definir)

* 7.21.6.3 The printf function (p: A definir)

* 7.21.6.5 The snprintf function (p: A definir)

* 7.21.6.6 The sprintf function (p: A definir)

* K.3.5.3.1 The fprintf_s function (p: A definir)

* K.3.5.3.3 The printf_s function (p: A definir)

* K.3.5.3.5 The snprintf_s function (p: A definir)

* K.3.5.3.6 The sprintf_s function (p: A definir)
* C17 standard (ISO/IEC 9899:2018):

* 7.21.6.1 The fprintf function (p: 225-230)

* 7.21.6.3 The printf function (p: 236)

* 7.21.6.5 The snprintf function (p: 237)

* 7.21.6.6 The sprintf function (p: 237)

* K.3.5.3.1 The fprintf_s function (p: 430)

* K.3.5.3.3 The printf_s function (p: 432)

* K.3.5.3.5 The snprintf_s function (p: 432-433)

* K.3.5.3.6 The sprintf_s function (p: 433)
* C11 standard (ISO/IEC 9899:2011):

* 7.21.6.1 The fprintf function (p: 309-316)

* 7.21.6.3 The printf function (p: 324)

* 7.21.6.5 The snprintf function (p: 325)

* 7.21.6.6 The sprintf function (p: 325-326)

* K.3.5.3.1 The fprintf_s function (p: 591)

* K.3.5.3.3 The printf_s function (p: 593-594)

* K.3.5.3.5 The snprintf_s function (p: 594-595)

* K.3.5.3.6 The sprintf_s function (p: 595-596)
* C99 standard (ISO/IEC 9899:1999):

* 7.19.6.1 The fprintf function (p: 274-282)

* 7.19.6.3 The printf function (p: 290)

* 7.19.6.5 The snprintf function (p: 290-291)

* 7.19.6.6 The sprintf function (p: 291)
* C89/C90 standard (ISO/IEC 9899:1990):

* 4.9.6.1 The fprintf function

* 4.9.6.3 The printf function

* 4.9.6.5 The sprintf function

### Veja também

[ wprintffwprintfswprintfwprintf_sfwprintf_sswprintf_ssnwprintf_s](<#/doc/io/fwprintf>)(C95)(C95)(C95)(C11)(C11)(C11)(C11) | imprime saída formatada de caracteres largos para [stdout](<#/doc/io/std_streams>), um fluxo de arquivo ou um buffer
(função)
[ vprintfvfprintfvsprintfvsnprintfvprintf_svfprintf_svsprintf_svsnprintf_s](<#/doc/io/vfprintf>)(C99)(C11)(C11)(C11)(C11) | imprime saída formatada para [stdout](<#/doc/io/std_streams>), um fluxo de arquivo ou um buffer
usando lista de argumentos variáveis
(função)
[ fputs](<#/doc/io/fputs>) | escreve uma string de caracteres em um fluxo de arquivo
(função)
[ scanffscanfsscanfscanf_sfscanf_ssscanf_s](<#/doc/io/fscanf>)(C11)(C11)(C11) | lê entrada formatada de [stdin](<#/doc/io/std_streams>), um fluxo de arquivo ou um buffer
(função)
[documentação C++](<#/>) para printf, fprintf, sprintf, snprintf