# timespec_getres

Definido no cabeçalho [`<time.h>`](<#/doc/chrono>) | | (desde C23)

```c
int timespec_getres( struct timespec *ts, int base );  // desde C23
```

Se `ts` não for nulo e `base` for suportado por timespec_get, modifica *ts para conter a resolução de tempo fornecida por timespec_get para `base`. Para cada `base` suportada, múltiplas chamadas a `timespec_getres` durante a mesma execução do programa têm resultados idênticos.

### Parâmetros

- **ts** — ponteiro para um objeto do tipo struct timespec
- **base** — TIME_UTC ou outro valor inteiro não nulo indicando a base de tempo

### Valor de retorno

O valor de `base` se `base` for suportado, zero caso contrário.

### Notas

A função POSIX [`clock_getres(clock_id, ts)`](<http://pubs.opengroup.org/onlinepubs/9699919799/functions/clock_getres.html>) também pode ser usada para preencher um timespec com a resolução de tempo identificada por `clock_id`.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <time.h>
     
    int main(void)
    {
        char buff[128];
        struct timespec ts;
        const int res = timespec_getres(&ts, TIME_UTC);
        if (res == TIME_UTC) {
            struct tm timer;
            strftime(buff, sizeof buff, "%D %T", gmtime_r(&ts.tv_sec, &timer));
            printf("Time resolution info: %s.%09ld UTC\n", buff, ts.tv_nsec);
        } else {
            printf("TIME_UTC base is not supported.");
        }
    }
```

Saída possível:
```
    Time resolution info: 01/01/70 00:00:00.000000001 UTC
```

### Veja também

[ timespec](<#/doc/chrono/timespec>)(C11) | tempo em segundos e nanossegundos
(struct)
[ timespec_get](<#/doc/chrono/timespec_get>)(C11) | retorna o tempo de calendário em segundos e nanossegundos com base em uma dada base de tempo
(function)
[ time](<#/doc/chrono/time>) | retorna o tempo de calendário atual do sistema como tempo desde a época
(function)