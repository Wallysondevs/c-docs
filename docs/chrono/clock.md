# clock

Definido no cabeçalho [`<time.h>`](<#/doc/chrono>)

```c
clock_t clock(void);
```

Retorna o tempo de processador aproximado usado pelo processo desde o início de uma era definida pela implementação, relacionada à execução do programa. Para converter o valor do resultado para segundos, divida-o por [CLOCKS_PER_SEC](<#/doc/chrono/CLOCKS_PER_SEC>).

Apenas a diferença entre dois valores retornados por chamadas diferentes a `clock` é significativa, pois o início da era `clock` não precisa coincidir com o início do programa.

O tempo de `clock` pode avançar mais rápido ou mais lento que o tempo de relógio de parede, dependendo dos recursos de execução concedidos ao programa pelo sistema operacional. Por exemplo, se a CPU for compartilhada por outros processos, o tempo de `clock` pode avançar mais lentamente que o tempo de relógio de parede. Por outro lado, se o processo atual for multithreaded e mais de um núcleo de execução estiver disponível, o tempo de `clock` pode avançar mais rapidamente que o tempo de relógio de parede.

### Valor de retorno

Tempo de processador usado pelo programa até o momento.

*   Se o tempo de processador usado não estiver disponível, retorna ([clock_t](<#/doc/chrono/clock_t>))(-1).
*   Se o valor do tempo de processador usado não puder ser representado por [clock_t](<#/doc/chrono/clock_t>), retorna um valor não especificado.

### Notas

Em sistemas compatíveis com POSIX, [`clock_gettime`](<http://pubs.opengroup.org/onlinepubs/9699919799/functions/clock_getres.html>) com o ID de clock CLOCK_PROCESS_CPUTIME_ID oferece melhor resolução.

O valor retornado por `clock()` pode estourar em algumas implementações. Por exemplo, em tal implementação, se [clock_t](<#/doc/chrono/clock_t>) for um inteiro assinado de 32 bits e [CLOCKS_PER_SEC](<#/doc/chrono/CLOCKS_PER_SEC>) for 1000000, ele estourará após cerca de 2147 segundos (cerca de 36 minutos).

### Exemplo

Este exemplo demonstra a diferença entre o tempo de `clock()` e o tempo real.

Execute este código
```c
    #ifndef __STDC_NO_THREADS__
        #include <threads.h>
    #else
        // POSIX alternative
        #define _POSIX_C_SOURCE 199309L
        #include <pthread.h>
    #endif
    
    #include <stdio.h>
    #include <stdlib.h>
    #include <time.h>
    
    // the function f() does some time-consuming work
    int f(void* thr_data) // return void* in POSIX
    {
        (void) thr_data;
        volatile double d = 0;
        for (int n = 0; n < 10000; ++n)
           for (int m = 0; m < 10000; ++m)
               d += d * n * m;
        return 0;
    }
    
    int main(void)
    {
        struct timespec ts1, tw1; // both C11 and POSIX
        clock_gettime(CLOCK_PROCESS_CPUTIME_ID, &ts1); // POSIX
        clock_gettime(CLOCK_MONOTONIC, &tw1); // POSIX; use timespec_get in C11
        clock_t t1 = clock();
    
    #ifndef __STDC_NO_THREADS__
        thrd_t thr1, thr2;  // C11; use pthread_t in POSIX
        thrd_create(&thr1, f, NULL); // C11; use pthread_create in POSIX
        thrd_create(&thr2, f, NULL);
        thrd_join(thr1, NULL); // C11; use pthread_join in POSIX
        thrd_join(thr2, NULL);
    #endif
    
        struct timespec ts2, tw2;
        clock_gettime(CLOCK_PROCESS_CPUTIME_ID, &ts2);
        clock_gettime(CLOCK_MONOTONIC, &tw2);
        clock_t t2 = clock();
    
        double dur = 1000.0 * (t2 - t1) / CLOCKS_PER_SEC;
        double posix_dur = 1000.0 * ts2.tv_sec + 1e-6 * ts2.tv_nsec
                               - (1000.0 * ts1.tv_sec + 1e-6 * ts1.tv_nsec);
        double posix_wall = 1000.0 * tw2.tv_sec + 1e-6 * tw2.tv_nsec
                                - (1000.0 * tw1.tv_sec + 1e-6 * tw1.tv_nsec);
    
        printf("CPU time used (per clock()): %.2f ms\n", dur);
        printf("CPU time used (per clock_gettime()): %.2f ms\n", posix_dur);
        printf("Wall time passed: %.2f ms\n", posix_wall);
    }
```

Saída possível:
```
    CPU time used (per clock()): 1580.00 ms
    CPU time used (per clock_gettime()): 1582.76 ms
    Wall time passed: 792.13 ms
```

### Referências

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.27.2.1 A função clock (p: 285)
*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.27.2.1 A função clock (p: 389)
*   Padrão C99 (ISO/IEC 9899:1999):

    *   7.23.2.1 A função clock (p: 339)
*   Padrão C89/C90 (ISO/IEC 9899:1990):

    *   4.12.2.1 A função clock

### Veja também

[ ctimectime_s](<#/doc/chrono/ctime>)(obsoleto em C23)(C11) | converte um objeto [time_t](<#/doc/chrono/time_t>) em uma representação textual
(função)
[ time](<#/doc/chrono/time>) | retorna o tempo de calendário atual do sistema como tempo desde a época
(função)
[Documentação C++](<#/>) para clock