# timespec_get

Definido no cabeçalho [`<time.h>`](<#/doc/chrono>)

```c
int timespec_get( struct timespec *ts, int base );  // desde C11
#define TIME_UTC /* implementation-defined */  // desde C11
```

1) Modifica o objeto timespec apontado por ts para conter o tempo de calendário atual na base de tempo base.

2) Expande para um valor adequado para uso como argumento base de `timespec_get`

Outras constantes de macro começando com `TIME_` podem ser fornecidas pela implementação para indicar bases de tempo adicionais

Se base for `TIME_UTC`, então

  * ts->tv_sec é definido como o número de segundos desde uma época definida pela implementação, truncado para um valor inteiro
  * o membro ts->tv_nsec é definido como o número inteiro de nanossegundos, arredondado para a resolução do relógio do sistema

### Parâmetros

- **ts** — ponteiro para um objeto do tipo struct timespec
- **base** — `TIME_UTC` ou outro valor inteiro diferente de zero indicando a base de tempo

### Valor de retorno

O valor de base se bem-sucedido, zero caso contrário.

### Observações

A função POSIX `[`clock_gettime(CLOCK_REALTIME, ts)`](<https://pubs.opengroup.org/onlinepubs/9799919799/functions/clock_getres.html>)` também pode ser usada para preencher um `timespec` com o tempo desde a Época.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <time.h>
    
    int main(void)
    {
        struct timespec ts;
        timespec_get(&ts, TIME_UTC);
        char buff[100];
        strftime(buff, sizeof buff, "%D %T", gmtime(&ts.tv_sec));
        printf("Current time: %s.%09ld UTC\n", buff, ts.tv_nsec);
    }
```

Saída possível:
```
    Current time: 02/18/15 14:34:03.048508855 UTC
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.27.2.5 A função timespec_get (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.27.2.5 A função timespec_get (p: 286)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.27.2.5 A função timespec_get (p: 390)

### Veja também

[ timespec](<#/doc/chrono/timespec>)(C11) | tempo em segundos e nanossegundos
(struct)
[ timespec_getres](<#/doc/chrono/timespec_getres>)(C23) | retorna a resolução do tempo de calendário com base em uma dada base de tempo
(função)
[ time](<#/doc/chrono/time>) | retorna o tempo de calendário atual do sistema como tempo desde a época
(função)
[documentação C++](<#/>) para timespec_get