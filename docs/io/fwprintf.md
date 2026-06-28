# wprintf, fwprintf, swprintf, wprintf_s, fwprintf_s, swprintf_s, snwprintf_s

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
int wprintf( const wchar_t* format, ... );  // desde C95
(até C99)  // até C99
int wprintf( const wchar_t* restrict format, ... );  // desde C99
int fwprintf( FILE* stream, const wchar_t* format, ... );  // desde C95
(até C99)  // até C99
int fwprintf( FILE* restrict stream,
const wchar_t* restrict format, ... );  // desde C99
int swprintf( wchar_t* buffer, size_t bufsz,
const wchar_t* format, ... );  // desde C95
(até C99)  // até C99
int swprintf( wchar_t* restrict buffer, size_t bufsz,
const wchar_t* restrict format, ... );  // desde C99
int wprintf_s( const wchar_t* restrict format, ... );  // desde C11
int fwprintf_s( FILE* restrict stream,
const wchar_t* restrict format, ... );  // desde C11
int swprintf_s( wchar_t* restrict buffer, rsize_t bufsz,
const wchar_t* restrict format, ... );  // desde C11
int snwprintf_s( wchar_t* restrict s, rsize_t n,
const wchar_t* restrict format, ... );  // desde C11
```

Carrega os dados dos locais fornecidos, converte-os para equivalentes de string de caracteres largos e escreve os resultados em uma variedade de destinos.

1) Escreve os resultados para [stdout](<#/doc/io/std_streams>).

2) Escreve os resultados para um fluxo de arquivo `stream`.

3) Se `bufsz` for maior que zero, escreve os resultados para um buffer de string de caracteres largos. No máximo `bufsz - 1` caracteres largos são escritos, seguidos por um caractere largo nulo. Se `bufsz` for zero, nada é escrito (e `buffer` pode ser um ponteiro nulo).

4-6) O mesmo que (1-3), exceto que os seguintes erros são detectados em tempo de execução e chamam a função [manipulador de restrição](<#/doc/error/set_constraint_handler_s>) atualmente instalada:

  * o especificador de conversão `%n` está presente em `format`
  * qualquer um dos argumentos correspondentes a `%s` é um ponteiro nulo
  * `format` ou `buffer` é um ponteiro nulo
  * `bufsz` é zero ou maior que RSIZE_MAX / sizeof(wchar_t)
  * ocorrem erros de codificação em qualquer um dos especificadores de conversão de string e caractere
  * (apenas para `swprintf_s`) o número de caracteres largos a serem escritos, incluindo o nulo, excederia `bufsz`.

7) O mesmo que (6), exceto que truncará o resultado para caber dentro do array apontado por `s`.

Assim como todas as funções com verificação de limites, `wprintf_s`, `fwprintf_s`, `swprintf_s` e `snwprintf_s` são garantidas de estarem disponíveis apenas se `__STDC_LIB_EXT1__` for definido pela implementação e se o usuário definir `__STDC_WANT_LIB_EXT1__` para a constante inteira 1 antes de incluir [`<stdio.h>`](<#/doc/io>).

### Parâmetros

- **stream** — fluxo de arquivo de saída para escrever
- **buffer** — ponteiro para uma string de caracteres largos para escrever
- **bufsz** — até `bufsz - 1` caracteres largos podem ser escritos, mais o terminador nulo
- **format** — ponteiro para uma string de caracteres largos terminada em nulo especificando como interpretar os dados
- **...** — argumentos especificando os dados a serem impressos. Se qualquer argumento após as [promoções de argumento padrão](<#/doc/language/conversion>) não for do tipo esperado pelo especificador de conversão correspondente, ou se houver menos argumentos do que o exigido por `format`, o comportamento é indefinido. Se houver mais argumentos do que o exigido por `format`, os argumentos extras são avaliados e ignorados.

A string de **formato** consiste em caracteres largos comuns (exceto `%`), que são copiados inalterados para o fluxo de saída, e especificações de conversão. Cada especificação de conversão tem o seguinte formato:

  * caractere `%` introdutório.

  * (opcional) uma ou mais flags que modificam o comportamento da conversão:

  * `-`: o resultado da conversão é justificado à esquerda dentro do campo (por padrão, é justificado à direita).
  * `+`: o sinal de conversões com sinal é sempre prefixado ao resultado da conversão (por padrão, o resultado é precedido por um sinal de menos apenas quando é negativo).
  * _espaço_ : se o resultado de uma conversão com sinal não começar com um caractere de sinal, ou for vazio, um espaço é prefixado ao resultado. É ignorado se a flag `+` estiver presente.
  * `#`: _forma alternativa_ da conversão é realizada. Veja a tabela abaixo para os efeitos exatos, caso contrário o comportamento é indefinido.
  * `0`: para conversões de números inteiros e de ponto flutuante, zeros à esquerda são usados para preencher o campo em vez de caracteres de _espaço_. Para números inteiros, é ignorado se a precisão for explicitamente especificada. Para outras conversões, o uso desta flag resulta em comportamento indefinido. É ignorado se a flag `-` estiver presente.

  * (opcional) valor inteiro ou `*` que especifica a largura mínima do campo. O resultado é preenchido com caracteres de _espaço_ (por padrão), se necessário, à esquerda quando justificado à direita, ou à direita se justificado à esquerda. No caso em que `*` é usado, a largura é especificada por um argumento adicional do tipo `int`, que aparece antes do argumento a ser convertido e do argumento que fornece a precisão, se um for fornecido. Se o valor do argumento for negativo, ele resulta na flag `-` especificada e largura de campo positiva (Nota: Esta é a largura mínima: O valor nunca é truncado).

  * (opcional) `.` seguido por um número inteiro ou `*`, ou nenhum, que especifica a _precisão_ da conversão. No caso em que `*` é usado, a _precisão_ é especificada por um argumento adicional do tipo `int`, que aparece antes do argumento a ser convertido, mas depois do argumento que fornece a largura mínima do campo, se um for fornecido. Se o valor deste argumento for negativo, ele é ignorado. Se nem um número nem `*` for usado, a precisão é considerada zero. Veja a tabela abaixo para os efeitos exatos da _precisão_.

  * (opcional) _modificador de comprimento_ que especifica o tamanho do argumento (em combinação com o especificador de formato de conversão, ele especifica o tipo do argumento correspondente).

  * especificador de formato de conversão.

