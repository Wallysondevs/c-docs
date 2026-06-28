# tm

Definido no cabeçalho [`<time.h>`](<#/doc/chrono>)

```c
struct tm;
```

Estrutura que armazena uma data e hora de calendário dividida em seus componentes.

### Membros

int tm_sec | segundos após o minuto – `[`​0​`, `61`]`(até C99)`[`​0​`, `60`]`(desde C99)[note 1](<#/doc/chrono/tm>)
(membro público)
int tm_min | minutos após a hora – `[`​0​`, `59`]`
(membro público)
int tm_hour | horas desde a meia-noite – `[`​0​`, `23`]`
(membro público)
int tm_mday | dia do mês – `[`1`, `31`]`
(membro público)
int tm_mon | meses desde janeiro – `[`​0​`, `11`]`
(membro público)
int tm_year | anos desde 1900
(membro público)
int tm_wday | dias desde domingo – `[`​0​`, `6`]`
(membro público)
int tm_yday | dias desde 1º de janeiro – `[`​0​`, `365`]`
(membro público)
int tm_isdst | Flag de Horário de Verão. O valor é positivo se o Horário de Verão estiver em vigor, zero se não estiver e negativo se nenhuma informação estiver disponível
(membro público)

###### Notas

O Padrão exige apenas a presença dos membros supracitados em qualquer ordem. As implementações geralmente adicionam mais membros de dados a esta estrutura.

1.  [↑](<#/doc/chrono/tm>) O intervalo permite um segundo bissexto positivo. Dois segundos bissextos no mesmo minuto não são permitidos (o intervalo C89 0..61 era um defeito)

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <time.h>
     
    int main(void)
    {
        struct tm start = {.tm_year = 2022 - 1900, .tm_mday = 1};
        mktime(&start);
        printf("%s", asctime(&start)); // note implicit trailing '\n'
    }
```

Saída:
```
    Sat Jan  1 00:00:00 2022
```

### Referências

*   Padrão C23 (ISO/IEC 9899:2024):

    *   7.27.1/3 Componentes de tempo (p: TBD)

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.27.1/3 Componentes de tempo (p: 284)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.27.1/3 Componentes de tempo (p: 388)

*   Padrão C99 (ISO/IEC 9899:1999):

    *   7.23.1/3 Componentes de tempo (p: 338)

*   Padrão C89/C90 (ISO/IEC 9899:1990):

    *   4.12.1 Componentes de tempo

### Veja também

[ localtimelocaltime_rlocaltime_s](<#/doc/chrono/localtime>)(C23)(C11) | converte o tempo desde a época para o tempo de calendário expresso como hora local
(função)
[ gmtimegmtime_rgmtime_s](<#/doc/chrono/gmtime>)(C23)(C11) | converte o tempo desde a época para o tempo de calendário expresso como Tempo Universal Coordenado (UTC)
(função)
[Documentação C++](<#/>) para tm