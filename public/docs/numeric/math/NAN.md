# NAN

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
#define NAN /*implementation defined*/  // desde C99
```

A macro `NAN` se expande para uma expressão constante do tipo float, que avalia para um valor de não é um número silencioso (QNaN). Se a implementação não suporta QNaNs, esta constante de macro não é definida.

O estilo usado para imprimir um NaN é definido pela implementação.

### Notas

Existem muitos valores NaN diferentes, diferenciados por suas cargas úteis (payloads) e seus bits de sinal. O conteúdo da carga útil (payload) e o bit de sinal do NaN gerado pela macro `NAN` são definidos pela implementação.

### Exemplo

Mostra o estilo usado para imprimir um NaN e o formato IEEE.

Execute este código
```c
    #include <inttypes.h>
    #include <math.h>
    #include <stdint.h>
    #include <stdio.h>
    #include <string.h>
    
    int main(void)
    {
        const double f = NAN;
        uint64_t fn;
        memcpy(&fn, &f, sizeof f);
        printf("NAN:   %f %" PRIx64 "\n", f, fn);
    }
```

Saída possível:
```
    NAN:   nan 7ff8000000000000
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.12/5 NAN (p: TBD)

    

  * F.10/11/13 NAN (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.12/5 NAN (p: TBD)

    

  * F.10/11/13 NAN (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.12/5 NAN (p: 232)

    

  * F.10/11/13 NAN (p: 518)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.12/5 NAN (p: 213)

    

  * F.9/11/13 NAN (p: 455)

### Veja também

[ nannanfnanl](<#/doc/numeric/math/nan.2>)(C99)(C99)(C99) | retorna um NaN (não é um número)
(função)
[ isnan](<#/doc/numeric/math/isnan>)(C99) | verifica se o número dado é NaN
(macro de função)
[documentação C++](<#/>) para NAN