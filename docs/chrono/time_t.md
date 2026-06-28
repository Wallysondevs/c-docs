# time_t

Definido no cabeçalho [`<time.h>`](<#/doc/chrono>)

```c
typedef /* não especificado */ time_t;
```

Tipo aritmético real capaz de representar tempos.

Embora não definido pelo padrão C, este é quase sempre um valor integral que armazena o número de segundos (sem contar segundos bissextos) desde 00:00, 1º de janeiro de 1970 UTC, correspondendo ao [ tempo POSIX](<https://en.wikipedia.org/wiki/Unix_time> "enwiki:Unix time").

### Notas

O padrão usa o termo _tempo de calendário_ ao se referir a um valor do tipo **time_t**.

### Exemplo

Mostra o início da época.

Run this code
```
    #include <stdio.h>
    #include <time.h>
    #include <stdint.h>
    
    int main(void)
    {
        time_t epoch = 0;
        printf("%jd seconds since the epoch began\n", (intmax_t)epoch);
        printf("%s", asctime(gmtime(&epoch)));
    }
```

Saída possível:
```
    0 seconds since the epoch began
    Thu Jan  1 00:00:00 1970
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.27.1/3 Componentes de tempo (p: 284)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.27.1/3 Componentes de tempo (p: 388)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.23.1/3 Componentes de tempo (p: 338)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.12.1 Componentes de tempo

### Veja também

[ time](<#/doc/chrono/time>) | retorna o tempo de calendário atual do sistema como tempo desde a época
(função)
[ localtimelocaltime_rlocaltime_s](<#/doc/chrono/localtime>)(C23)(C11) | converte o tempo desde a época para tempo de calendário expresso como hora local
(função)
[ gmtimegmtime_rgmtime_s](<#/doc/chrono/gmtime>)(C23)(C11) | converte o tempo desde a época para tempo de calendário expresso como Tempo Universal Coordenado (UTC)
(função)
[Documentação C++](<#/>) para time_t