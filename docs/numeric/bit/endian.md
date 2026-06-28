# __STDC_ENDIAN_LITTLE__, __STDC_ENDIAN_BIG__, __STDC_ENDIAN_NATIVE__

Definido no cabeçalho [`<stdbit.h>`](<#/doc/numeric>)

```c
#define __STDC_ENDIAN_LITTLE__ /* implementation-defined */  // desde C23
#define __STDC_ENDIAN_BIG__ /* implementation-defined */  // desde C23
#define __STDC_ENDIAN_NATIVE__ /* implementation-defined */  // desde C23
```

Indica a [endianness](<https://en.wikipedia.org/wiki/Endianness#Overview> "enwiki:Endianness") de todos os [tipos escalares](<#/>):

*   Se todos os tipos escalares são little-endian, __STDC_ENDIAN_NATIVE__ é igual a __STDC_ENDIAN_LITTLE__.
*   Se todos os tipos escalares são big-endian, __STDC_ENDIAN_NATIVE__ é igual a __STDC_ENDIAN_BIG__.
*   Se a plataforma não usa nem little-endian nem big-endian, __STDC_ENDIAN_NATIVE__ não é igual a __STDC_ENDIAN_BIG__ nem a __STDC_ENDIAN_LITTLE__.
*   Os valores das expressões de constante inteira para __STDC_ENDIAN_BIG__ e __STDC_ENDIAN_LITTLE__ não são iguais.

### Exemplo

Execute este código
```c
    #include <stdbit.h>
    #include <stdio.h>
    
    int main()
    {
        switch(__STDC_ENDIAN_NATIVE__)
        {
            case __STDC_ENDIAN_LITTLE__:
                printf("__STDC_ENDIAN_LITTLE__\n");
                break;
            case __STDC_ENDIAN_BIG__:
                printf("__STDC_ENDIAN_BIG__\n");
                break;
            default:
                printf("mixed-endian\n");
        }
        return __STDC_ENDIAN_NATIVE__;
    }
```

Saída possível:
```
    mixed-endian
```

### Veja também

[documentação C++](<#/>) para endian
---