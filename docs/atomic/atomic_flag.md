# atomic_flag

Definido no cabeçalho [`<stdatomic.h>`](<#/doc/thread>)

```c
typedef struct /* unspecified */ atomic_flag;  // desde C11
```

`atomic_flag` é um tipo booleano atômico. Diferente de outros tipos atômicos, ele é garantido como *lock-free*. Diferente de [`atomic_bool`](<#/doc/thread>), `atomic_flag` não fornece operações de carregamento (load) ou armazenamento (store).

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.17.1/5 atomic_flag (p: 293)

    

  * 7.17.8 Tipo e operações de flag atômica (p: 302-303)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.17.1/4 atomic_flag (p: 200)

    

  * 7.17.8 Tipo e operações de flag atômica (p: 208-209)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.17.1/4 atomic_flag (p: 273)

    

  * 7.17.8 Tipo e operações de flag atômica (p: 285-286)

### Veja também

[ ATOMIC_FLAG_INIT](<#/doc/atomic/ATOMIC_FLAG_INIT>)(C11) | inicializa uma nova atomic_flag
(constante de macro)
[ atomic_flag_test_and_setatomic_flag_test_and_set_explicit](<#/doc/atomic/atomic_flag_test_and_set>)(C11) | define uma atomic_flag como true e retorna o valor antigo
(função)
[ atomic_flag_clearatomic_flag_clear_explicit](<#/doc/atomic/atomic_flag_clear>)(C11) | define uma atomic_flag como false
(função)
[documentação C++](<#/>) para atomic_flag