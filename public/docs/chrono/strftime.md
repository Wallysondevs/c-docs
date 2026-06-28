# strftime

Definido no cabeçalho [`<time.h>`](<#/doc/chrono>)

```c
size_t strftime( char* str, size_t count,
const char* format, const struct tm* tp );  // até C99
size_t strftime( char* restrict str, size_t count,
const char* restrict format, const struct tm* restrict tp );  // desde C99
```

Converte as informações de data e hora de um determinado tempo de calendário tp para uma string de caracteres multibyte terminada em nulo str de acordo com a [string de formato](<#/doc/chrono/strftime>) format. Até count bytes são escritos.

### Parâmetros

- **str** — ponteiro para o primeiro elemento do array de char para saída
- **count** — número máximo de bytes a serem escritos
- **format** — ponteiro para uma string de caracteres multibyte terminada em nulo especificando o [formato de conversão](<#/doc/chrono/strftime>)
- **tp** — ponteiro para um objeto struct [tm](<#/doc/chrono/tm>) especificando o tempo a ser formatado

### String de formato

A string de formato consiste em zero ou mais especificadores de conversão e caracteres comuns (exceto `%`). Todos os caracteres comuns, incluindo o caractere nulo de terminação, são copiados para a string de saída sem modificação. Cada especificação de conversão começa com o caractere `%`, opcionalmente seguido pelo modificador `E` ou `O` (ignorado se não suportado pela localidade), seguido pelo caractere que determina o comportamento do especificador. Os seguintes especificadores de formato estão disponíveis:

Especificador de
conversão | Explicação | Campos usados
`%` | escreve o literal `%`. A especificação de conversão completa deve ser `%%`. |
`n`
(C99) | escreve o caractere de nova linha |
`t`
(C99) | escreve o caractere de tabulação horizontal |
Ano
`Y` | escreve o **ano** como um número decimal, ex: 2017 | `tm_year`
`EY`
(C99) | escreve o **ano** na representação alternativa, ex: 平成23年 (ano Heisei 23) em vez de 2011年 (ano 2011) na localidade ja_JP | `tm_year`
`y` | escreve os últimos 2 dígitos do **ano** como um número decimal (intervalo `[00,99]`) | `tm_year`
`Oy`
(C99) | escreve os últimos 2 dígitos do **ano** usando o sistema numérico alternativo, ex: 十一 em vez de 11 na localidade ja_JP | `tm_year`
`Ey`
(C99) | escreve o **ano** como deslocamento do período de calendário alternativo da localidade `%EC` (dependente da localidade) | `tm_year`
`C`
(C99) | escreve os primeiros 2 dígitos do **ano** como um número decimal (intervalo `[00,99]`) | `tm_year`
`EC`
(C99) | escreve o nome do **ano base (período)** na representação alternativa da localidade, ex: 平成 (era Heisei) em ja_JP | `tm_year`
`G`
(C99) | escreve o **ano baseado na semana ISO 8601**, ou seja, o ano que contém a semana especificada. No ISO 8601, as semanas começam na segunda-feira e a primeira semana do ano deve satisfazer os seguintes requisitos:

  * Inclui 4 de janeiro
  * Inclui a primeira quinta-feira do ano

| `tm_year`, `tm_wday`, `tm_yday`
`g`
(C99) | escreve os últimos 2 dígitos do **ano baseado na semana ISO 8601**, ou seja, o ano que contém a semana especificada (intervalo `[00,99]`). No ISO 8601, as semanas começam na segunda-feira e a primeira semana do ano deve satisfazer os seguintes requisitos:

  * Inclui 4 de janeiro
  * Inclui a primeira quinta-feira do ano

| `tm_year`, `tm_wday`, `tm_yday`
Mês
`b` | escreve o nome **abreviado do mês**, ex: `Out` (dependente da localidade) | `tm_mon`
`Ob`
(C23) | escreve o nome **abreviado do mês** na representação alternativa da localidade | `tm_mon`
`h`
(C99) | sinônimo de `b` | `tm_mon`
`B` | escreve o nome **completo do mês**, ex: `Outubro` (dependente da localidade) | `tm_mon`
`OB`
(C23) | escreve o nome **completo do mês** apropriado na representação alternativa da localidade | `tm_mon`
`m` | escreve o **mês** como um número decimal (intervalo `[01,12]`) | `tm_mon`
`Om`
(C99) | escreve o **mês** usando o sistema numérico alternativo, ex: 十二 em vez de 12 na localidade ja_JP | `tm_mon`
Semana
`U` | escreve a **semana do ano** como um número decimal (domingo é o primeiro dia da semana) (intervalo `[00,53]`) | `tm_year`, `tm_wday`, `tm_yday`
`OU`
(C99) | escreve a **semana do ano**, como por `%U`, usando o sistema numérico alternativo, ex: 五十二 em vez de 52 na localidade ja_JP | `tm_year`, `tm_wday`, `tm_yday`
`W` | escreve a **semana do ano** como um número decimal (segunda-feira é o primeiro dia da semana) (intervalo `[00,53]`) | `tm_year`, `tm_wday`, `tm_yday`
`OW`
(C99) | escreve a **semana do ano**, como por `%W`, usando o sistema numérico alternativo, ex: 五十二 em vez de 52 na localidade ja_JP | `tm_year`, `tm_wday`, `tm_yday`
`V`
(C99) | escreve a **semana do ano ISO 8601** (intervalo `[01,53]`). No ISO 8601, as semanas começam na segunda-feira e a primeira semana do ano deve satisfazer os seguintes requisitos:

  * Inclui 4 de janeiro
  * Inclui a primeira quinta-feira do ano

| `tm_year`, `tm_wday`, `tm_yday`
`OV`
(C99) | escreve a **semana do ano**, como por `%V`, usando o sistema numérico alternativo, ex: 五十二 em vez de 52 na localidade ja_JP | `tm_year`, `tm_wday`, `tm_yday`
Dia do ano/mês
`j` | escreve o **dia do ano** como um número decimal (intervalo `[001,366]`) | `tm_yday`
`d` | escreve o **dia do mês** como um número decimal (intervalo `[01,31]`) | `tm_mday`
`Od`
(C99) | escreve o **dia do mês** baseado em zero usando o sistema numérico alternativo, ex: 二十七 em vez de 27 na localidade ja_JP. Um único caractere é precedido por um espaço. | `tm_mday`
`e`
(C99) | escreve o **dia do mês** como um número decimal (intervalo `[1,31]`). Um único dígito é precedido por um espaço. | `tm_mday`
`Oe`
(C99) | escreve o **dia do mês** baseado em um usando o sistema numérico alternativo, ex: 二十七 em vez de 27 na localidade ja_JP. Um único caractere é precedido por um espaço. | `tm_mday`
Dia da semana
`a` | escreve o nome **abreviado do dia da semana**, ex: `Sex` (dependente da localidade) | `tm_wday`
`A` | escreve o nome **completo do dia da semana**, ex: `Sexta-feira` (dependente da localidade) | `tm_wday`
`w` | escreve o **dia da semana** como um número decimal, onde domingo é `0` (intervalo `[0-6]`) | `tm_wday`
`Ow`
(C99) | escreve o **dia da semana**, onde domingo é `0`, usando o sistema numérico alternativo, ex: 二 em vez de 2 na localidade ja_JP | `tm_wday`
`u`
(C99) | escreve o **dia da semana** como um número decimal, onde segunda-feira é `1` (formato ISO 8601) (intervalo `[1-7]`) | `tm_wday`
`Ou`
(C99) | escreve o **dia da semana**, onde segunda-feira é `1`, usando o sistema numérico alternativo, ex: 二 em vez de 2 na localidade ja_JP | `tm_wday`
Hora, minuto, segundo
`H` | escreve a **hora** como um número decimal, relógio de 24 horas (intervalo `[00-23]`) | `tm_hour`
`OH`
(C99) | escreve a **hora** do relógio de 24 horas usando o sistema numérico alternativo, ex: 十八 em vez de 18 na localidade ja_JP | `tm_hour`
`I` | escreve a **hora** como um número decimal, relógio de 12 horas (intervalo `[01,12]`) | `tm_hour`
`OI`
(C99) | escreve a **hora** do relógio de 12 horas usando o sistema numérico alternativo, ex: 六 em vez de 06 na localidade ja_JP | `tm_hour`
`M` | escreve o **minuto** como um número decimal (intervalo `[00,59]`) | `tm_min`
`OM`
(C99) | escreve o **minuto** usando o sistema numérico alternativo, ex: 二十五 em vez de 25 na localidade ja_JP | `tm_min`
`S` | escreve o **segundo** como um número decimal (intervalo `[00,60]`) | `tm_sec`
`OS`
(C99) | escreve o **segundo** usando o sistema numérico alternativo, ex: 二十四 em vez de 24 na localidade ja_JP | `tm_sec`
Outros
`c` | escreve a **string padrão de data e hora**, ex: `Dom Out 17 04:41:13 2010` (dependente da localidade) | todos
`Ec`
(C99) | escreve a **string alternativa de data e hora**, ex: usando 平成23年 (ano Heisei 23) em vez de 2011年 (ano 2011) na localidade ja_JP | todos
`x` | escreve a **representação de data** localizada (dependente da localidade) | todos
`Ex`
(C99) | escreve a **representação de data alternativa**, ex: usando 平成23年 (ano Heisei 23) em vez de 2011年 (ano 2011) na localidade ja_JP | todos
`X` | escreve a **representação de hora** localizada, ex: 18:40:20 ou 6:40:20 PM (dependente da localidade) | todos
`EX`
(C99) | escreve a **representação de hora alternativa** (dependente da localidade) | todos
`D`
(C99) | equivalente a **"%m/%d/%y"** | `tm_mon`, `tm_mday`, `tm_year`
`F`
(C99) | equivalente a **"%Y-%m-%d"** (o formato de data ISO 8601) | `tm_mon`, `tm_mday`, `tm_year`
`r`
(C99) | escreve a hora do **relógio de 12 horas** localizada (dependente da localidade) | `tm_hour`, `tm_min`, `tm_sec`
`R`
(C99) | equivalente a **"%H:%M"** | `tm_hour`, `tm_min`
`T`
(C99) | equivalente a **"%H:%M:%S"** (o formato de hora ISO 8601) | `tm_hour`, `tm_min`, `tm_sec`
`p` | escreve **a.m. ou p.m.** localizado (dependente da localidade) | `tm_hour`
`z`
(C99) | escreve o **deslocamento do UTC** no formato ISO 8601 (ex: `-0430`), ou nenhum caractere se a informação de fuso horário não estiver disponível | `tm_isdst`
`Z` | escreve o **nome ou abreviação do fuso horário** dependente da localidade, ou nenhum caractere se a informação de fuso horário não estiver disponível | `tm_isdst`

### Valor de retorno

O número de bytes escritos no array de caracteres apontado por str, não incluindo o '\0' de terminação, em caso de sucesso. Se count for atingido antes que a string inteira possa ser armazenada, ​0​ é retornado e o conteúdo é indeterminado.

### Exemplo

Execute este código
```c
    #include <locale.h>
    #include <stdio.h>
    #include <time.h>
     
    int main(void)
    {
        char buff[70];
        struct tm my_time = { .tm_year=112, // = year 2012
                              .tm_mon=9,    // = 10th month
                              .tm_mday=9,   // = 9th day
                              .tm_hour=8,   // = 8 hours
                              .tm_min=10,   // = 10 minutes
                              .tm_sec=20    // = 20 secs
        };
     
        if (strftime(buff, sizeof buff, "%A %c", &my_time))
            puts(buff);
        else
            puts("strftime failed");
     
        setlocale(LC_TIME, "el_GR.utf8");
     
        if (strftime(buff, sizeof buff, "%A %c", &my_time))
            puts(buff);
        else
            puts("strftime failed");
    }
```

Saída possível:
```
    Sunday Sun Oct  9 08:10:20 2012
    Κυριακή Κυρ 09 Οκτ 2012 08:10:20 πμ EST
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.27.3.5 A função strftime (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.27.3.5 A função strftime (p: 288-291)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.27.3.5 A função strftime (p: 394-397)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.23.3.5 A função strftime (p: 343-347)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.12.3.5 A função strftime

### Veja também

[ asctimeasctime_s](<#/doc/chrono/asctime>)(obsoleto em C23)(C11) | converte um objeto [tm](<#/doc/chrono/tm>) para uma representação textual
(função)
[ ctimectime_s](<#/doc/chrono/ctime>)(obsoleto em C23)(C11) | converte um objeto [time_t](<#/doc/chrono/time_t>) para uma representação textual
(função)
[ wcsftime](<#/doc/chrono/wcsftime>)(C95) | converte um objeto [tm](<#/doc/chrono/tm>) para uma representação textual de string larga personalizada
(função)
[Documentação C++](<#/>) para strftime