Os seguintes especificadores de formato estão disponíveis:

Conversão
Especificador | Explicação | Tipo de Argumento
Esperado
**Modificador de Comprimento****→** | `hh` (C99) | `h` | (nenhum) | `l` | `ll` (C99) | `j` (C99) | `z` (C99) | `t` (C99) | `L`
`%` | Escreve o literal `%`. A especificação de conversão completa deve ser `%%`. | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A
`c` |

    Escreve um **único caractere**.
O argumento é primeiro convertido para `wchar_t` como se por uma chamada a [btowc](<#/doc/string/multibyte/btowc>). Se o modificador `l` for usado, o argumento `wint_t` é primeiro convertido para `wchar_t`. | N/A | N/A | int | wint_t | N/A | N/A | N/A | N/A | N/A
`s` |

    Escreve uma **string de caracteres**
O argumento deve ser um ponteiro para o elemento inicial de um array de caracteres contendo uma sequência de caracteres multibyte começando no estado de shift inicial, que é convertida para um array de caracteres largos como se por uma chamada a [mbrtowc](<#/doc/string/multibyte/mbrtowc>) com estado de conversão inicializado com zero. A _precisão_ especifica o número máximo de caracteres largos a serem escritos. Se a _precisão_ não for especificada, escreve todos os caracteres largos até, mas não incluindo, o primeiro terminador nulo. Se o especificador `l` for usado, o argumento deve ser um ponteiro para o elemento inicial de um array de `wchar_t`. | N/A | N/A | char* | wchar_t* | N/A | N/A | N/A | N/A | N/A
`d`
`i` |

    Converte um **inteiro com sinal** para representação decimal _[-]dddd_.
A _precisão_ especifica o número mínimo de dígitos a aparecer. A precisão padrão é 1.
Se tanto o valor convertido quanto a precisão forem ​0​, a conversão resulta em nenhum caractere. | signed char | short | int | long | long long | [intmax_t](<#/doc/types/integer>) | signed [size_t](<#/doc/types/size_t>) | [ptrdiff_t](<#/doc/types/ptrdiff_t>) | N/A
`o` |

    Converte um **inteiro sem sinal** para representação octal _oooo_.
A _precisão_ especifica o número mínimo de dígitos a aparecer. A precisão padrão é 1. Se tanto o valor convertido quanto a precisão forem ​0​, a conversão resulta em nenhum caractere. Na _implementação alternativa_, a precisão é aumentada se necessário, para escrever um zero à esquerda. Nesse caso, se tanto o valor convertido quanto a precisão forem ​0​, um único ​0​ é escrito. | unsigned char | unsigned short | unsigned int | unsigned long | unsigned long long | [uintmax_t](<#/doc/types/integer>) | [size_t](<#/doc/types/size_t>) | versão unsigned de [ptrdiff_t](<#/doc/types/ptrdiff_t>) | N/A
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
Seja `P` igual à precisão se não for zero, 6 se a precisão não for especificada, ou 1 se a precisão for ​0​. Então, se uma conversão com estilo `E` teria um expoente de `X`:

  * se _P > X ≥ −4_, a conversão é com estilo `f` ou `F` e precisão _P − 1 − X_.
  * caso contrário, a conversão é com estilo `e` ou `E` e precisão _P − 1_.

A menos que a _representação alternativa_ seja solicitada, os zeros à direita são removidos, e o caractere de ponto decimal também é removido se nenhuma parte fracionária for deixada. Para o estilo de conversão de infinito e não-número, veja as notas. | N/A | N/A | N/A | N/A | N/A | N/A
`n` |

    Retorna o **número de caracteres escritos** até agora por esta chamada à função.
O resultado é _escrito_ para o valor apontado pelo argumento. A especificação não pode conter nenhuma _flag_, _largura de campo_ ou _precisão_. | signed char* | short* | int* | long* | long long* | [intmax_t](<#/doc/types/integer>)* | signed [size_t](<#/doc/types/size_t>)* | [ptrdiff_t](<#/doc/types/ptrdiff_t>)* | N/A
`p` | Escreve uma sequência de caracteres definida pela implementação que define um **ponteiro**. | N/A | N/A | void* | N/A | N/A | N/A | N/A | N/A

As funções de conversão de ponto flutuante convertem infinito para `inf` ou `infinity`. Qual delas é usada é definida pela implementação.

Não-é-um-número é convertido para `nan` ou `nan(_sequência_de_caracteres_)`. Qual delas é usada é definida pela implementação.

As conversões `F`, `E`, `G`, `A` produzem `INF`, `INFINITY`, `NAN` em vez disso.

O especificador de conversão usado para imprimir `char`, `unsigned char`, `signed char`, `short` e `unsigned short` espera tipos promovidos das [promoções de argumento padrão](<#/doc/language/conversion>), mas antes de imprimir seu valor será convertido para `char`, `unsigned char`, `signed char`, `short` e `unsigned short`. É seguro passar valores desses tipos devido à promoção que ocorre quando uma função variádica é chamada.

As especificações de conversão corretas para os tipos de caracteres de largura fixa ([int8_t](<#/doc/types/integer>), etc) são definidas no cabeçalho [`<inttypes.h>`](<#/doc/types/integer>) (embora [PRIdMAX](<#/doc/types/integer>), [PRIuMAX](<#/doc/types/integer>), etc sejam sinônimos de `%jd`, `%ju`, etc).

O especificador de conversão `%n` que escreve na memória é um alvo comum de explorações de segurança onde strings de formato dependem da entrada do usuário e não é suportado pela família de funções `printf_s` com verificação de limites.

Existe um [ponto de sequência](<#/doc/language/eval_order>) após a ação de cada especificador de conversão; isso permite armazenar múltiplos resultados de `%n` na mesma variável ou, como um caso limite, imprimir uma string modificada por um `%n` anterior dentro da mesma chamada.

Se uma especificação de conversão for inválida, o comportamento é indefinido.

### Valor de retorno

1,2) Número de caracteres largos escritos se bem-sucedido ou valor negativo se ocorreu um erro.

3) Número de caracteres largos escritos (sem contar o caractere largo nulo terminador) se bem-sucedido ou valor negativo se ocorreu um erro de codificação ou se o número de caracteres a serem gerados foi igual ou maior que `bufsz` (incluindo quando `bufsz` é zero).

4,5) Número de caracteres largos escritos se bem-sucedido ou valor negativo se ocorreu um erro.

6) Número de caracteres largos (sem contar o nulo terminador) que foram escritos no `buffer`. Retorna um valor negativo em erros de codificação e em estouro. Retorna zero em todos os outros erros.

7) Número de caracteres largos (sem contar o nulo terminador) que teriam sido escritos no `buffer` se `bufsz` tivesse sido suficientemente grande, ou um valor negativo se ocorrer um erro. (significando que a escrita foi bem-sucedida e completa apenas se o retorno for não negativo e menor que `bufsz`)

### Notas

Enquanto strings estreitas fornecem [snprintf](<#/doc/io/fprintf>), que torna possível determinar o tamanho do buffer de saída necessário, não há equivalente para strings de caracteres largos (até `snwprintf_s`)(desde C11), e para determinar o tamanho do buffer, o programa pode precisar chamar `swprintf`, verificar o valor do resultado e realocar um buffer maior, tentando novamente até ter sucesso.

`snwprintf_s`, ao contrário de `swprintf_s`, truncará o resultado para caber dentro do array apontado por `buffer`, embora o truncamento seja tratado como um erro pela maioria das funções com verificação de limites.

### Exemplo

Execute este código
```c
    #include <locale.h>
    #include <wchar.h>
     
    int main(void)
    {
        char narrow_str[] = "z\u00df\u6c34\U0001f34c";
                      // or "zß水🍌"
                      // or "\x7a\xc3\x9f\xe6\xb0\xb4\xf0\x9f\x8d\x8c";
        wchar_t warr[29]; // the expected string is 28 characters plus 1 null terminator
        setlocale(LC_ALL, "en_US.utf8");
        swprintf(warr, sizeof warr / sizeof* warr,
                 L"Converted from UTF-8: '%s'", narrow_str);
        wprintf(L"%ls\n", warr);
    }
```

Saída:
```
    Converted from UTF-8: 'zß水🍌'
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.29.2.1 A função fwprintf (p: TBD)

    

  * 7.29.2.3 A função swprintf (p: TBD)

    

  * 7.29.2.11 A função wprintf (p: TBD)

    

  * K.3.9.1.1 A função fwprintf_s (p: TBD)

    

  * K.3.9.1.4 A função swprintf_s (p: TBD)

    

  * K.3.9.1.13 A função wprintf_s (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.29.2.1 A função fwprintf (p: TBD)

    

  * 7.29.2.3 A função swprintf (p: TBD)

    

  * 7.29.2.11 A função wprintf (p: TBD)

    

  * K.3.9.1.1 A função fwprintf_s (p: TBD)

    

  * K.3.9.1.4 A função swprintf_s (p: TBD)

    

  * K.3.9.1.13 A função wprintf_s (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.29.2.1 A função fwprintf (p: 403-410)

    

  * 7.29.2.3 A função swprintf (p: 416)

    

  * 7.29.2.11 A função wprintf (p: 421)

    

  * K.3.9.1.1 A função fwprintf_s (p: 628)

    

  * K.3.9.1.4 A função swprintf_s (p: 630-631)

    

  * K.3.9.1.13 A função wprintf_s (p: 637-638)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.24.2.1 A função fwprintf (p: 349-356)

    

  * 7.24.2.3 A função swprintf (p: 362)

    

  * 7.24.2.11 A função wprintf (p: 366)

### Veja também

[ printffprintfsprintfsnprintfprintf_sfprintf_ssprintf_ssnprintf_s](<#/doc/io/fprintf>)(C99)(C11)(C11)(C11)(C11) | imprime saída formatada para [stdout](<#/doc/io/std_streams>), um fluxo de arquivo ou um buffer (função)
[ vwprintfvfwprintfvswprintfvwprintf_svfwprintf_svswprintf_svsnwprintf_s](<#/doc/io/vfwprintf>)(C95)(C95)(C95)(C11)(C11)(C11)(C11) | imprime saída formatada de caracteres largos para [stdout](<#/doc/io/std_streams>), um fluxo de arquivo
ou um buffer usando lista de argumentos variáveis (função)
[ fputws](<#/doc/io/fputws>)(C95) | escreve uma string de caracteres largos para um fluxo de arquivo (função)
[Documentação C++](<#/>) para wprintf, fwprintf, swprintf