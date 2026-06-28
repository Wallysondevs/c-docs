# SIGTERM, SIGSEGV, SIGINT, SIGILL, SIGABRT, SIGFPE

Definido no cabeçalho [`<signal.h>`](<#/doc/program>)

```c
#define SIGTERM /*implementation defined*/
#define SIGSEGV /*implementation defined*/
#define SIGINT /*implementation defined*/
#define SIGILL /*implementation defined*/
#define SIGABRT /*implementation defined*/
#define SIGFPE /*implementation defined*/
```

Cada uma das constantes de macro acima se expande para uma expressão constante inteira com valores distintos, que representam diferentes sinais enviados ao programa.

Constante | Explicação
`SIGTERM` | solicitação de término, enviada ao programa
`SIGSEGV` | acesso inválido à memória (falha de segmentação)
`SIGINT` | interrupção externa, geralmente iniciada pelo usuário
`SIGILL` | imagem de programa inválida, como instrução inválida
`SIGABRT` | condição de término anormal, como a iniciada por [abort()](<#/doc/program/abort>)
`SIGFPE` | operação aritmética errônea, como divisão por zero

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

[ signal](<#/doc/program/signal>) | define um manipulador de sinal para um sinal específico
(função)
[ raise](<#/doc/program/raise>) | executa o manipulador de sinal para um sinal específico
(função)
[documentação C++](<#/>) para tipos de sinal