# raise

Definido no cabeçalho [`<signal.h>`](<#/doc/program>)

```c
int raise( int sig );
```

Envia o sinal sig para o programa. O manipulador de sinal, especificado usando [signal()](<#/doc/program/signal>), é invocado.

Se a estratégia de manipulação de sinal definida pelo usuário ainda não foi configurada usando [signal()](<#/doc/program/signal>), é definido pela implementação se o sinal será ignorado ou se o manipulador padrão será invocado.

### Parâmetros

- **sig** — o sinal a ser enviado. Pode ser um valor definido pela implementação ou um dos seguintes valores: | [ SIGABRTSIGFPESIGILLSIGINTSIGSEGVSIGTERM](<#/doc/program/SIG_types>) | define tipos de sinal
(constante de macro)

### Valor de retorno

`0` em caso de sucesso, valor diferente de zero em caso de falha.

### Exemplo

Execute este código
```c
    #include <signal.h>
    #include <stdio.h>
    
    void signal_handler(int signal)
    {
        printf("Received signal %d\n", signal);
    }
    
    int main(void)
    {
        // Install a signal handler.
        signal(SIGTERM, signal_handler);
    
        printf("Sending signal %d\n", SIGTERM);
        raise(SIGTERM);
        printf("Exit main()\n");
    }
```

Saída:
```
    Sending signal 15
    Received signal 15
    Exit main()
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.14.2.1 A função raise (p: 194-195)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.14.2.1 A função raise (p: 267)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.14.2.1 A função raise (p: 248)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.7.2.1 A função raise

### Veja também

[ signal](<#/doc/program/signal>) | define um manipulador de sinal para um sinal específico
(função)
[Documentação C++](<#/>) para raise