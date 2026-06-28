# vprintf, vfprintf, vsprintf, vsnprintf, vprintf_s, vfprintf_s, vsprintf_s, vsnprintf_s

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
int vprintf( const char* format, va_list vlist );  // até C99
int vprintf( const char* restrict format, va_list vlist );  // desde C99
int vfprintf( FILE* stream, const char* format, va_list vlist );  // até C99
int vfprintf( FILE* restrict stream, const char* restrict format,
va_list vlist );  // desde C99
int vsprintf( char* buffer, const char* format, va_list vlist );  // até C99
int vsprintf( char* restrict buffer, const char* restrict format,
va_list vlist );  // desde C99
int vsnprintf( char* restrict buffer, size_t bufsz,
const char* restrict format, va_list vlist );  // desde C99
int vprintf_s( const char* restrict format, va_list vlist );  // desde C11
int vfprintf_s( FILE* restrict stream, const char* restrict format,
va_list vlist );  // desde C11
int vsprintf_s( char* restrict buffer, rsize_t bufsz,
const char* restrict format, va_list vlist );  // desde C11
int vsnprintf_s( char* restrict buffer, rsize_t bufsz,
const char* restrict format, va_list vlist );  // desde C11
```

  
Carrega os dados dos locais, definidos por vlist, converte-os para equivalentes de string de caracteres e escreve os resultados para uma variedade de destinos.

1) Escreve os resultados para [stdout](<#/doc/io/std_streams>).

2) Escreve os resultados para um fluxo de arquivo stream.

3) Escreve os resultados para um buffer de string de caracteres.

4) Escreve os resultados para um buffer de string de caracteres. No máximo bufsz - 1 caracteres são escritos. A string de caracteres resultante será terminada com um caractere nulo, a menos que bufsz seja zero. Se bufsz for zero, nada é escrito e buffer pode ser um ponteiro nulo, no entanto, o valor de retorno (número de bytes que seriam escritos sem incluir o terminador nulo) ainda é calculado e retornado.

5-8) O mesmo que (1-4), exceto que os seguintes erros são detectados em tempo de execução e chamam a função [constraint handler](<#/doc/error/set_constraint_handler_s>) atualmente instalada: 

    

  * o especificador de conversão `%n` está presente em format
  * qualquer um dos argumentos correspondentes a `%s` é um ponteiro nulo 
  * format ou buffer é um ponteiro nulo 
  * bufsz é zero ou maior que RSIZE_MAX
  * erros de codificação ocorrem em qualquer um dos especificadores de conversão de string e caractere 
  * (apenas para `vsprintf_s`), a string a ser armazenada em buffer (incluindo o nulo final) excederia bufsz

Assim como todas as funções com verificação de limites, `vprintf_s`, `vfprintf_s`, `vsprintf_s` e `vsnprintf_s` são garantidas de estarem disponíveis apenas se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir [`<stdio.h>`](<#/doc/io>).

### Parâmetros

stream  |  \-  |  fluxo de arquivo de saída para escrever   
buffer  |  \-  |  ponteiro para uma string de caracteres para escrever   
bufsz  |  \-  |  até bufsz - 1 caracteres podem ser escritos, mais o terminador nulo   
format  |  \-  |  ponteiro para uma string de caracteres terminada em nulo especificando como interpretar os dados   
vlist  |  \-  |  lista de argumentos variáveis contendo os dados a serem impressos.   
  
A string **format** consiste em caracteres de byte comuns (exceto `%`), que são copiados inalterados para o fluxo de saída, e especificações de conversão. Cada especificação de conversão tem o seguinte formato: 

    

  * caractere `%` introdutório. 

    

  * (opcional) uma ou mais flags que modificam o comportamento da conversão: 

    

  * `-`: o resultado da conversão é justificado à esquerda dentro do campo (por padrão é justificado à direita). 
  * `+`: o sinal de conversões com sinal é sempre prefixado ao resultado da conversão (por padrão, o resultado é precedido por menos apenas quando é negativo). 
  * _espaço_ : se o resultado de uma conversão com sinal não começar com um caractere de sinal, ou for vazio, um espaço é prefixado ao resultado. É ignorado se a flag `+` estiver presente. 
  * `#`: _forma alternativa_ da conversão é realizada. Veja a tabela abaixo para os efeitos exatos, caso contrário o comportamento é indefinido. 
  * `0`: para conversões de números inteiros e de ponto flutuante, zeros à esquerda são usados para preencher o campo em vez de caracteres de _espaço_. Para números inteiros, é ignorado se a precisão for explicitamente especificada. Para outras conversões, o uso desta flag resulta em comportamento indefinido. É ignorado se a flag `-` estiver presente. 

    

  * (opcional) valor inteiro ou `*` que especifica a largura mínima do campo. O resultado é preenchido com caracteres de _espaço_ (por padrão), se necessário, à esquerda quando justificado à direita, ou à direita se justificado à esquerda. No caso em que `*` é usado, a largura é especificada por um argumento adicional do tipo int, que aparece antes do argumento a ser convertido e do argumento que fornece a precisão, se um for fornecido. Se o valor do argumento for negativo, resulta na flag `-` especificada e largura de campo positiva (Nota: Esta é a largura mínima: O valor nunca é truncado.). 

    

  * (opcional) `.` seguido por um número inteiro ou `*`, ou nenhum que especifica a _precisão_ da conversão. No caso em que `*` é usado, a _precisão_ é especificada por um argumento adicional do tipo int, que aparece antes do argumento a ser convertido, mas depois do argumento que fornece a largura mínima do campo, se um for fornecido. Se o valor deste argumento for negativo, ele é ignorado. Se nem um número nem `*` for usado, a precisão é considerada zero. Veja a tabela abaixo para os efeitos exatos da _precisão_. 

    

  * (opcional) _modificador de comprimento_ que especifica o tamanho do argumento (em combinação com o especificador de formato de conversão, ele especifica o tipo do argumento correspondente). 

    

  * especificador de formato de conversão. 

