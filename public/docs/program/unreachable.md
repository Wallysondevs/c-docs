# unreachable

Definido no cabeçalho [`<stddef.h>`](<#/doc/types>)

```c
#define unreachable() /* veja abaixo */  // desde C23
```

A macro tipo função `unreachable` expande para uma expressão void. A execução de unreachable() resulta em [comportamento indefinido](<#/doc/language/behavior>).

Uma implementação pode usar isso para otimizar ramos de código impossíveis (tipicamente, em builds otimizadas) ou para capturá-los para prevenir execução posterior (tipicamente, em builds de depuração).

### Implementação possível
```c
    // Usa extensões específicas do compilador, se possível.
    #ifdef __GNUC__ // GCC, Clang, ICC
    
    #define unreachable() (__builtin_unreachable())
    
    #elifdef _MSC_VER // MSVC
    
    #define unreachable() (__assume(false))
    
    #else
    // Mesmo que nenhuma extensão seja usada, o comportamento indefinido ainda é levantado pelo
    // corpo da função vazia e pelo atributo noreturn.
    
    // A definição externa de unreachable_impl deve ser emitida em uma TU separada
    // devido à regra para funções inline em C.
    
    [[noreturn]] inline void unreachable_impl() {}
    #define unreachable() (unreachable_impl())
    
    #endif
```

---

### Exemplo

Execute este código
```c
    #include <assert.h>
    #include <stddef.h>
    #include <stdint.h>
    #include <stdlib.h>
    
    struct Color { uint8_t r, g, b, a; };
    struct ColorSpan { struct Color* data; size_t size; };
    
    // Assume que apenas um conjunto restrito de capacidades de textura é suportado.
    struct ColorSpan allocate_texture(size_t xy)
    {
        switch (xy)
        {
        case 128: [[fallthrough]];
        case 256: [[fallthrough]];
        case 512:
        {
            /* ... */
            struct ColorSpan result = {
                .data = malloc(xy * xy * sizeof(struct Color)),
                .size = xy * xy
            };
    
            if (!result.data)
                result.size = 0;
    
            return result;
        }
        default:
            unreachable();
        }
    }
    
    int main(void)
    {
        struct ColorSpan tex = allocate_texture(128); // OK
        assert(tex.size == 128 * 128);
    
        struct ColorSpan badtex = allocate_texture(32);  // Comportamento indefinido
    
        free(badtex.data);
        free(tex.data);
    }
```

Saída possível:
```
    Segmentation fault
```

### Veja também

[Documentação C++](<#/>) para unreachable
---

### Links Externos

1. | [Documentação GCC: `__builtin_unreachable`](<https://gcc.gnu.org/onlinedocs/gcc/Other-Builtins.html#index-_005f_005fbuiltin_005funreachable>)
2. | [Documentação Clang: `__builtin_unreachable`](<https://clang.llvm.org/docs/LanguageExtensions.html#builtin-unreachable>)
3. | [Documentação MSVC: `__assume`](<https://docs.microsoft.com/en-us/cpp/intrinsics/assume>)