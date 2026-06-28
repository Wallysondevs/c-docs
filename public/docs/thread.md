# Biblioteca de suporte à concorrência

C inclui suporte embutido para threads, operações atômicas, exclusão mútua, variáveis de condição e armazenamentos específicos de thread.

Esses recursos são fornecidos opcionalmente:

  * se a constante de macro `__STDC_NO_THREADS__` for definida pelo compilador, o cabeçalho `< threads.h>` e todos os nomes fornecidos nele não são fornecidos;
  * se a constante de macro `__STDC_NO_ATOMICS__` for definida pelo compilador, o cabeçalho [`<stdatomic.h>`](<#/doc/thread>) e todos os nomes fornecidos nele não são fornecidos.

Veja também [especificador e qualificador de tipo **_Atomic**](<#/doc/language/atomic>).

### Threads

Definido no cabeçalho `<threads.h>`
---
`thrd_t` | tipo de objeto completo definido pela implementação que identifica uma thread
[ thrd_create](<#/doc/thread/thrd_create>)(C11) | cria uma thread
(função)
[ thrd_equal](<#/doc/thread/thrd_equal>)(C11) | verifica se dois identificadores se referem à mesma thread
(função)
[ thrd_current](<#/doc/thread/thrd_current>)(C11) | obtém o identificador da thread atual
(função)
[ thrd_sleep](<#/doc/thread/thrd_sleep>)(C11) | suspende a execução da thread chamadora pelo período de tempo especificado
(função)
[ thrd_yield](<#/doc/thread/thrd_yield>)(C11) | cede a fatia de tempo atual
(função)
[ thrd_exit](<#/doc/thread/thrd_exit>)(C11) | encerra a thread chamadora
(função)
[ thrd_detach](<#/doc/thread/thrd_detach>)(C11) | desvincula uma thread
(função)
[ thrd_join](<#/doc/thread/thrd_join>)(C11) | bloqueia até que uma thread termine
(função)
[ thrd_successthrd_timedoutthrd_busythrd_nomemthrd_error](<#/doc/thread/thrd_errors>)(C11) | indica um status de erro de thread
(constante)
thrd_start_t(C11) | um typedef do tipo ponteiro de função int(*)(void*), usado por [thrd_create](<#/doc/thread/thrd_create>)
(typedef)

### Operações atômicas

Definido no cabeçalho `[`<stdatomic.h>`](<#/doc/thread>)`
---

##### Operações em tipos atômicos

[ ATOMIC_BOOL_LOCK_FREEATOMIC_CHAR_LOCK_FREEATOMIC_CHAR16_T_LOCK_FREEATOMIC_CHAR32_T_LOCK_FREEATOMIC_WCHAR_T_LOCK_FREEATOMIC_SHORT_LOCK_FREEATOMIC_INT_LOCK_FREEATOMIC_LONG_LOCK_FREEATOMIC_LLONG_LOCK_FREEATOMIC_POINTER_LOCK_FREE](<#/doc/atomic/ATOMIC_LOCK_FREE_consts>)(C11) | indica que o tipo atômico fornecido é livre de bloqueio (lock-free)
(constante de macro)
[ atomic_is_lock_free](<#/doc/atomic/atomic_is_lock_free>)(C11) | indica se o objeto atômico é livre de bloqueio (lock-free)
(função)
[ atomic_storeatomic_store_explicit](<#/doc/atomic/atomic_store>)(C11) | armazena um valor em um objeto atômico
(função)
[ atomic_loadatomic_load_explicit](<#/doc/atomic/atomic_load>)(C11) | lê um valor de um objeto atômico
(função)
[ atomic_exchangeatomic_exchange_explicit](<#/>)(C11) | troca um valor com o valor de um objeto atômico
(função)
[ atomic_compare_exchange_strongatomic_compare_exchange_strong_explicitatomic_compare_exchange_weakatomic_compare_exchange_weak_explicit](<#/doc/atomic/atomic_compare_exchange>)(C11) | troca um valor com um objeto atômico se o valor antigo for o esperado, caso contrário, lê o valor antigo
(função)
[ atomic_fetch_addatomic_fetch_add_explicit](<#/doc/atomic/atomic_fetch_add>)(C11) | adição atômica
(função)
[ atomic_fetch_subatomic_fetch_sub_explicit](<#/doc/atomic/atomic_fetch_sub>)(C11) | subtração atômica
(função)
[ atomic_fetch_oratomic_fetch_or_explicit](<#/doc/atomic/atomic_fetch_or>)(C11) | OR bit a bit atômico
(função)
[ atomic_fetch_xoratomic_fetch_xor_explicit](<#/doc/atomic/atomic_fetch_xor>)(C11) | OR exclusivo bit a bit atômico
(função)
[ atomic_fetch_andatomic_fetch_and_explicit](<#/doc/atomic/atomic_fetch_and>)(C11) | AND bit a bit atômico
(função)

##### Tipo de flag e operações

[ atomic_flag](<#/doc/atomic/atomic_flag>)(C11) | flag booleana atômica livre de bloqueio (lock-free)
(estrutura)
[ atomic_flag_test_and_setatomic_flag_test_and_set_explicit](<#/doc/atomic/atomic_flag_test_and_set>)(C11) | define uma atomic_flag como true e retorna o valor antigo
(função)
[ atomic_flag_clearatomic_flag_clear_explicit](<#/doc/atomic/atomic_flag_clear>)(C11) | define uma atomic_flag como false
(função)

##### Inicialização

[ atomic_init](<#/doc/atomic/atomic_init>)(C11) | inicializa um objeto atômico existente
(função)
[ ATOMIC_VAR_INIT](<#/doc/atomic/ATOMIC_VAR_INIT>)(C11)(obsoleto em C17)(removido em C23) | inicializa um novo objeto atômico
(macro de função)
[ ATOMIC_FLAG_INIT](<#/doc/atomic/ATOMIC_FLAG_INIT>)(C11) | inicializa uma nova [atomic_flag](<#/doc/atomic/atomic_flag>)
(constante de macro)

##### Ordem de sincronização de memória

[ memory_order](<#/doc/atomic/memory_order>)(C11) | define restrições de ordem de memória
(enum)
[ kill_dependency](<#/doc/atomic/kill_dependency>)(C11) | quebra uma cadeia de dependência para [memory_order_consume](<#/doc/atomic/memory_order>)
(macro de função)
[ atomic_thread_fence](<#/doc/atomic/atomic_thread_fence>)(C11) | primitiva de sincronização de barreira (fence) genérica dependente da ordem de memória
(função)
[ atomic_signal_fence](<#/doc/atomic/atomic_signal_fence>)(C11) | barreira (fence) entre uma thread e um manipulador de sinal executado na mesma thread
(função)

##### Aliases de tipo de conveniência

---
Nome do typedef | Nome completo do tipo
`atomic_bool` (C11) | _Atomic _Bool(até C23)_Atomic bool(desde C23)
`atomic_char` (C11) | _Atomic char
`atomic_schar` (C11) | _Atomic signed char
`atomic_uchar` (C11) | _Atomic unsigned char
`atomic_short` (C11) | _Atomic short
`atomic_ushort` (C11) | _Atomic unsigned short
`atomic_int` (C11) | _Atomic int
`atomic_uint` (C11) | _Atomic unsigned int
`atomic_long` (C11) | _Atomic long
`atomic_ulong` (C11) | _Atomic unsigned long
`atomic_llong` (C11) | _Atomic long long
`atomic_ullong` (C11) | _Atomic unsigned long long
`atomic_char8_t` (C23) | _Atomic char8_t
`atomic_char16_t` (C11) | _Atomic char16_t
`atomic_char32_t` (C11) | _Atomic char32_t
`atomic_wchar_t` (C11) | _Atomic wchar_t
`atomic_int_least8_t` (C11) | _Atomic [int_least8_t](<#/doc/types/integer>)
`atomic_uint_least8_t` (C11) | _Atomic [uint_least8_t](<#/doc/types/integer>)
`atomic_int_least16_t` (C11) | _Atomic [int_least16_t](<#/doc/types/integer>)
`atomic_uint_least16_t` (C11) | _Atomic [uint_least16_t](<#/doc/types/integer>)
`atomic_int_least32_t` (C11) | _Atomic [int_least32_t](<#/doc/types/integer>)
`atomic_uint_least32_t` (C11) | _Atomic [uint_least32_t](<#/doc/types/integer>)
`atomic_int_least64_t` (C11) | _Atomic [int_least64_t](<#/doc/types/integer>)
`atomic_uint_least64_t` (C11) | _Atomic [uint_least64_t](<#/doc/types/integer>)
`atomic_int_fast8_t` (C11) | _Atomic [int_fast8_t](<#/doc/types/integer>)
`atomic_uint_fast8_t` (C11) | _Atomic [uint_fast8_t](<#/doc/types/integer>)
`atomic_int_fast16_t` (C11) | _Atomic [int_fast16_t](<#/doc/types/integer>)
`atomic_uint_fast16_t` (C11) | _Atomic [uint_fast16_t](<#/doc/types/integer>)
`atomic_int_fast32_t` (C11) | _Atomic [int_fast32_t](<#/doc/types/integer>)
`atomic_uint_fast32_t` (C11) | _Atomic [uint_fast32_t](<#/doc/types/integer>)
`atomic_int_fast64_t` (C11) | _Atomic [int_fast64_t](<#/doc/types/integer>)
`atomic_uint_fast64_t` (C11) | _Atomic [uint_fast64_t](<#/doc/types/integer>)
`atomic_intptr_t` (C11) | _Atomic [intptr_t](<#/doc/types/integer>)
`atomic_uintptr_t` (C11) | _Atomic [uintptr_t](<#/doc/types/integer>)
`atomic_size_t` (C11) | _Atomic [size_t](<#/doc/types/size_t>)
`atomic_ptrdiff_t` (C11) | _Atomic [ptrdiff_t](<#/doc/types/ptrdiff_t>)
`atomic_intmax_t` (C11) | _Atomic [intmax_t](<#/doc/types/integer>)
`atomic_uintmax_t` (C11) | _Atomic [uintmax_t](<#/doc/types/integer>)

### Exclusão mútua

Definido no cabeçalho `<threads.h>`
---
`mtx_t` | identificador de mutex
[ mtx_init](<#/doc/thread/mtx_init>)(C11) | cria um mutex
(função)
[ mtx_lock](<#/doc/thread/mtx_lock>)(C11) | bloqueia até que um mutex seja travado
(função)
[ mtx_timedlock](<#/doc/thread/mtx_timedlock>)(C11) | bloqueia até que um mutex seja travado ou o tempo se esgote
(função)
[ mtx_trylock](<#/doc/thread/mtx_trylock>)(C11) | trava um mutex ou retorna sem bloquear se já estiver travado
(função)
[ mtx_unlock](<#/doc/thread/mtx_unlock>)(C11) | destrava um mutex
(função)
[ mtx_destroy](<#/doc/thread/mtx_destroy>)(C11) | destrói um mutex
(função)
[ mtx_plainmtx_recursivemtx_timed](<#/doc/thread/mtx_types>)(C11)(C11)(C11) | define o tipo de um mutex
(enum)

##### Chamar uma vez

[ call_once](<#/doc/thread/ONCE_FLAG_INIT>)(C11) | chama uma função exatamente uma vez
(função)

### Variáveis de condição

Definido no cabeçalho `<threads.h>`
---
`cnd_t` | identificador de variável de condição
[ cnd_init](<#/doc/thread/cnd_init>)(C11) | cria uma variável de condição
(função)
[ cnd_signal](<#/doc/thread/cnd_signal>)(C11) | desbloqueia uma thread bloqueada em uma variável de condição
(função)
[ cnd_broadcast](<#/doc/thread/cnd_broadcast>)(C11) | desbloqueia todas as threads bloqueadas em uma variável de condição
(função)
[ cnd_wait](<#/doc/thread/cnd_wait>)(C11) | bloqueia em uma variável de condição
(função)
[ cnd_timedwait](<#/doc/thread/cnd_timedwait>)(C11) | bloqueia em uma variável de condição, com um tempo limite
(função)
[ cnd_destroy](<#/doc/thread/cnd_destroy>)(C11) | destrói uma variável de condição
(função)

### Armazenamento específico de thread

Definido no cabeçalho `<threads.h>`
---
[ thread_local](<#/doc/thread/thread_local>)(C11)(removido em C23) | macro de conveniência para o especificador de classe de armazenamento _Thread_local
(macro de palavra-chave)
`tss_t` | ponteiro de armazenamento específico de thread
[ TSS_DTOR_ITERATIONS](<#/doc/thread/TSS_DTOR_ITERATIONS>)(C11) | número máximo de vezes que os destrutores são chamados
(constante de macro)
`tss_dtor_t`(C11) | tipo de ponteiro de função void(*)(void*), usado para destrutor TSS
(typedef)
[ tss_create](<#/doc/thread/tss_create>)(C11) | cria um ponteiro de armazenamento específico de thread com um destrutor fornecido
(função)
[ tss_get](<#/doc/thread/tss_get>)(C11) | lê do armazenamento específico de thread
(função)
[ tss_set](<#/doc/thread/tss_set>)(C11) | escreve no armazenamento específico de thread
(função)
[ tss_delete](<#/doc/thread/tss_delete>)(C11) | libera os recursos mantidos por um determinado ponteiro específico de thread
(função)

### Identificadores reservados

Em futuras revisões do padrão C:

  * nomes de funções, nomes de tipos e constantes de enumeração que começam com `cnd_`, `mtx_`, `thrd_` ou `tss_`, e uma letra minúscula podem ser adicionados às declarações no cabeçalho `<threads.h>`;
  * macros que começam com `ATOMIC_` e uma letra maiúscula podem ser adicionadas às macros definidas no cabeçalho [`<stdatomic.h>`](<#/doc/thread>);
  * nomes de typedef que começam com `atomic_` ou `memory_`, e uma letra minúscula podem ser adicionados às declarações no cabeçalho [`<stdatomic.h>`](<#/doc/thread>);
  * constantes de enumeração que começam com `memory_order_` e uma letra minúscula podem ser adicionadas à definição do tipo [memory_order](<#/doc/atomic/memory_order>) no cabeçalho [`<stdatomic.h>`](<#/doc/thread>);
  * nomes de funções que começam com `atomic_` e uma letra minúscula podem ser adicionados às declarações no cabeçalho [`<stdatomic.h>`](<#/doc/thread>).

Identificadores reservados para nomes de funções são sempre potencialmente (desde C23) reservados para uso como identificadores com ligação externa, enquanto outros identificadores listados aqui são potencialmente (desde C23) reservados quando [`<stdatomic.h>`](<#/doc/thread>) é incluído.

Declarar, definir ou #undefinar tal identificador resulta em comportamento indefinido se for fornecido pelo padrão ou implementação (desde C23). Programas portáveis não devem usar esses identificadores.

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.17 Atômicos <stdatomic.h> (p: TBD)

    

  * 7.26 Threads <threads.h> (p: TBD)

    

  * 7.31.8 Atômicos <stdatomic.h> (p: TBD)

    

  * 7.31.15 Threads <threads.h> (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.17 Atômicos <stdatomic.h> (p: 200-209)

    

  * 7.26 Threads <threads.h> (p: 274-283)

    

  * 7.31.8 Atômicos <stdatomic.h> (p: 332)

    

  * 7.31.15 Threads <threads.h> (p: 333)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.17 Atômicos <stdatomic.h> (p: 273-286)

    

  * 7.26 Threads <threads.h> (p: 376-387)

    

  * 7.31.8 Atômicos <stdatomic.h> (p: 455-456)

    

  * 7.31.15 Threads <threads.h> (p: 456)

### Veja também

[Documentação C++](<#/>) para a biblioteca de suporte à concorrência
---

### Links externos

[Manual GNU GCC Libc: Mutexes ISO C](<https://www.gnu.org/software/libc/manual/html_node/ISO-C-Mutexes.html>)
---