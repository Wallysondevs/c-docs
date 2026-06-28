# thrd_yield

Definido no cabeçalho [`<threads.h>`](<#/doc/thread>)

```c
void thrd_yield(void);  // desde C11
```

Fornece uma dica para a implementação reagendar a execução de threads, permitindo que outras threads sejam executadas.

### Parâmetros

(nenhum)

### Valor de retorno

(nenhum)

### Notas

O comportamento exato desta função depende da implementação, em particular da mecânica do escalonador do sistema operacional em uso e do estado do sistema. Por exemplo, um escalonador de tempo real "first-in-first-out" (`SCHED_FIFO` no Linux) suspenderia a thread atual e a colocaria no final da fila de threads de mesma prioridade que estão prontas para serem executadas, e se não houver outras threads com a mesma prioridade, `yield` não terá efeito.

O equivalente POSIX desta função é [`sched_yield`](<http://pubs.opengroup.org/onlinepubs/9699919799/functions/sched_yield.html>).

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <time.h>
    #include <threads.h>
    
    // utility function: difference between timespecs in microseconds
    double usdiff(struct timespec s, struct timespec e)
    {
        double sdiff = difftime(e.tv_sec, s.tv_sec);
        long nsdiff = e.tv_nsec - s.tv_nsec;
        if(nsdiff < 0) return 1000000*(sdiff-1) + (1000000000L+nsdiff)/1000.0;
        else return 1000000*(sdiff) + nsdiff/1000.0;
    }
    
    // busy wait while yielding
    void sleep_100us()
    {
        struct timespec start, end;
        timespec_get(&start, TIME_UTC);
        do {
            thrd_yield();
            timespec_get(&end, TIME_UTC);
        } while(usdiff(start, end) < 100.0);
    }
    
    int main()
    {
        struct timespec start, end;
        timespec_get(&start, TIME_UTC);
        sleep_100us();
        timespec_get(&end, TIME_UTC);
        printf("Waited for %.3f us\n", usdiff(start, end));
    }
```

Saída possível:
```
    Waited for 100.344 us
```

### Referências

* Padrão C17 (ISO/IEC 9899:2018):

  * 7.26.5.8 A função thrd_yield (p: 281)

* Padrão C11 (ISO/IEC 9899:2011):

  * 7.26.5.8 A função thrd_yield (p: 385)

### Veja também

[ thrd_sleep](<#/doc/thread/thrd_sleep>)(C11) | suspende a execução da thread chamadora pelo período de tempo especificado
(função)
[Documentação C++](<#/>) para yield