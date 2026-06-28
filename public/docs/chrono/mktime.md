# mktime

Definido no cabeçalho [`<time.h>`](<#/doc/chrono>)

```c
time_t mktime( struct tm* arg );
```

Renormaliza o tempo de calendário local expresso como um objeto [struct tm](<#/doc/chrono/tm>) e também o converte para o tempo desde a época como um objeto [time_t](<#/doc/chrono/time_t>). arg->tm_wday e arg->tm_yday são ignorados. Os valores em arg não são verificados quanto a estarem fora do intervalo.

Um valor negativo de arg->tm_isdst faz com que `mktime` tente determinar se o Horário de Verão estava em vigor no tempo especificado.

Se a conversão para `time_t` for bem-sucedida, o objeto arg é modificado. Todos os campos de arg são atualizados para se ajustarem aos seus intervalos apropriados. arg->tm_wday e arg->tm_yday são recalculados usando informações disponíveis em outros campos.

### Parâmetros

- **arg** — ponteiro para um objeto [tm](<#/doc/chrono/tm>) especificando o tempo de calendário local a ser convertido

### Valor de retorno

tempo desde a época como um objeto [time_t](<#/doc/chrono/time_t>) em caso de sucesso, ou -1 se arg não puder ser representado como um objeto [time_t](<#/doc/chrono/time_t>) (POSIX também exige que `EOVERFLOW` seja armazenado em [errno](<#/doc/error/errno>) neste caso).

### Observações

Se o objeto struct [tm](<#/doc/chrono/tm>) foi obtido de POSIX [`strptime`](<https://pubs.opengroup.org/onlinepubs/009695399/functions/strptime.html>) ou função equivalente, o valor de `tm_isdst` é indeterminado e precisa ser definido explicitamente antes de chamar `mktime`.

### Exemplo

Execute este código
```
    #define _POSIX_C_SOURCE 200112L // for setenv on gcc
    #include <stdio.h>
    #include <stdlib.h>
    #include <time.h>
     
    int main(void)
    {
        setenv("TZ", "/usr/share/zoneinfo/America/New_York", 1); // POSIX-specific
     
        struct tm tm = *localtime(&(time_t){time(NULL)});
        printf("Today is           %s", asctime(&tm));
        printf("(DST is %s)\n", tm.tm_isdst ? "in effect" : "not in effect");
        tm.tm_mon -= 100;  // tm_mon is now outside its normal range
        mktime(&tm);       // tm_isdst is not set to -1; today's DST status is used
        printf("100 months ago was %s", asctime(&tm));
        printf("(DST was %s)\n", tm.tm_isdst ? "in effect" : "not in effect");
    }
```

Saída possível:
```
    Today is           Fri Apr 22 11:53:36 2016
    (DST is in effect)
    100 months ago was Sat Dec 22 10:53:36 2007
    (DST was not in effect)
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.27.2.3 A função mktime (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.27.2.3 A função mktime (p: 285-286)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.27.2.3 A função mktime (p: 390-391)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.23.2.3 A função mktime (p: 340-341)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.12.2.3 A função mktime

### Veja também

[ localtimelocaltime_rlocaltime_s](<#/doc/chrono/localtime>)(C23)(C11) | converte o tempo desde a época para o tempo de calendário expresso como tempo local
(função)
[Documentação C++](<#/>) para mktime