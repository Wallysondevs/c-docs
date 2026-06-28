# Utilitários de Data e Hora

### Funções  
  
##### Manipulação de Tempo   
  
---  
Definido no cabeçalho `<time.h>`  
[ difftime](<#/doc/chrono/difftime>) | calcula a diferença entre tempos   
(função)  
[ time](<#/doc/chrono/time>) | retorna o tempo de calendário atual do sistema como tempo desde a época   
(função)  
[ clock](<#/doc/chrono/clock>) | retorna o tempo de clock bruto do processador desde o início do programa   
(função)  
[ timespec_get](<#/doc/chrono/timespec_get>)(C11) | retorna o tempo de calendário em segundos e nanossegundos com base em uma dada base de tempo   
(função)  
[ timespec_getres](<#/doc/chrono/timespec_getres>)(C23) | retorna a resolução do tempo de calendário com base em uma dada base de tempo   
(função)  
  
##### Conversões de Formato   
  
Definido no cabeçalho `<time.h>`  
[ asctimeasctime_s](<#/doc/chrono/asctime>)(obsoleto em C23)(C11) | converte um objeto [tm](<#/doc/chrono/tm>) para uma representação textual   
(função)  
[ ctimectime_s](<#/doc/chrono/ctime>)(obsoleto em C23)(C11) | converte um objeto [time_t](<#/doc/chrono/time_t>) para uma representação textual   
(função)  
[ strftime](<#/doc/chrono/strftime>) | converte um objeto [tm](<#/doc/chrono/tm>) para uma representação textual personalizada   
(função)  
Definido no cabeçalho `[`<wchar.h>`](<#/doc/string/wide>)`  
[ wcsftime](<#/doc/chrono/wcsftime>)(C95) | converte um objeto [tm](<#/doc/chrono/tm>) para uma representação textual de string larga personalizada   
(função)  
Definido no cabeçalho `<time.h>`  
[ gmtimegmtime_rgmtime_s](<#/doc/chrono/gmtime>)(C23)(C11) | converte o tempo desde a época para o tempo de calendário expresso como Tempo Universal Coordenado (UTC)   
(função)  
[ localtimelocaltime_rlocaltime_s](<#/doc/chrono/localtime>)(C23)(C11) | converte o tempo desde a época para o tempo de calendário expresso como tempo local   
(função)  
[ mktime](<#/doc/chrono/mktime>) | converte o tempo de calendário para o tempo desde a época   
(função)  
  
### Constantes

Definido no cabeçalho `<time.h>`  
---  
[ CLOCKS_PER_SEC](<#/doc/chrono/CLOCKS_PER_SEC>) | número de tiques de clock do processador por segundo   
(macro constante)  
  
### Tipos

Definido no cabeçalho `<time.h>`  
---  
[ tm](<#/doc/chrono/tm>) | tipo de tempo de calendário  
(estrutura)  
[ time_t](<#/doc/chrono/time_t>) | tipo de tempo de calendário desde a época   
(typedef)  
[ clock_t](<#/doc/chrono/clock_t>) | tipo de tempo do processador desde a era   
(typedef)  
[ timespec](<#/doc/chrono/timespec>)(C11) | tempo em segundos e nanossegundos   
(estrutura)  
  
### Referências

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.27 Data e hora <time.h> (p: 284-291) 

    

  * 7.29.5.1 A função wcsftime (p: 320-321) 

    

  * 7.31.14 Data e hora <time.h> (p: 333) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.27 Data e hora <time.h> (p: 388-397) 

    

  * 7.29.5.1 A função wcsftime (p: 439-440) 

    

  * 7.31.14 Data e hora <time.h> (p: 456) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.23 Data e hora <time.h> (p: 338-347) 

    

  * 7.24.5.1 A função wcsftime (p: 385-386) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.12 DATA E HORA <time.h>

### Veja também

[documentação C++](<#/>) para utilitários de Data e hora em C  
---