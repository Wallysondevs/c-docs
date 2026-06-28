# ATOMIC_*_LOCK_FREE

Definido no cabeçalho [`<stdatomic.h>`](<#/doc/thread>)

```c
#define ATOMIC_BOOL_LOCK_FREE /* implementation-defined */
#define ATOMIC_CHAR_LOCK_FREE /* implementation-defined */
#define ATOMIC_CHAR16_T_LOCK_FREE /* implementation-defined */
#define ATOMIC_CHAR32_T_LOCK_FREE /* implementation-defined */
#define ATOMIC_WCHAR_T_LOCK_FREE /* implementation-defined */
#define ATOMIC_SHORT_LOCK_FREE /* implementation-defined */
#define ATOMIC_INT_LOCK_FREE /* implementation-defined */
#define ATOMIC_LONG_LOCK_FREE /* implementation-defined */
#define ATOMIC_LLONG_LOCK_FREE /* implementation-defined */
#define ATOMIC_POINTER_LOCK_FREE /* implementation-defined */  // desde C11
#define ATOMIC_CHAR8_T_LOCK_FREE /* implementation-defined */  // desde C23
```

Expande para [expressões constantes do pré-processador](<#/doc/language/constant_expression>) que avaliam para `0`, `1`, ou `2` que indicam a propriedade lock-free dos [tipos atômicos](<#/doc/thread>) correspondentes (tanto com sinal quanto sem sinal).

Valor | Explicação
`0` | O tipo atômico nunca é lock-free
`1` | O tipo atômico é às vezes lock-free
`2` | O tipo atômico é sempre lock-free

### Referências

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.17.1/3 macros atômicas lock-free (p: 200)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.17.1/3 macros atômicas lock-free (p: 273)