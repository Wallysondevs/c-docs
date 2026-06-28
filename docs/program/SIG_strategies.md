# SIG_DFL, SIG_IGN

Definido no cabeçalho [`<signal.h>`](<#/doc/program>)

```c
#define SIG_DFL /*implementation defined*/
#define SIG_IGN /*implementation defined*/
```

As macros **SIG_DFL** e **SIG_IGN** expandem-se para expressões integrais que não são iguais ao endereço de nenhuma função. As macros definem estratégias de tratamento de sinal para a função [signal](<#/doc/program/signal>)().

Constante | Explicação
`SIG_DFL` | tratamento de sinal padrão
`SIG_IGN` | sinal é ignorado

### Exemplo

Execute este código
```c
    #include <signal.h>
    #include <stdio.h>
     
    int main(void)
    {
        /* using the default signal handler */
        raise(SIGTERM);
        printf("Exit main()\n");   /* never reached */
    }
```

Saída:
```
    (none)
```

### Exemplo

Execute este código
```c
    #include <signal.h>
    #include <stdio.h>
     
    int main(void)
    {
        /* ignoring the signal */
        signal(SIGTERM, SIG_IGN);
        raise(SIGTERM);
        printf("Exit main()\n");
    }
```

Saída:
```
    Exit main()
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.14/3 Tratamento de sinal <signal.h> (p: 193)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.14/3 Tratamento de sinal <signal.h> (p: 265)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.14/3 Tratamento de sinal <signal.h> (p: 246)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.7 TRATAMENTO DE SINAL <signal.h>

### Veja também

[documentação C++](<#/>) para SIG_DFL, SIG_IGN
---