# static_assert

Definido no cabeçalho [`<assert.h>`](<#/doc/error>)

```c
#define static_assert _Static_assert  // desde C11
(removido em C23)
```

Esta macro de conveniência se expande para a palavra-chave [`_Static_assert`](<#/doc/keyword/_Static_assert>).

### Exemplo

Execute este código
```c
    #include <assert.h>
    
    int main(void)
    {
        static_assert(2 + 2 == 4, "2+2 isn't 4");   // bem-formado
    
        static_assert(sizeof(int) < sizeof(char),   // erro em tempo de compilação
                      "este programa requer que int seja menor que char");
    }
```

### Notas

Desde C23, [`static_assert`](<#/doc/language/static_assert>) é em si uma palavra-chave, que também pode ser uma macro predefinida, então `[`<assert.h>`](<#/doc/error>)` não a fornece mais.

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.2/3 Diagnósticos <assert.h> (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.2/3 Diagnósticos <assert.h> (p: 135) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.2/3 Diagnósticos <assert.h> (p: 186) 

### Veja também

[Documentação C++](<#/>) para Asserção Estática  
---