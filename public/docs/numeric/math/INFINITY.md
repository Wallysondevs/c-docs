# INFINITY

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
#define INFINITY /*implementation defined*/  // desde C99
```

Se a implementação suporta infinitos de ponto flutuante, a macro `INFINITY` se expande para uma expressão constante do tipo float que avalia para infinito positivo ou não-sinalizado.

Se a implementação não suporta infinitos de ponto flutuante, a macro `INFINITY` se expande para um valor positivo que é garantido de causar um estouro (overflow) em um float em tempo de compilação, e o uso desta macro gera um aviso do compilador.

O estilo usado para imprimir um infinito é definido pela implementação.

### Exemplo

Mostra o estilo usado para imprimir um infinito e o formato IEEE.

Execute este código
```c
    #include <stdio.h>
    #include <math.h>
    #include <stdint.h>
    #include <inttypes.h>
    #include <string.h>
    
    int main(void)
    {
        double f = INFINITY;
        uint64_t fn; memcpy(&fn, &f, sizeof f);
        printf("INFINITY:   %f %" PRIx64 "\n", f, fn);
    }
```

Saída possível:
```
    INFINITY:   inf 7ff0000000000000
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.12/4 INFINITY (p: 231-232)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.12/4 INFINITY (p: 212-213)

### Veja também

[ isinf](<#/doc/numeric/math/isinf>)(C99) | verifica se o número dado é infinito
(macro de função)
[ HUGE_VALFHUGE_VALHUGE_VALL](<#/doc/numeric/math/HUGE_VAL>)(C99)(C99) | indica valor muito grande para ser representável (infinito) por float, double e long double, respectivamente
(macro constante)
[Documentação C++](<#/>) para INFINITY