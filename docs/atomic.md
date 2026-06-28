# Biblioteca de operações atômicas

Se a macro constante `__STDC_NO_ATOMICS__`(C11) for definida pelo compilador, o cabeçalho `<stdatomic.h>`, a palavra-chave _Atomic e todos os nomes listados aqui não são fornecidos.

### Tipos

Definido no cabeçalho `[`<stdatomic.h>`](<#/doc/thread>)`
---
[ memory_order](<#/doc/atomic/memory_order>)(C11) | define restrições de ordenação de memória
(enum)
[ atomic_flag](<#/doc/atomic/atomic_flag>)(C11) | flag booleana atômica lock-free
(struct)

### Macros

Definido no cabeçalho `[`<stdatomic.h>`](<#/doc/thread>)`
---
[ ATOMIC_BOOL_LOCK_FREEATOMIC_CHAR_LOCK_FREEATOMIC_CHAR16_T_LOCK_FREEATOMIC_CHAR32_T_LOCK_FREEATOMIC_WCHAR_T_LOCK_FREEATOMIC_SHORT_LOCK_FREEATOMIC_INT_LOCK_FREEATOMIC_LONG_LOCK_FREEATOMIC_LLONG_LOCK_FREEATOMIC_POINTER_LOCK_FREE](<#/doc/atomic/ATOMIC_LOCK_FREE_consts>)(C11) | indica que o tipo atômico fornecido é lock-free
(macro constante)
[ ATOMIC_FLAG_INIT](<#/doc/atomic/ATOMIC_FLAG_INIT>)(C11) | inicializa uma nova [atomic_flag](<#/doc/atomic/atomic_flag>)
(macro constante)
[ ATOMIC_VAR_INIT](<#/doc/atomic/ATOMIC_VAR_INIT>)(C11)(obsoleto em C17)(removido em C23) | inicializa um novo objeto atômico
(macro de função)
[ kill_dependency](<#/doc/atomic/kill_dependency>)(C11) | quebra uma cadeia de dependência para [memory_order_consume](<#/doc/atomic/memory_order>)
(macro de função)

### Funções

Definido no cabeçalho `[`<stdatomic.h>`](<#/doc/thread>)`
---
[ atomic_flag_test_and_setatomic_flag_test_and_set_explicit](<#/doc/atomic/atomic_flag_test_and_set>)(C11) | define uma atomic_flag como true e retorna o valor antigo
(função)
[ atomic_flag_clearatomic_flag_clear_explicit](<#/doc/atomic/atomic_flag_clear>)(C11) | define uma atomic_flag como false
(função)
[ atomic_init](<#/doc/atomic/atomic_init>)(C11) | inicializa um objeto atômico existente
(função)
[ atomic_is_lock_free](<#/doc/atomic/atomic_is_lock_free>)(C11) | indica se o objeto atômico é lock-free
(função)
[ atomic_storeatomic_store_explicit](<#/doc/atomic/atomic_store>)(C11) | armazena um valor em um objeto atômico
(função)
[ atomic_loadatomic_load_explicit](<#/doc/atomic/atomic_load>)(C11) | lê um valor de um objeto atômico
(função)
[ atomic_exchangeatomic_exchange_explicit](<#/doc/atomic/atomic_exchange>)(C11) | troca um valor com o valor de um objeto atômico
(função)
[ atomic_compare_exchange_strongatomic_compare_exchange_strong_explicitatomic_compare_exchange_weakatomic_compare_exchange_weak_explicit](<#/doc/atomic/atomic_compare_exchange>)(C11) | troca um valor com um objeto atômico se o valor antigo for o esperado, caso contrário, lê o valor antigo
(função)
[ atomic_fetch_addatomic_fetch_add_explicit](<#/doc/atomic/atomic_fetch_add>)(C11) | adição atômica
(função)
[ atomic_fetch_subatomic_fetch_sub_explicit](<#/doc/atomic/atomic_fetch_sub>)(C11) | subtração atômica
(função)
[ atomic_fetch_oratomic_fetch_or_explicit](<#/doc/atomic/atomic_fetch_or>)(C11) | OR bit a bit atômico
(função)
[ atomic_fetch_xoratomic_fetch_xor_explicit](<#/doc/atomic/atomic_fetch_xor>)(C11) | OU exclusivo bit a bit atômico
(função)
[ atomic_fetch_andatomic_fetch_and_explicit](<#/>)(C11) | AND bit a bit atômico
(função)
[ atomic_thread_fence](<#/doc/atomic/atomic_thread_fence>)(C11) | primitiva de sincronização de barreira genérica dependente da ordem de memória
(função)
[ atomic_signal_fence](<#/doc/atomic/atomic_signal_fence>)(C11) | barreira entre uma thread e um manipulador de sinal executado na mesma thread
(função)

### Tipos

A biblioteca padrão oferece typedefs de conveniência para os [tipos atômicos da linguagem principal](<#/doc/language/atomic>).

Nome do typedef | Nome completo do tipo
`atomic_bool` | _Atomic _Bool
`atomic_char` | _Atomic char
`atomic_schar` | _Atomic signed char
`atomic_uchar` | _Atomic unsigned char
`atomic_short` | _Atomic short
`atomic_ushort` | _Atomic unsigned short
`atomic_int` | _Atomic int
`atomic_uint` | _Atomic unsigned int
`atomic_long` | _Atomic long
`atomic_ulong` | _Atomic unsigned long
`atomic_llong` | _Atomic long long
`atomic_ullong` | _Atomic unsigned long long
`atomic_char8_t` (C23) | _Atomic char8_t
`atomic_char16_t` | _Atomic char16_t
`atomic_char32_t` | _Atomic char32_t
`atomic_wchar_t` | _Atomic wchar_t
`atomic_int_least8_t` | _Atomic [int_least8_t](<#/doc/types/integer>)
`atomic_uint_least8_t` | _Atomic [uint_least8_t](<#/doc/types/integer>)
`atomic_int_least16_t` | _Atomic [int_least16_t](<#/doc/types/integer>)
`atomic_uint_least16_t` | _Atomic [uint_least16_t](<#/doc/types/integer>)
`atomic_int_least32_t` | _Atomic [int_least32_t](<#/doc/types/integer>)
`atomic_uint_least32_t` | _Atomic [uint_least32_t](<#/doc/types/integer>)
`atomic_int_least64_t` | _Atomic [int_least64_t](<#/doc/types/integer>)
`atomic_uint_least64_t` | _Atomic [uint_least64_t](<#/doc/types/integer>)
`atomic_int_fast8_t` | _Atomic [int_fast8_t](<#/doc/types/integer>)
`atomic_uint_fast8_t` | _Atomic [uint_fast8_t](<#/doc/types/integer>)
`atomic_int_fast16_t` | _Atomic [int_fast16_t](<#/doc/types/integer>)
`atomic_uint_fast16_t` | _Atomic [uint_fast16_t](<#/doc/types/integer>)
`atomic_int_fast32_t` | _Atomic [int_fast32_t](<#/doc/types/integer>)
`atomic_uint_fast32_t` | _Atomic [uint_fast32_t](<#/doc/types/integer>)
`atomic_int_fast64_t` | _Atomic [int_fast64_t](<#/doc/types/integer>)
`atomic_uint_fast64_t` | _Atomic [uint_fast64_t](<#/doc/types/integer>)
`atomic_intptr_t` | _Atomic [intptr_t](<#/doc/types/integer>)
`atomic_uintptr_t` | _Atomic [uintptr_t](<#/doc/types/integer>)
`atomic_size_t` | _Atomic [size_t](<#/doc/types/size_t>)
`atomic_ptrdiff_t` | _Atomic [ptrdiff_t](<#/doc/types/ptrdiff_t>)
`atomic_intmax_t` | _Atomic [intmax_t](<#/doc/types/integer>)
`atomic_uintmax_t` | _Atomic [uintmax_t](<#/doc/types/integer>)

### Referências

* Padrão C23 (ISO/IEC 9899:2024):

  * 7.17 Atomics <stdatomic.h> (p: TBD)

  * 7.31.8 Atomics <stdatomic.h> (p: TBD)

* Padrão C17 (ISO/IEC 9899:2018):

  * 7.17 Atomics <stdatomic.h> (p: TBD)

  * 7.31.8 Atomics <stdatomic.h> (p: TBD)

* Padrão C11 (ISO/IEC 9899:2011):

  * 7.17 Atomics <stdatomic.h> (p: 273-286)

  * 7.31.8 Atomics <stdatomic.h> (p: 455-456)

### Veja também

[documentação C++](<#/>) para Biblioteca de operações atômicas
---