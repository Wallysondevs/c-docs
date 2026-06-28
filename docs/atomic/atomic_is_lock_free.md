# atomic_is_lock_free

Definido no cabeçalho [`<stdatomic.h>`](<#/doc/thread>) | | (desde C11)

```c
`_Bool atomic_is_lock_free( const volatile A* obj );`  // desde C11
```

Determina se as operações atômicas em todos os objetos do tipo `A` (o tipo do objeto apontado por `obj`) são *lock-free*. Em qualquer execução de programa, o resultado da chamada de `atomic_is_lock_free` é o mesmo para todos os ponteiros do mesmo tipo.

Esta é uma [função genérica](<#/doc/language/generic>) definida para todos os [tipos de objeto atômico](<#/doc/language/atomic>) `A`. O argumento é um ponteiro para um tipo atômico `volatile` para aceitar endereços de objetos atômicos tanto não-`volatile` quanto [volatile](<#/doc/language/volatile>) (por exemplo, I/O mapeado em memória), e a semântica `volatile` é preservada ao aplicar esta operação a objetos atômicos `volatile`.

É não especificado se o nome de uma função genérica é uma macro ou um identificador declarado com ligação externa. Se uma definição de macro for suprimida para acessar uma função real (por exemplo, entre parênteses como (atomic_is_lock_free)(...)), ou um programa definir um identificador externo com o nome de uma função genérica, o comportamento é indefinido.

### Parâmetros

- **obj** — ponteiro para o objeto atômico a ser inspecionado

### Valor de retorno

`true` se as operações em todos os objetos do tipo `A` são *lock-free*, `false` caso contrário.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <stdatomic.h>
    
    _Atomic struct A { int a[100]; } a;
    _Atomic struct B { int x, y; } b;
    int main(void)
    {
        printf("_Atomic struct A is lock free? %s\n", 
                atomic_is_lock_free(&a) ? "true" : "false");
        printf("_Atomic struct B is lock free? %s\n", 
                atomic_is_lock_free(&b) ? "true" : "false");
    }
```

Saída possível:
```
    _Atomic struct A is lock free? false
    _Atomic struct B is lock free? true
```

### Relatórios de defeito

Os seguintes relatórios de defeito que alteram o comportamento foram aplicados retroativamente a padrões C publicados anteriormente.

DR | Aplicado a | Comportamento conforme publicado | Comportamento correto
[DR 465](<https://www.open-std.org/jtc1/sc22/wg14/www/docs/n2396.htm#dr_465>) | C11 | esta função era por objeto | esta função é por tipo

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.17.5.1 A função genérica atomic_is_lock_free (p: 205)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.17.5.1 A função genérica atomic_is_lock_free (p: 280)

### Veja também

[ ATOMIC_BOOL_LOCK_FREEATOMIC_CHAR_LOCK_FREEATOMIC_CHAR16_T_LOCK_FREEATOMIC_CHAR32_T_LOCK_FREEATOMIC_WCHAR_T_LOCK_FREEATOMIC_SHORT_LOCK_FREEATOMIC_INT_LOCK_FREEATOMIC_LONG_LOCK_FREEATOMIC_LLONG_LOCK_FREEATOMIC_POINTER_LOCK_FREE](<#/doc/atomic/ATOMIC_LOCK_FREE_consts>)(C11) | indica que o tipo atômico fornecido é *lock-free*
(constante de macro)
[Documentação C++](<#/>) para atomic_is_lock_free