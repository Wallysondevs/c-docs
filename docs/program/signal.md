# signal

Definido no cabeçalho [`<signal.h>`](<#/doc/program>)

```c
void (*signal( int sig, void (*handler) (int))) (int);
```

Define o manipulador de sinal para o sinal `sig`. O manipulador de sinal pode ser configurado para que o tratamento padrão ocorra, o sinal seja ignorado ou uma função definida pelo usuário seja chamada.

Quando o manipulador de sinal é definido para uma função e um sinal ocorre, é definido pela implementação se `signal(sig, [SIG_DFL](<#/doc/program/SIG_strategies>))` será executado imediatamente antes do início do manipulador de sinal. Além disso, a implementação pode impedir que um conjunto de sinais definido pela implementação ocorra enquanto o manipulador de sinal é executado.

### Parâmetros

- **sig** — o sinal para o qual definir o manipulador de sinal. Pode ser um valor definido pela implementação ou um dos seguintes valores: | [ SIGABRTSIGFPESIGILLSIGINTSIGSEGVSIGTERM](<#/doc/program/SIG_types>) | define tipos de sinal (macro constante)
- **handler** — o manipulador de sinal. Deve ser um dos seguintes:

  * macro [SIG_DFL](<#/doc/program/SIG_strategies>). O manipulador de sinal é definido para o manipulador de sinal padrão.
  * macro [SIG_IGN](<#/doc/program/SIG_strategies>). O sinal é ignorado.
  * ponteiro para uma função. A assinatura da função deve ser equivalente à seguinte:

| void fun(int sig);

### Valor de retorno

Manipulador de sinal anterior em caso de sucesso ou [SIG_ERR](<#/doc/program/SIG_ERR>) em caso de falha (a configuração de um manipulador de sinal pode ser desabilitada em algumas implementações).

### Manipulador de sinal

As seguintes limitações são impostas à função definida pelo usuário que é instalada como um manipulador de sinal.

Se a função definida pelo usuário retornar ao manipular [SIGFPE](<#/doc/program/SIG_types>), [SIGILL](<#/doc/program/SIG_types>) ou [SIGSEGV](<#/doc/program/SIG_types>), o comportamento é indefinido.

Se o manipulador de sinal for chamado como resultado de [abort](<#/doc/program/abort>) ou [raise](<#/doc/program/raise>), o comportamento é indefinido se o manipulador de sinal chamar [raise](<#/doc/program/raise>).

Se o manipulador de sinal for chamado NÃO como resultado de [abort](<#/doc/program/abort>) ou [raise](<#/doc/program/raise>) (em outras palavras, o manipulador de sinal é _assíncrono_), o comportamento é indefinido se

  * o manipulador de sinal chamar qualquer função da biblioteca padrão, exceto

    

  * [abort](<#/doc/program/abort>)
  * [_Exit](<#/doc/program/_Exit>)
  * [quick_exit](<#/doc/program/quick_exit>)
  * `signal` com o primeiro argumento sendo o número do sinal atualmente manipulado (um manipulador assíncrono pode se registrar novamente, mas não outros sinais).
  * funções atômicas de [`<stdatomic.h>`](<#/doc/thread>) se os argumentos atômicos forem lock-free
  * [atomic_is_lock_free](<#/doc/atomic/atomic_is_lock_free>) (com qualquer tipo de argumentos atômicos)

  * o manipulador de sinal se referir a qualquer objeto com [duração de armazenamento](<#/doc/language/storage_duration>) estática ou thread-local (desde C11) que não seja um [atômico](<#/doc/language/atomic>) lock-free (desde C11), exceto por atribuição a um [sig_atomic_t](<#/doc/program/sig_atomic_t>) volátil estático.

Na entrada do manipulador de sinal, o estado do ambiente de ponto flutuante e os valores de todos os objetos são não especificados, exceto para

  * objetos do tipo volatile [sig_atomic_t](<#/doc/program/sig_atomic_t>)
  * objetos de tipos atômicos lock-free (desde C11)
  * efeitos colaterais tornados visíveis através de [atomic_signal_fence](<#/doc/atomic/atomic_signal_fence>) (desde C11)

No retorno de um manipulador de sinal, o valor de qualquer objeto modificado pelo manipulador de sinal que não seja volatile [sig_atomic_t](<#/doc/program/sig_atomic_t>) ou atômico lock-free (desde C11) é indefinido.

O comportamento é indefinido se `signal` for usado em um programa multithread. Não é exigido que seja thread-safe.

### Notas

POSIX exige que `signal` seja thread-safe e [especifica uma lista de funções de biblioteca async-signal-safe](<http://pubs.opengroup.org/onlinepubs/9699919799/functions/V2_chap02.html#tag_15_04>) que podem ser chamadas de qualquer manipulador de sinal.

Além de `abort` e `raise`, POSIX especifica que `kill`, `pthread_kill` e `sigqueue` geram sinais síncronos.

POSIX recomenda [`sigaction`](<http://pubs.opengroup.org/onlinepubs/9699919799/functions/sigaction.html>) em vez de `signal`, devido ao seu comportamento subespecificado e variações significativas de implementação, em relação à entrega de sinais enquanto um manipulador de sinal é executado.

### Exemplo

Execute este código
```c
    #include <signal.h>
    #include <stdio.h>
    
    volatile sig_atomic_t gSignalStatus;
    
    void signal_handler(int signal)
    {
      gSignalStatus = signal;
    }
    
    int main(void)
    {
      signal(SIGINT, signal_handler);
    
      printf("SignalValue: %d\n", gSignalStatus);
      printf("Sending signal: %d\n", SIGINT);
      raise(SIGINT);
      printf("SignalValue: %d\n", gSignalStatus);
    }
```

Saída:
```
    SignalValue: 0
    Sending signal: 2
    SignalValue: 2
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.14.1.1 A função signal (p: 193-194)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.14.1.1 A função signal (p: 266-267)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.14.1.1 A função signal (p: 247-248)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.7.1.1 A função signal

### Veja também

[ raise](<#/doc/program/raise>) | executa o manipulador de sinal para um sinal específico (função)
[documentação C++](<#/>) para signal