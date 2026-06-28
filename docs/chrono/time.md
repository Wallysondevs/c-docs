# time

Definido no cabeçalho [`<time.h>`](<#/doc/chrono>)

```c
time_t time( time_t* arg );
```

Retorna o tempo de calendário atual codificado como um objeto [time_t](<#/doc/chrono/time_t>), e também o armazena no objeto [time_t](<#/doc/chrono/time_t>) apontado por arg (a menos que arg seja um ponteiro nulo)

### Parâmetros

- **arg** — ponteiro para um objeto [time_t](<#/doc/chrono/time_t>) onde o tempo será armazenado, ou um ponteiro nulo

### Valor de retorno

Tempo de calendário atual codificado como objeto [time_t](<#/doc/chrono/time_t>) em caso de sucesso, ([time_t](<#/doc/chrono/time_t>))(-1) em caso de erro. Se arg não for um ponteiro nulo, o valor de retorno também é armazenado no objeto apontado por arg.

### Observações

A codificação do tempo de calendário em [time_t](<#/doc/chrono/time_t>) é não especificada, mas a maioria dos sistemas está em conformidade com a [especificação POSIX](<https://pubs.opengroup.org/onlinepubs/9799919799/functions/time.html>) e retorna um valor de tipo integral que contém o número de segundos desde a [Época](<https://pubs.opengroup.org/onlinepubs/9799919799/basedefs/V1_chap04.html#tag_04_15>). Implementações nas quais [time_t](<#/doc/chrono/time_t>) é um inteiro assinado de 32 bits (muitas implementações históricas) falham no ano [2038](<https://en.wikipedia.org/wiki/Year_2038_problem> "enwiki:Year 2038 problem").

### Exemplo

Execute este código
```c
    #include <stdint.h>
    #include <stdio.h>
    #include <time.h>
    
    int main(void)
    {
        time_t result = time(NULL);
        if (result != (time_t)(-1))
            printf("The current time is %s(%jd seconds since the Epoch)\n",
                   asctime(gmtime(&result)), (intmax_t)result);
    }
```

Saída possível:
```
    The current time is Fri Apr 24 15:05:25 2015
    (1429887925 seconds since the Epoch)
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.27.2.4 A função time (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.27.2.4 A função time (p: 286)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.27.2.4 A função time (p: 391)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.23.2.4 A função time (p: 341)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.12.2.4 A função time

### Veja também

[ localtimelocaltime_rlocaltime_s](<#/doc/chrono/localtime>)(C23)(C11) | converte o tempo desde a época para tempo de calendário expresso como hora local
(função)
[ gmtimegmtime_rgmtime_s](<#/doc/chrono/gmtime>)(C23)(C11) | converte o tempo desde a época para tempo de calendário expresso como Tempo Universal Coordenado (UTC)
(função)
[ timespec_get](<#/doc/chrono/timespec_get>)(C11) | retorna o tempo de calendário em segundos e nanossegundos com base em uma dada base de tempo
(função)
[Documentação C++](<#/>) para time