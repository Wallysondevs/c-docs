# fpos_t

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
typedef /* implementation-defined */ fpos_t;
```

`fpos_t` é um tipo de objeto completo não-array, que pode ser usado para armazenar (por [fgetpos](<#/doc/io/fgetpos>)) e restaurar (por [fsetpos](<#/doc/io/fsetpos>)) a posição e o estado do analisador multibyte (se houver) para um fluxo C.

O estado do analisador multibyte de um fluxo C orientado a caracteres largos é representado por um objeto [mbstate_t](<#/doc/string/multibyte/mbstate_t>), cujo valor é armazenado como parte do valor de um objeto `fpos_t` por [fgetpos](<#/doc/io/fgetpos>). | (desde C95)

### Referências

  * C17 standard (ISO/IEC 9899:2018):

    

  * 7.21.1 Introduction (p: 217-218)

    

  * 7.21.2 Streams (p: 218-219)

  * C11 standard (ISO/IEC 9899:2011):

    

  * 7.21.1 Introduction (p: 296-298)

    

  * 7.21.2 Streams (p: 298-299)

  * C99 standard (ISO/IEC 9899:1999):

    

  * 7.19.1 Introduction (p: 262-264)

    

  * 7.19.2 Streams (p: 264-265)

  * C89/C90 standard (ISO/IEC 9899:1990):

    

  * 4.9.1 Introduction

    

  * 4.9.2 Streams

### Veja também

[ fgetpos](<#/doc/io/fgetpos>) | obtém o indicador de posição do arquivo
(função)
[ fsetpos](<#/doc/io/fsetpos>) | move o indicador de posição do arquivo para um local específico em um arquivo
(função)
[ mbstate_t](<#/doc/string/multibyte/mbstate_t>)(C95) | informações de estado de conversão necessárias para iterar strings de caracteres multibyte
(classe)
[Documentação C++](<#/>) para fpos_t