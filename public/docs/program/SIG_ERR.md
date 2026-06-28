# SIG_ERR

Definido no cabeçalho [`<signal.h>`](<#/doc/program>)

```c
#define SIG_ERR /* implementation defined */
```

Um valor do tipo `void (*)(int)`. Quando retornado por [signal](<#/doc/program/signal>), indica que ocorreu um erro.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
    #include <signal.h>
    
    void signal_handler(int sig)
    {
        printf("Received signal: %d\n", sig);
    }
    
    int main(void)
    {
        /* Install a signal handler. */
        if (signal(SIGTERM, signal_handler) == SIG_ERR)
        {
            printf("Error while installing a signal handler.\n");
            exit(EXIT_FAILURE);
        }
    
        printf("Sending signal: %d\n", SIGTERM);
        if (raise(SIGTERM) != 0)
        {
            printf("Error while raising the SIGTERM signal.\n");
            exit(EXIT_FAILURE);
        }
    
        printf("Exit main()\n");
        return EXIT_SUCCESS;
    }
```

Saída:
```
    Sending signal: 15
    Received signal: 15
    Exit main()
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.14/3 Manipulação de sinais <signal.h> (p: 194)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.14/3 Manipulação de sinais <signal.h> (p: 265)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.14/3 Manipulação de sinais <signal.h> (p: 246)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.7 MANIPULAÇÃO DE SINAIS <signal.h>

### Veja também

[ signal](<#/doc/program/signal>) | define um manipulador de sinal para um sinal específico
(função)
[Documentação C++](<#/>) para SIG_ERR