Os seguintes especificadores de formato estão disponíveis: 

Especificador  
de Conversão  | Explicação  | Tipo de  
Argumento Esperado   
**Modificador  
de Comprimento****→** | `hh` (C99) | `h` | (nenhum)  | `l` | `ll` (C99) | `j` (C99) | `z` (C99) | `t` (C99) | `L`  
`%` | Escreve o literal `%`. A especificação de conversão completa deve ser `%%`.  |  N/A |  N/A |  N/A |  N/A |  N/A |  N/A |  N/A |  N/A |  N/A  
`c` | 

    Escreve um **único caractere**. 
O argumento é primeiro convertido para unsigned char. Se o modificador **l** for usado, o argumento é primeiro convertido para uma string de caracteres como se por **%ls** com um argumento wchar_t[2].  |  N/A |  N/A | int | wint_t |  N/A |  N/A |  N/A |  N/A |  N/A  
`s` | 

    Escreve uma **string de caracteres**
O argumento deve ser um ponteiro para o elemento inicial de um array de caracteres. A _precisão_ especifica o número máximo de bytes a serem escritos. Se a _precisão_ não for especificada, escreve cada byte até e não incluindo o primeiro terminador nulo. Se o especificador **l** for usado, o argumento deve ser um ponteiro para o elemento inicial de um array de wchar_t, que é convertido para um array de char como se por uma chamada para [wcrtomb](<#/doc/string/multibyte/wcrtomb>) com estado de conversão inicializado com zero.  |  N/A |  N/A | char* | wchar_t* |  N/A |  N/A |  N/A |  N/A |  N/A  
`d`  
`i` | 

    Converte um **inteiro com sinal** para representação decimal _[-]dddd_. 
A _precisão_ especifica o número mínimo de dígitos a aparecer. A precisão padrão é 1.  
Se tanto o valor convertido quanto a precisão forem ​0​, a conversão resulta em nenhum caractere.  | signed char | short | int | long | long long | [intmax_t](<#/doc/types/integer>) | signed [size_t](<#/doc/types/size_t>) | [ptrdiff_t](<#/doc/types/ptrdiff_t>) |  N/A  
`o` | 

    Converte um **inteiro sem sinal** para representação octal _oooo_. 
A _precisão_ especifica o número mínimo de dígitos a aparecer. A precisão padrão é 1. Se tanto o valor convertido quanto a precisão forem ​0​, a conversão resulta em nenhum caractere. Na _implementação alternativa_, a precisão é aumentada se necessário, para escrever um zero à esquerda. Nesse caso, se tanto o valor convertido quanto a precisão forem ​0​, um único ​0​ é escrito.  | unsigned char | unsigned short | unsigned int | unsigned long | unsigned long long | [uintmax_t](<#/doc/types/integer>) | [size_t](<#/doc/types/size_t>) | versão unsigned de [ptrdiff_t](<#/doc/types/ptrdiff_t>) |  N/A  
`x`  
`X` | 

    Converte um **inteiro sem sinal** para representação hexadecimal _hhhh_. 
Para a conversão `x`, as letras `abcdef` são usadas.  
Para a conversão `X`, as letras `ABCDEF` são usadas.  
A _precisão_ especifica o número mínimo de dígitos a aparecer. A precisão padrão é 1. Se tanto o valor convertido quanto a precisão forem ​0​, a conversão resulta em nenhum caractere. Na _implementação alternativa_, `0x` ou `0X` é prefixado aos resultados se o valor convertido for diferente de zero.  |  N/A  
`u` | 

    Converte um **inteiro sem sinal** para representação decimal _dddd_. 
A _precisão_ especifica o número mínimo de dígitos a aparecer. A precisão padrão é 1. Se tanto o valor convertido quanto a precisão forem ​0​, a conversão resulta em nenhum caractere.  |  N/A  
`f`  
`F` | 

    Converte **número de ponto flutuante** para a notação decimal no estilo _[-]ddd.ddd_. 
A _precisão_ especifica o número exato de dígitos a aparecer após o caractere de ponto decimal. A precisão padrão é 6. Na _implementação alternativa_, o caractere de ponto decimal é escrito mesmo que nenhum dígito o siga. Para o estilo de conversão de infinito e não-número, veja as notas.  |  N/A |  N/A | double | double(C99) |  N/A |  N/A |  N/A |  N/A | long double  
`e`  
`E` | 

    Converte **número de ponto flutuante** para a notação de expoente decimal. 
Para o estilo de conversão `e`, _[-]d.ddd_ ﻿`e` _±dd_ é usado.  
Para o estilo de conversão `E`, _[-]d.ddd_ ﻿`E` _±dd_ é usado.  
O expoente contém pelo menos dois dígitos, mais dígitos são usados apenas se necessário. Se o valor for ​0​, o expoente também é ​0​. A _precisão_ especifica o número exato de dígitos a aparecer após o caractere de ponto decimal. A precisão padrão é 6. Na _implementação alternativa_, o caractere de ponto decimal é escrito mesmo que nenhum dígito o siga. Para o estilo de conversão de infinito e não-número, veja as notas.  |  N/A |  N/A |  N/A |  N/A |  N/A |  N/A  
`a`  
`A` (C99) | 

    Converte **número de ponto flutuante** para a notação de expoente hexadecimal. 
Para o estilo de conversão `a`, _[-]_ ﻿`0x` _h.hhh_ ﻿`p` _±d_ é usado.  
Para o estilo de conversão `A`, _[-]_ ﻿`0X` _h.hhh_ ﻿`P` _±d_ é usado.  
O primeiro dígito hexadecimal não é `0` se o argumento for um valor de ponto flutuante normalizado. Se o valor for ​0​, o expoente também é ​0​. A _precisão_ especifica o número exato de dígitos a aparecer após o caractere de ponto hexadecimal. A precisão padrão é suficiente para a representação exata do valor. Na _implementação alternativa_, o caractere de ponto decimal é escrito mesmo que nenhum dígito o siga. Para o estilo de conversão de infinito e não-número, veja as notas.  |  N/A |  N/A |  N/A |  N/A |  N/A |  N/A  
`g`  
`G` | 

    Converte **número de ponto flutuante** para notação decimal ou de expoente decimal dependendo do valor e da _precisão_. 
Para o estilo de conversão `g`, a conversão com estilo `e` ou `f` será realizada.  
Para o estilo de conversão `G`, a conversão com estilo `E` ou `F` será realizada.  
Seja `P` igual à precisão se diferente de zero, 6 se a precisão não for especificada, ou 1 se a precisão for ​0​. Então, se uma conversão com estilo `E` tivesse um expoente de `X`: 

  * se _P > X ≥ −4_, a conversão é com estilo `f` ou `F` e precisão _P − 1 − X_. 
  * caso contrário, a conversão é com estilo `e` ou `E` e precisão _P − 1_. 

A menos que a _representação alternativa_ seja solicitada, os zeros à direita são removidos, e o caractere de ponto decimal também é removido se nenhuma parte fracionária for deixada. Para o estilo de conversão de infinito e não-número, veja as notas.  |  N/A |  N/A |  N/A |  N/A |  N/A |  N/A  
`n` | 

    Retorna o **número de caracteres escritos** até agora por esta chamada à função. 
O resultado é _escrito_ para o valor apontado pelo argumento. A especificação não pode conter nenhuma _flag_, _largura de campo_ ou _precisão_.  | signed char* | short* | int* | long* | long long* | [intmax_t](<#/doc/types/integer>)* | signed [size_t](<#/doc/types/size_t>)* | [ptrdiff_t](<#/doc/types/ptrdiff_t>)* |  N/A  
`p` | Escreve uma sequência de caracteres definida pela implementação que define um **ponteiro**.  |  N/A |  N/A | void* |  N/A |  N/A |  N/A |  N/A |  N/A |  N/A  
  
As funções de conversão de ponto flutuante convertem infinito para `inf` ou `infinity`. Qual delas é usada é definida pela implementação. 

Não-é-um-número é convertido para `nan` ou `nan(_char_sequence_)`. Qual delas é usada é definida pela implementação. 

As conversões `F`, `E`, `G`, `A` produzem `INF`, `INFINITY`, `NAN` em vez disso. 

O especificador de conversão usado para imprimir char, unsigned char, signed char, short e unsigned short espera tipos promovidos de [promoções de argumento padrão](<#/doc/language/conversion>), mas antes de imprimir seu valor será convertido para char, unsigned char, signed char, short e unsigned short. É seguro passar valores desses tipos por causa da promoção que ocorre quando uma função variádica é chamada. 

As especificações de conversão corretas para os tipos de caracteres de largura fixa ([int8_t](<#/doc/types/integer>), etc) são definidas no cabeçalho [`<inttypes.h>`](<#/doc/types/integer>) (embora [PRIdMAX](<#/doc/types/integer>), [PRIuMAX](<#/doc/types/integer>), etc sejam sinônimos de `%jd`, `%ju`, etc). 

O especificador de conversão de escrita de memória `%n` é um alvo comum de exploits de segurança onde as strings de formato dependem da entrada do usuário e não é suportado pela família de funções `printf_s` com verificação de limites. 

Existe um [ponto de sequência](<#/doc/language/eval_order>) após a ação de cada especificador de conversão; isso permite armazenar múltiplos resultados de `%n` na mesma variável ou, como um caso extremo, imprimir uma string modificada por um `%n` anterior dentro da mesma chamada. 

Se uma especificação de conversão for inválida, o comportamento é indefinido. 

### Valor de retorno

1-3) O número de caracteres escritos se bem-sucedido ou valor negativo se ocorreu um erro.

4) O número de caracteres escritos se bem-sucedido ou valor negativo se ocorreu um erro. Se a string resultante for truncada devido ao limite de buf_size, a função retorna o número total de caracteres (não incluindo o byte nulo terminador) que teriam sido escritos, se o limite não tivesse sido imposto.

5,6) número de caracteres transmitidos para o fluxo de saída ou valor negativo se ocorreu um erro de saída, um erro de violação de restrições de tempo de execução ou um erro de codificação.

7) número de caracteres escritos no buffer, sem contar o caractere nulo (que é sempre escrito desde que buffer não seja um ponteiro nulo e bufsz não seja zero e não seja maior que RSIZE_MAX), ou zero em violações de restrições de tempo de execução, e valor negativo em erros de codificação

8) número de caracteres sem incluir o caractere nulo terminador (que é sempre escrito desde que buffer não seja um ponteiro nulo e bufsz não seja zero e não seja maior que RSIZE_MAX), que teriam sido escritos no buffer se bufsz fosse ignorado, ou um valor negativo se ocorreu uma violação de restrições de tempo de execução ou um erro de codificação

### Notas

Todas essas funções invocam va_arg pelo menos uma vez, o valor de arg é indeterminado após o retorno. Essas funções não invocam va_end, e isso deve ser feito pelo chamador. 

`vsnprintf_s`, ao contrário de `vsprintf_s`, truncará o resultado para caber dentro do array apontado por buffer. 

A implementação de `vsnprintf_s` no [Microsoft CRT](<https://learn.microsoft.com/en-us/cpp/c-runtime-library/reference/vsnprintf-s-vsnprintf-s-vsnprintf-s-l-vsnwprintf-s-vsnwprintf-s-l>) não está em conformidade com o padrão C. A versão da Microsoft tem um parâmetro extra [size_t](<#/doc/types/size_t>) count na terceira posição que contém a quantidade máxima de caracteres a serem escritos, sem incluir o terminador nulo. Este parâmetro é possivelmente distinto do tamanho do buffer fornecido através do parâmetro [size_t](<#/doc/types/size_t>) bufsz. 

### Exemplo

Execute este código
```c
    #include <stdarg.h>
    #include <stdio.h>
    #include <time.h>
    
    void debug_log(const char* fmt, ...)
    {
        struct timespec ts;
        timespec_get(&ts, TIME_UTC);
        char time_buf[100];
        size_t rc = strftime(time_buf, sizeof time_buf, "%D %T", gmtime(&ts.tv_sec));
        snprintf(time_buf + rc, sizeof time_buf - rc, ".%06ld UTC", ts.tv_nsec / 1000);
    
        va_list args1;
        va_start(args1, fmt);
        va_list args2;
        va_copy(args2, args1);
        char buf1+vsnprintf([NULL, 0, fmt, args1)];
        va_end(args1);
        vsnprintf(buf, sizeof buf, fmt, args2);
        va_end(args2);
    
        printf("%s [debug]: %s\n", time_buf, buf);
    }
    
    int main(void)
    {
        debug_log("Logging, %d, %d, %d", 1, 2, 3);
    }
```

Saída possível: 
```
    02/20/15 21:58:09.072683 UTC [debug]: Logging, 1, 2, 3
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.21.6.8 A função vfprintf (p: TBD) 

    

  * 7.21.6.10 A função vprintf (p: TBD) 

    

  * 7.21.6.12 A função vsnprintf (p: TBD) 

    

  * 7.21.6.13 A função vsprintf (p: TBD) 

    

  * K.3.5.3.8 A função vfprintf_s (p: TBD) 

    

  * K.3.5.3.10 A função vprintf_s (p: TBD) 

    

  * K.3.5.3.12 A função vsnprintf_s (p: TBD) 

    

  * K.3.5.3.13 A função vsprintf_s (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.21.6.8 A função vfprintf (p: 238) 

    

  * 7.21.6.10 A função vprintf (p: 239) 

    

  * 7.21.6.12 A função vsnprintf (p: 239-240) 

    

  * 7.21.6.13 A função vsprintf (p: 240) 

    

  * K.3.5.3.8 A função vfprintf_s (p: 434) 

    

  * K.3.5.3.10 A função vprintf_s (p: 435) 

    

  * K.3.5.3.12 A função vsnprintf_s (p: 436-437) 

    

  * K.3.5.3.13 A função vsprintf_s (p: 437) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.21.6.8 A função vfprintf (p: 326-327) 

    

  * 7.21.6.10 A função vprintf (p: 328) 

    

  * 7.21.6.12 A função vsnprintf (p: 329) 

    

  * 7.21.6.13 A função vsprintf (p: 329) 

    

  * K.3.5.3.8 A função vfprintf_s (p: 597) 

    

  * K.3.5.3.10 A função vprintf_s (p: 598-599) 

    

  * K.3.5.3.12 A função vsnprintf_s (p: 600) 

    

  * K.3.5.3.13 A função vsprintf_s (p: 601) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.19.6.8 A função vfprintf (p: 292) 

    

  * 7.19.6.10 A função vprintf (p: 293) 

    

  * 7.19.6.12 A função vsnprintf (p: 294) 

    

  * 7.19.6.13 A função vsprintf (p: 295) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.9.6.7 A função vfprintf 

    

  * 4.9.6.8 A função vprintf 

    

  * 4.9.6.9 A função vsprintf 

### Veja também

[ vwprintfvfwprintfvswprintfvwprintf_svfwprintf_svswprintf_svsnwprintf_s](<#/doc/io/vfwprintf>)(C95)(C95)(C95)(C11)(C11)(C11)(C11) |  imprime saída formatada de caracteres largos para [stdout](<#/doc/io/std_streams>), um fluxo de arquivo  
ou um buffer usando lista de argumentos variáveis   
(função)  
[ printffprintfsprintfsnprintfprintf_sfprintf_ssprintf_ssnprintf_s](<#/doc/io/fprintf>)(C99)(C11)(C11)(C11)(C11) |  imprime saída formatada para [stdout](<#/doc/io/std_streams>), um fluxo de arquivo ou um buffer   
(função)  
[ vscanfvfscanfvsscanfvscanf_svfscanf_svsscanf_s](<#/doc/io/vfscanf>)(C99)(C99)(C99)(C11)(C11)(C11) |  lê entrada formatada de [stdin](<#/doc/io/std_streams>), um fluxo de arquivo ou um buffer  
usando lista de argumentos variáveis   
(função)  
[Documentação C++](<#/>) para vprintf, vfprintf, vsprintf, vsnprintf