# wcsftime

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
size_t wcsftime( wchar_t* str, size_t count, const wchar_t* format, const struct tm* time );  // desde C95
```

Converte as informações de data e hora de um determinado tempo de calendário `time` para uma string de caracteres largos terminada em nulo `str` de acordo com a [string de formato](<#/doc/chrono/wcsftime>) `format`. Até `count` bytes são escritos.

### Parâmetros

- **str** — ponteiro para o primeiro elemento do array `wchar_t` para saída
- **count** — número máximo de caracteres largos a serem escritos
- **format** — ponteiro para uma string de caracteres largos terminada em nulo especificando o [formato de conversão](<#/doc/chrono/wcsftime>)

### String de formato

A string de formato consiste em zero ou mais especificadores de conversão e caracteres comuns (exceto `%`). Todos os caracteres comuns, incluindo o caractere nulo terminador, são copiados para a string de saída sem modificação. Cada especificação de conversão começa com o caractere `%`, opcionalmente seguido pelo modificador `E` ou `O` (ignorado se não suportado pela localidade), seguido pelo caractere que determina o comportamento do especificador. Os seguintes especificadores de formato estão disponíveis:

Especificador de conversão | Explicação | Campos usados
`%` | escreve o caractere literal `%`. A especificação de conversão completa deve ser `%%`. |
`n`
(desde C99) | escreve o caractere de nova linha |
`t`
(desde C99) | escreve o caractere de tabulação horizontal |
Ano
`Y` | escreve o **ano** como um número decimal, ex: 2017 | `tm_year`
`EY`
(desde C99) | escreve o **ano** na representação alternativa, ex: 平成23年 (ano Heisei 23) em vez de 2011年 (ano 2011) na localidade ja_JP | `tm_year`
`y` | escreve os últimos 2 dígitos do **ano** como um número decimal (intervalo `[00,99]`) | `tm_year`
`Oy`
(desde C99) | escreve os últimos 2 dígitos do **ano** usando o sistema numérico alternativo, ex: 十一 em vez de 11 na localidade ja_JP | `tm_year`
`Ey`
(desde C99) | escreve o **ano** como deslocamento do período de calendário alternativo da localidade `%EC` (dependente da localidade) | `tm_year`
`C`
(desde C99) | escreve os primeiros 2 dígitos do **ano** como um número decimal (intervalo `[00,99]`) | `tm_year`
`EC`
(desde C99) | escreve o nome do **ano (período) base** na representação alternativa da localidade, ex: 平成 (era Heisei) em ja_JP | `tm_year`
`G`
(desde C99) | escreve o **ano baseado em semana ISO 8601**, ou seja, o ano que contém a semana especificada. No ISO 8601, as semanas começam na segunda-feira e a primeira semana do ano deve satisfazer os seguintes requisitos:

  * Inclui 4 de janeiro
  * Inclui a primeira quinta-feira do ano

| `tm_year`, `tm_wday`, `tm_yday`
`g`
(desde C99) | escreve os últimos 2 dígitos do **ano baseado em semana ISO 8601**, ou seja, o ano que contém a semana especificada (intervalo `[00,99]`). No ISO 8601, as semanas começam na segunda-feira e a primeira semana do ano deve satisfazer os seguintes requisitos:

  * Inclui 4 de janeiro
  * Inclui a primeira quinta-feira do ano

| `tm_year`, `tm_wday`, `tm_yday`
Mês
`b` | escreve o nome **abreviado do mês**, ex: `Oct` (dependente da localidade) | `tm_mon`
`Ob`
(C23) | escreve o nome **abreviado do mês** na representação alternativa da localidade | `tm_mon`
`h`
(desde C99) | sinônimo de `b` | `tm_mon`
`B` | escreve o nome **completo do mês**, ex: `October` (dependente da localidade) | `tm_mon`
`OB`
(C23) | escreve o nome **completo do mês** apropriado na representação alternativa da localidade | `tm_mon`
`m` | escreve o **mês** como um número decimal (intervalo `[01,12]`) | `tm_mon`
`Om`
(desde C99) | escreve o **mês** usando o sistema numérico alternativo, ex: 十二 em vez de 12 na localidade ja_JP | `tm_mon`
Semana
`U` | escreve a **semana do ano** como um número decimal (domingo é o primeiro dia da semana) (intervalo `[00,53]`) | `tm_year`, `tm_wday`, `tm_yday`
`OU`
(desde C99) | escreve a **semana do ano**, como por `%U`, usando o sistema numérico alternativo, ex: 五十二 em vez de 52 na localidade ja_JP | `tm_year`, `tm_wday`, `tm_yday`
`W` | escreve a **semana do ano** como um número decimal (segunda-feira é o primeiro dia da semana) (intervalo `[00,53]`) | `tm_year`, `tm_wday`, `tm_yday`
`OW`
(desde C99) | escreve a **semana do ano**, como por `%W`, usando o sistema numérico alternativo, ex: 五十二 em vez de 52 na localidade ja_JP | `tm_year`, `tm_wday`, `tm_yday`
`V`
(desde C99) | escreve a **semana do ano ISO 8601** (intervalo `[01,53]`). No ISO 8601, as semanas começam na segunda-feira e a primeira semana do ano deve satisfazer os seguintes requisitos:

  * Inclui 4 de janeiro
  * Inclui a primeira quinta-feira do ano

| `tm_year`, `tm_wday`, `tm_yday`
`OV`
(desde C99) | escreve a **semana do ano**, como por `%V`, usando o sistema numérico alternativo, ex: 五十二 em vez de 52 na localidade ja_JP | `tm_year`, `tm_wday`, `tm_yday`
Dia do ano/mês
`j` | escreve o **dia do ano** como um número decimal (intervalo `[001,366]`) | `tm_yday`
`d` | escreve o **dia do mês** como um número decimal (intervalo `[01,31]`) | `tm_mday`
`Od`
(desde C99) | escreve o **dia do mês** baseado em zero usando o sistema numérico alternativo, ex: 二十七 em vez de 27 na localidade ja_JP. Um único caractere é precedido por um espaço. | `tm_mday`
`e`
(desde C99) | escreve o **dia do mês** como um número decimal (intervalo `[1,31]`). Um único dígito é precedido por um espaço. | `tm_mday`
`Oe`
(desde C99) | escreve o **dia do mês** baseado em um usando o sistema numérico alternativo, ex: 二十七 em vez de 27 na localidade ja_JP. Um único caractere é precedido por um espaço. | `tm_mday`
Dia da semana
`a` | escreve o nome **abreviado do dia da semana**, ex: `Fri` (dependente da localidade) | `tm_wday`
`A` | escreve o nome **completo do dia da semana**, ex: `Friday` (dependente da localidade) | `tm_wday`
`w` | escreve o **dia da semana** como um número decimal, onde domingo é `0` (intervalo `[0-6]`) | `tm_wday`
`Ow`
(desde C99) | escreve o **dia da semana**, onde domingo é `0`, usando o sistema numérico alternativo, ex: 二 em vez de 2 na localidade ja_JP | `tm_wday`
`u`
(desde C99) | escreve o **dia da semana** como um número decimal, onde segunda-feira é `1` (formato ISO 8601) (intervalo `[1-7]`) | `tm_wday`
`Ou`
(desde C99) | escreve o **dia da semana**, onde segunda-feira é `1`, usando o sistema numérico alternativo, ex: 二 em vez de 2 na localidade ja_JP | `tm_wday`
Hora, minuto, segundo
`H` | escreve a **hora** como um número decimal, relógio de 24 horas (intervalo `[00-23]`) | `tm_hour`
`OH`
(desde C99) | escreve a **hora** do relógio de 24 horas usando o sistema numérico alternativo, ex: 十八 em vez de 18 na localidade ja_JP | `tm_hour`
`I` | escreve a **hora** como um número decimal, relógio de 12 horas (intervalo `[01,12]`) | `tm_hour`
`OI`
(desde C99) | escreve a **hora** do relógio de 12 horas usando o sistema numérico alternativo, ex: 六 em vez de 06 na localidade ja_JP | `tm_hour`
`M` | escreve o **minuto** como um número decimal (intervalo `[00,59]`) | `tm_min`
`OM`
(desde C99) | escreve o **minuto** usando o sistema numérico alternativo, ex: 二十五 em vez de 25 na localidade ja_JP | `tm_min`
`S` | escreve o **segundo** como um número decimal (intervalo `[00,60]`) | `tm_sec`
`OS`
(desde C99) | escreve o **segundo** usando o sistema numérico alternativo, ex: 二十四 em vez de 24 na localidade ja_JP | `tm_sec`
Outros
`c` | escreve a **string padrão de data e hora**, ex: `Sun Oct 17 04:41:13 2010` (dependente da localidade) | todos
`Ec`
(desde C99) | escreve a **string alternativa de data e hora**, ex: usando 平成23年 (ano Heisei 23) em vez de 2011年 (ano 2011) na localidade ja_JP | todos
`x` | escreve a **representação de data** localizada (dependente da localidade) | todos
`Ex`
(desde C99) | escreve a **representação de data alternativa**, ex: usando 平成23年 (ano Heisei 23) em vez de 2011年 (ano 2011) na localidade ja_JP | todos
`X` | escreve a **representação de hora** localizada, ex: 18:40:20 ou 6:40:20 PM (dependente da localidade) | todos
`EX`
(desde C99) | escreve a **representação de hora alternativa** (dependente da localidade) | todos
`D`
(desde C99) | equivalente a **"%m/%d/%y"** | `tm_mon`, `tm_mday`, `tm_year`
`F`
(desde C99) | equivalente a **"%Y-%m-%d"** (o formato de data ISO 8601) | `tm_mon`, `tm_mday`, `tm_year`
`r`
(desde C99) | escreve a hora do **relógio de 12 horas** localizada (dependente da localidade) | `tm_hour`, `tm_min`, `tm_sec`
`R`
(desde C99) | equivalente a **"%H:%M"** | `tm_hour`, `tm_min`
`T`
(desde C99) | equivalente a **"%H:%M:%S"** (o formato de hora ISO 8601) | `tm_hour`, `tm_min`, `tm_sec`
`p` | escreve **a.m. ou p.m.** localizado (dependente da localidade) | `tm_hour`
`z`
(desde C99) | escreve o **deslocamento do UTC** no formato ISO 8601 (ex: `-0430`), ou nenhum caractere se a informação do fuso horário não estiver disponível | `tm_isdst`
`Z` | escreve o **nome ou abreviação do fuso horário** dependente da localidade, ou nenhum caractere se a informação do fuso horário não estiver disponível | `tm_isdst`

### Valor de retorno

Número de caracteres largos escritos no array de caracteres largos apontado por `str`, não incluindo o `L'\0'` terminador em caso de sucesso. Se `count` for atingido antes que a string inteira possa ser armazenada, `0` é retornado e o conteúdo é indefinido.

### Exemplo

Execute este código
```c
    #include <locale.h>
    #include <stdio.h>
    #include <time.h>
    #include <wchar.h>
    
    int main(void)
    {
        wchar_t buff[40];
        struct tm my_time =
        {
            .tm_year = 112, // = ano 2012
            .tm_mon = 9,    // = 10º mês
            .tm_mday = 9,   // = 9º dia
            .tm_hour = 8,   // = 8 horas
            .tm_min = 10,   // = 10 minutos
            .tm_sec = 20    // = 20 segundos
        };
    
        if (wcsftime(buff, sizeof buff, L"%A %c", &my_time))
            printf("%ls\n", buff);
        else
            puts("wcsftime failed");
    
        setlocale(LC_ALL, "ja_JP.utf8");
    
        if (wcsftime(buff, sizeof buff, L"%A %c", &my_time))
            printf("%ls\n", buff);
        else
            puts("wcsftime failed");
    }
```

Saída:
```
    Sunday Sun Oct  9 08:10:20 2012
    日曜日 2012年10月09日 08時10分20秒
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.29.5.1 A função wcsftime (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.29.5.1 A função wcsftime (p: 230-231)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.29.5.1 A função wcsftime (p: 439-440)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.24.5.1 A função wcsftime (p: 385-386)

### Veja também

[ strftime](<#/doc/chrono/strftime>) | converte um objeto [tm](<#/doc/chrono/tm>) para representação textual personalizada
(função)
[Documentação C++](<#/>) para wcsftime