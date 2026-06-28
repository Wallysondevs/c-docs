# atomic_init

Definido no cabeçalho [`<stdatomic.h>`](<#/doc/thread>)

```c
void atomic_init( volatile A* obj, C desired );  // desde C11
```

Inicializa o objeto atômico obj construído por padrão com o valor desired. A função não é atômica: acesso concorrente de outra thread, mesmo através de uma operação atômica, é uma condição de corrida (data race).

Esta é uma [função genérica](<#/doc/language/generic>) definida para todos os [tipos de objeto atômico](<#/doc/language/atomic>) `A`. O argumento é um ponteiro para um tipo atômico volátil para aceitar endereços de objetos atômicos não-voláteis e [voláteis](<#/doc/language/volatile>) (ex: I/O mapeado em memória), e a semântica volátil é preservada ao aplicar esta operação a objetos atômicos voláteis. `C` é o tipo não-atômico correspondente a `A`.

É não especificado se o nome de uma função genérica é uma macro ou um identificador declarado com ligação externa. Se uma definição de macro for suprimida para acessar uma função real (ex: entre parênteses como (atomic_init)(...)), ou um programa definir um identificador externo com o nome de uma função genérica, o comportamento é indefinido.

### Parâmetros

- **obj** — ponteiro para um objeto atômico a ser inicializado
- **desired** — o valor para inicializar o objeto atômico

### Valor de retorno

(nenhum)

### Notas

`atomic_init` é a única forma de inicializar objetos atômicos alocados dinamicamente. Por exemplo:
```c
    _Atomic int *p = malloc(sizeof(_Atomic int));
    atomic_init(p, 42);
```

### Referências

*   Padrão C23 (ISO/IEC 9899:2024):

    *   7.17.2.2 A função genérica atomic_init (p: TBD)

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.17.2.2 A função genérica atomic_init (p: 201)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.17.2.2 A função genérica atomic_init (p: 274-275)

### Veja também

[ ATOMIC_VAR_INIT](<#/doc/atomic/ATOMIC_VAR_INIT>)(C11)(obsoleto em C17)(removido em C23) | inicializa um novo objeto atômico
(macro de função)
[Documentação C++](<#/>) para atomic_init