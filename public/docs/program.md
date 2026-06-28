# Utilitários de suporte ao programa

### Terminação do programa
As seguintes funções gerenciam a terminação do programa e a limpeza de recursos.

Definido no cabeçalho `<stdlib.h>`
---
[ abort](<#/doc/program/abort>) | causa a terminação anormal do programa (sem limpeza)
(função)
[ exit](<#/doc/program/exit>) | causa a terminação normal do programa com limpeza
(função)
[ quick_exit](<#/doc/program/quick_exit>)(C11) | causa a terminação normal do programa sem limpeza completa
(função)
[ _Exit](<#/doc/program/_Exit>)(C99) | causa a terminação normal do programa sem limpeza
(função)
[ atexit](<#/doc/program/atexit>) | registra uma função a ser chamada na invocação de [exit()](<#/doc/program/exit>)
(função)
[ at_quick_exit](<#/doc/program/at_quick_exit>)(C11) | registra uma função a ser chamada na invocação de [`quick_exit`](<#/doc/program/quick_exit>)
(função)
[ EXIT_SUCCESSEXIT_FAILURE](<#/doc/program/EXIT_status>) | indica o status de execução do programa
(macro constante)

### Fluxo de controle inalcançável

Definido no cabeçalho `[`<stddef.h>`](<#/doc/types>)`
---
[ unreachable](<#/doc/program/unreachable>)(C23) | marca um ponto de execução inalcançável
(macro de função)

### Comunicação com o ambiente

Definido no cabeçalho `<stdlib.h>`
---
[ system](<#/doc/program/system>) | chama o processador de comandos do ambiente hospedeiro
(função)
[ getenvgetenv_s](<#/doc/program/getenv>)(C11) | acesso à lista de variáveis de ambiente
(função)

### Consulta de alinhamento de memória

Definido no cabeçalho `<stdlib.h>`
---
[ memalignment](<#/doc/program/memalignment>)(C23) | consulta o alinhamento de um valor de ponteiro
(função)

### Sinais

Várias funções e macros constantes para gerenciamento de sinais são fornecidas.

Definido no cabeçalho `<signal.h>`
---
[ signal](<#/doc/program/signal>) | define um manipulador de sinal para um sinal específico
(função)
[ raise](<#/doc/program/raise>) | executa o manipulador de sinal para um sinal específico
(função)
[ sig_atomic_t](<#/doc/program/sig_atomic_t>) | o tipo inteiro que pode ser acessado como uma entidade atômica a partir de um manipulador de sinal assíncrono
(typedef)
[ SIG_DFLSIG_IGN](<#/doc/program/SIG_strategies>) | define estratégias de manipulação de sinal
(macro constante)
[ SIG_ERR](<#/doc/program/SIG_ERR>) | erro foi encontrado
(macro constante)

##### Tipos de sinal

[ SIGABRTSIGFPESIGILLSIGINTSIGSEGVSIGTERM](<#/doc/program/SIG_types>) | define tipos de sinal
(macro constante)

### Saltos não locais

Definido no cabeçalho `<setjmp.h>`
---
[ setjmp](<#/doc/program/setjmp>) | salva o contexto
(macro de função)
[ longjmp](<#/doc/program/longjmp>) | salta para o local especificado
(função)

##### Tipos

[ jmp_buf](<#/doc/program/jmp_buf>) | tipo de contexto de execução
(typedef)

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.13 Saltos não locais <setjmp.h> (p: 283-284)

    

  * 7.14 Manipulação de sinais <signal.h> (p: 285-287)

    

  * 7.24 Utilitários gerais <stdlib.h> (p: 356-374)

    

  * 7.33.9 Manipulação de sinais <signal.h> (p: 458)

    

  * 7.33.16 Utilitários gerais <stdlib.h> (p: 458)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.13 Saltos não locais <setjmp.h> (p: 191-192)

    

  * 7.14 Manipulação de sinais <signal.h> (p: 193-195)

    

  * 7.22 Utilitários gerais <stdlib.h> (p: 248-262)

    

  * 7.31.7 Manipulação de sinais <signal.h> (p: 332)

    

  * 7.31.12 Utilitários gerais <stdlib.h> (p: 333)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.13 Saltos não locais <setjmp.h> (p: 262-264)

    

  * 7.14 Manipulação de sinais <signal.h> (p: 265-267)

    

  * 7.22 Utilitários gerais <stdlib.h> (p: 340-360)

    

  * 7.31.7 Manipulação de sinais <signal.h> (p: 455)

    

  * 7.31.12 Utilitários gerais <stdlib.h> (p: 456)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.13 Saltos não locais <setjmp.h> (p: 243-245)

    

  * 7.14 Manipulação de sinais <signal.h> (p: 246-248)

    

  * 7.20 Utilitários gerais <stdlib.h> (p: 306-324)

    

  * 7.26.6 Manipulação de sinais <signal.h> (p: 401)

    

  * 7.26.10 Utilitários gerais <stdlib.h> (p: 402)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.6 SALTOS NÃO LOCAIS <setjmp.h>

    

  * 4.7 MANIPULAÇÃO DE SINAIS <signal.h>

    

  * 4.10 UTILITÁRIOS GERAIS <stdlib.h>

    

  * 4.13.5 Manipulação de sinais <signal.h>

    

  * 7.13.7 Utilitários gerais <stdlib.h>

### Veja também

[documentação C++](<#/>) para Utilitários de suporte ao programa
---