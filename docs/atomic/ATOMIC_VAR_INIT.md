# ATOMIC_VAR_INIT

Definido no cabeçalho [`<stdatomic.h>`](<#/doc/thread>)

```c
#define ATOMIC_VAR_INIT(value) /* unspecified */  // desde C11
(obsoleto em C17)
(removido em C23)
```

Expande para uma expressão que pode ser usada para inicializar uma variável atômica do mesmo tipo que `value`.

O valor inicial de um objeto atômico com duração de armazenamento automática que não é explicitamente inicializado é indeterminado. No entanto, a inicialização padrão (zero) de variáveis estáticas e thread-local produz um valor válido.

Ao inicializar uma variável atômica, qualquer acesso concorrente, mesmo através de uma operação atômica, é uma condição de corrida (data race) (isso pode acontecer se o endereço for imediatamente passado para outra thread com uma operação [memory_order_relaxed](<#/doc/atomic/memory_order>)).

### Notas

Esta macro fazia parte do projeto inicial de rascunho para tipos atômicos C11. Ela não é necessária em C11, e é obsoleta em C17 e removida em C23.

### Relatórios de defeito

Os seguintes relatórios de defeito que alteram o comportamento foram aplicados retroativamente a padrões C publicados anteriormente.

DR | Aplicado a | Comportamento conforme publicado | Comportamento correto
[DR 485](<https://www.open-std.org/jtc1/sc22/wg14/www/docs/n2396.htm#dr_485>) | C11 | a especificação era redundante e contraditória à linguagem principal | corrigido

### Referências

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.17.2.1 A macro ATOMIC_VAR_INIT (p: 201)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.17.2.1 A macro ATOMIC_VAR_INIT (p: 274)

### Veja também

[ ATOMIC_FLAG_INIT](<#/doc/atomic/ATOMIC_FLAG_INIT>)(C11) | inicializa uma nova [atomic_flag](<#/doc/atomic/atomic_flag>)
(constante de macro)
[Documentação C++](<#/>) para ATOMIC_VAR_INIT