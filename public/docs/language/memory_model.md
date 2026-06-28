# Modelo de Memória

Define a semântica do armazenamento da memória do computador para o propósito da máquina abstrata C.

O armazenamento de dados (memória) disponível para um programa C é uma ou mais sequências contíguas de _bytes_. Cada byte na memória possui um _endereço_ único.

### Byte

Um _byte_ é a menor unidade de memória endereçável. É definido como uma sequência contígua de bits, grande o suficiente para armazenar qualquer membro do _conjunto básico de caracteres de execução_ ([os 96 caracteres](<#/doc/language/translation_phases>) que são exigidos como sendo de byte único). C suporta bytes de tamanhos de 8 bits ou mais.

Os [tipos](<#/doc/language/types>) char, unsigned char e signed char usam um byte tanto para armazenamento quanto para [representação de valor](<#/doc/language/object>). O número de bits em um byte é acessível como [CHAR_BIT](<#/doc/types/limits>).

Para o uso de bytes para representar valores de outros tipos fundamentais (incluindo layouts de memória big-endian e little-endian), veja [representação de objeto](<#/doc/language/object>)

### Localização de memória

Uma _localização de memória_ é

*   um objeto de [tipo escalar](<#/doc/language/compatible_type>) (tipo aritmético, tipo ponteiro, tipo enumeração)
*   ou a maior sequência contígua de [campos de bits](<#/doc/language/bit_field>) de comprimento não nulo

```c
    struct S
    {
        char a;     // localização de memória #1
        int b : 5;  // localização de memória #2
        int c : 11, // localização de memória #2 (continuação)
              : 0,
            d : 8;  // localização de memória #3
        struct
        {
            int ee : 8; // localização de memória #4
        } e;
    } obj; // O objeto 'obj' consiste em 4 localizações de memória separadas
```

### Threads e condições de corrida de dados

Um thread de execução é um fluxo de controle dentro de um programa que começa com a invocação de uma função de nível superior por [thrd_create](<#/doc/thread/thrd_create>) ou outros meios. Qualquer thread pode potencialmente acessar qualquer objeto no programa (objetos com [duração de armazenamento](<#/doc/language/storage_duration>) automática e thread-local ainda podem ser acessados por outro thread através de um ponteiro). Diferentes threads de execução são sempre permitidos a acessar (ler e modificar) diferentes _localizações de memória_ concorrentemente, sem interferência e sem requisitos de sincronização. (note que não é seguro atualizar concorrentemente dois campos de bits não atômicos na mesma estrutura se todos os membros declarados entre eles também forem campos de bits (de comprimento não nulo), independentemente dos tamanhos desses campos de bits intermediários) Quando uma [avaliação](<#/doc/language/eval_order>) de uma expressão escreve em uma localização de memória e outra avaliação lê ou modifica a mesma localização de memória, as expressões são ditas _conflitantes_. Um programa que possui duas avaliações conflitantes tem uma _condição de corrida de dados_ (data race) a menos que:

*   ambas as avaliações conflitantes sejam [operações atômicas](<#/doc/language/atomic>)
*   uma das avaliações conflitantes _acontece-antes_ de outra (veja [memory_order](<#/doc/atomic/memory_order>))

Se ocorrer uma condição de corrida de dados, o comportamento do programa é [comportamento indefinido](undefined behavior). (em particular, [mtx_unlock](<#/doc/thread/mtx_unlock>) é _sincronizado-com_ e, portanto, _acontece-antes_ de [mtx_lock](<#/doc/thread/mtx_lock>) do mesmo mutex por outro thread, o que torna possível usar bloqueios de mutex para proteger contra condições de corrida de dados)
| | Esta seção está incompleta
Razão: um ou dois exemplos pequenos

### Ordem de memória

Quando um thread lê um valor de uma localização de memória, ele pode ver o valor inicial, o valor escrito no mesmo thread, ou o valor escrito em outro thread. Veja [memory_order](<#/doc/atomic/memory_order>) para detalhes sobre a ordem em que as escritas feitas por threads se tornam visíveis para outros threads.

(desde C11)

### Referências

*   Padrão C23 (ISO/IEC 9899:2024):

    *   3.6 byte (p: TBD)

    *   3.14 localização de memória (p: TBD)

    *   5.1.2.4 Execuções multi-threaded e condições de corrida de dados (p: TBD)
*   Padrão C17 (ISO/IEC 9899:2018):

    *   3.6 byte (p: TBD)

    *   3.14 localização de memória (p: TBD)

    *   5.1.2.4 Execuções multi-threaded e condições de corrida de dados (p: TBD)
*   Padrão C11 (ISO/IEC 9899:2011):

    *   3.6 byte (p: 4)

    *   3.14 localização de memória (p: 5)

    *   5.1.2.4 Execuções multi-threaded e condições de corrida de dados (p: 17-21)
*   Padrão C99 (ISO/IEC 9899:1999):

    *   3.6 byte (p: 4)
*   Padrão C89/C90 (ISO/IEC 9899:1990):

    *   1.6 DEFINIÇÕES DE TERMOS

### Veja também

[documentação C++](<#/>) para Modelo de Memória
---