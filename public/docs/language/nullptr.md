# Constante de ponteiro nulo predefinida (desde C23)

### Sintaxe
  
---  
`nullptr` |  |  (desde C23)  
  
### Explicação

A palavra-chave nullptr denota uma constante de ponteiro nulo predefinida. É um [não-lvalue](<#/doc/language/value_category>) do tipo [nullptr_t](<#/doc/types/nullptr_t>). nullptr pode ser [convertido](<#/doc/language/conversion>) para tipos de ponteiro ou bool, onde o resultado é o valor de ponteiro nulo desse tipo ou false, respectivamente.

### Palavras-chave

[`nullptr`](<#/doc/keyword/nullptr>)

### Exemplo

Demonstra que uma cópia de nullptr também pode ser usada como uma constante de ponteiro nulo.

Execute este código
```
    #include <stddef.h>
    #include <stdio.h>
     
    void g(int*)
    {
        puts("Function g called");
    }
     
    #define DETECT_NULL_POINTER_CONSTANT(e) \
        _Generic(e,                         \
            void* : puts("void*"),          \
            nullptr_t : puts("nullptr_t"),  \
            default : puts("integer")       \
        )
     
    int main()
    {
        g(nullptr); // OK
        g(NULL); // OK
        g(0); // OK
     
        auto cloned_nullptr = nullptr;
        g(cloned_nullptr); // OK
     
        [[maybe_unused]] auto cloned_NULL = NULL;
    //  g(cloned_NULL); // implementation-defined: maybe OK
     
        [[maybe_unused]] auto cloned_zero = 0;
    //  g(cloned_zero); // Error
     
        DETECT_NULL_POINTER_CONSTANT(((void*)0));
        DETECT_NULL_POINTER_CONSTANT(0);
        DETECT_NULL_POINTER_CONSTANT(nullptr);
        DETECT_NULL_POINTER_CONSTANT(NULL); // implementation-defined
    }
```

Saída possível: 
```
    Function g called
    Function g called
    Function g called
    Function g called
    void*
    integer
    nullptr_t
    void*
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 6.4.4.6 Constantes predefinidas (p: 66) 

### Veja também

[ NULL](<#/doc/types/NULL>) |  constante de ponteiro nulo definida pela implementação   
(macro constante)  
[ nullptr_t](<#/doc/types/nullptr_t>)(C23) |  o tipo da constante de ponteiro nulo predefinida `nullptr`   
(typedef)  
[Documentação C++](<#/>) para nullptr