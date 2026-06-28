# sig_atomic_t

Definido no cabeçalho [`<signal.h>`](<#/doc/program>)

```c
typedef /* unspecified */ sig_atomic_t;
```

Um tipo inteiro que pode ser acessado como uma entidade atômica mesmo na presença de interrupções assíncronas feitas por sinais.

### Exemplo

Execute este código
```
    #include <signal.h>
    #include <stdio.h>
    
    volatile sig_atomic_t gSignalStatus = 0;
    
    void signal_handler(int status)
    {
        gSignalStatus = status;
    }
    
    int main(void)
    {
        /* Install a signal handler. */
        signal(SIGINT, signal_handler);
    
        printf("SignalValue:    %d\n", gSignalStatus);
        printf("Sending signal: %d\n", SIGINT);
        raise(SIGINT);
        printf("SignalValue:    %d\n", gSignalStatus);
    }
```

Saída possível:
```
    SignalValue:    0
    Sending signal: 2
    SignalValue:    2
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.14/2 Manipulação de sinais <signal.h> (p: 194-195)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.14/2 Manipulação de sinais <signal.h> (p: 265)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.14/2 Manipulação de sinais <signal.h> (p: 246)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.7 MANIPULAÇÃO DE SINAIS <signal.h>

### Veja também

[ signal](<#/doc/program/signal>) | define um manipulador de sinal para um sinal específico
(função)
[Documentação C++](<#/>) para sig_atomic_t