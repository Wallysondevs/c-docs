# nullptr_t

Definido no cabeçalho [`<stddef.h>`](<#/doc/types>)

```c
typedef typeof(nullptr) nullptr_t;  // desde C23
```

`nullptr_t` é o tipo da constante de ponteiro nulo predefinida, [`nullptr`](<#/doc/language/nullptr>). É um tipo distinto que não é um tipo de ponteiro em si. Pode ser [implicitamente convertido](<#/doc/language/conversion>) para qualquer tipo de ponteiro ou `bool`, e o resultado é o valor de ponteiro nulo desse tipo ou `false`, respectivamente. Nenhum tipo além do próprio `nullptr_t` pode ser convertido ou explicitamente moldado para `nullptr_t`.

sizeof(nullptr_t) e alignof(nullptr_t) são iguais a sizeof(void*) e alignof(void*) respectivamente.

`nullptr_t` possui apenas um valor válido, ou seja, `nullptr`. A representação de objeto de `nullptr` é a mesma que a de `(void*)0`. Se uma [conversão de lvalue](<#/doc/language/conversion>) produzir um valor `nullptr_t` com uma representação de objeto diferente, o comportamento é indefinido.

### Exemplo

Demonstra que `nullptr_t` é um tipo distinto.

Execute este código
```c
    #include <stddef.h>
    #include <stdio.h>
    
    #define DETECT_NULL_POINTER_CONSTANT(e) \
        _Generic(e,                         \
            void* : puts("void*"),          \
            nullptr_t : puts("nullptr_t"),  \
            default : puts("other")         \
        )
    
    int main()
    {
        DETECT_NULL_POINTER_CONSTANT(((void*)0));
        DETECT_NULL_POINTER_CONSTANT(0);
        DETECT_NULL_POINTER_CONSTANT(nullptr);
    }
```

Saída:
```
    void*
    other
    nullptr_t
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.21.2 O tipo nullptr_t (p: 315-316) 

### Veja também

[ NULL](<#/doc/types/NULL>) | constante de ponteiro nulo definida pela implementação
(macro constante)
[Documentação C++](<#/>) para nullptr_t