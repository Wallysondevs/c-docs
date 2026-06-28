# FE_DOWNWARD, FE_TONEAREST, FE_TOWARDZERO, FE_UPWARD

Definido no cabeçalho [`<fenv.h>`](<#/doc/numeric/fenv>)

```c
#define FE_DOWNWARD /*definido pela implementação*/  // desde C99
#define FE_TONEAREST /*definido pela implementação*/  // desde C99
#define FE_TOWARDZERO /*definido pela implementação*/  // desde C99
#define FE_UPWARD /*definido pela implementação*/  // desde C99
```

Cada uma dessas constantes de macro se expande para uma expressão constante inteira não negativa, que pode ser usada com [fesetround](<#/doc/numeric/fenv/feround>) e [fegetround](<#/doc/numeric/fenv/feround>) para indicar um dos modos de arredondamento de ponto flutuante suportados. A implementação pode definir constantes de modo de arredondamento adicionais em [`<fenv.h>`](<#/doc/numeric/fenv>), as quais devem todas começar com `FE_` seguido por pelo menos uma letra maiúscula. Cada macro é definida apenas se for suportada.

Constante | Explicação
`FE_DOWNWARD` | arredondamento em direção ao infinito negativo
`FE_TONEAREST` | arredondamento em direção ao valor representável mais próximo
`FE_TOWARDZERO` | arredondamento em direção a zero
`FE_UPWARD` | arredondamento em direção ao infinito positivo

Modos de arredondamento adicionais podem ser suportados por uma implementação.

O modo de arredondamento atual afeta o seguinte:

*   resultados de operadores aritméticos de ponto flutuante fora de expressões constantes

```c
    double x = 1;
    x / 10; // 0.09999999999999999167332731531132594682276248931884765625 ou
            // 0.1000000000000000055511151231257827021181583404541015625
```

*   resultados de [funções matemáticas](<#/doc/numeric/math>) da biblioteca padrão

```c
    sqrt(2); // 1.41421356237309492343001693370752036571502685546875 ou
             // 1.4142135623730951454746218587388284504413604736328125
```

*   conversão implícita e casts de ponto flutuante para ponto flutuante

```c
    double d = 1 + DBL_EPSILON;
    float f = d; // 1.00000000000000000000000 ou
                 // 1.00000011920928955078125
```

*   conversões de string como [strtod](<#/doc/string/byte/strtof>) ou [printf](<#/doc/io/fprintf>)

```c
    strtof("0.1", NULL); // 0.0999999940395355224609375 ou
                         // 0.100000001490116119384765625
```

*   as funções de arredondamento da biblioteca [nearbyint](<#/doc/numeric/math/nearbyint>), [rint](<#/doc/numeric/math/rint>), [lrint](<#/doc/numeric/math/rint>)

```c
    lrint(2.1); // 2 ou 3
```

O modo de arredondamento atual NÃO afeta o seguinte:

*   conversão implícita e casts de ponto flutuante para inteiro (sempre em direção a zero)
*   resultados de operadores aritméticos de ponto flutuante em expressões constantes executadas em tempo de compilação (sempre para o mais próximo)
*   as funções da biblioteca [round](<#/doc/numeric/math/round>), [lround](<#/doc/numeric/math/round>), [llround](<#/doc/numeric/math/round>), [ceil](<#/doc/numeric/math/ceil>), [floor](<#/doc/numeric/math/floor>), [trunc](<#/doc/numeric/math/trunc>)

Assim como qualquer funcionalidade do [ambiente de ponto flutuante](<#/doc/numeric/fenv>), o arredondamento é garantido apenas se `#pragma STDC FENV_ACCESS ON` estiver definido.

Compiladores que não suportam o pragma podem oferecer suas próprias maneiras de suportar o modo de arredondamento atual. Por exemplo, Clang e GCC têm a opção `-frounding-math` destinada a desabilitar otimizações que alterariam o significado do código sensível ao arredondamento.

### Exemplo

Execute este código
```c
    #include <fenv.h>
    #include <math.h>
    #include <stdio.h>
    #include <stdlib.h>
    
    // #pragma STDC FENV_ACCESS ON
    
    int main()
    {
        fesetround(FE_DOWNWARD);
        puts("rounding down: ");
        printf("           pi = %.22f\n", acosf(-1));
        printf("strtof(\"1.1\") = %.22f\n", strtof("1.1", NULL));
        printf("    rint(2.1) = %.22f\n\n", rintf(2.1));
        fesetround(FE_UPWARD);
        puts("rounding up: ");
        printf("           pi = %.22f\n", acosf(-1));
        printf("strtof(\"1.1\") = %.22f\n", strtof("1.1", NULL));
        printf("    rint(2.1) = %.22f\n", rintf(2.1));
    }
```

Saída:
```
    rounding down:
               pi = 3.1415925025939941406250
    strtof("1.1") = 1.0999999046325683593750
        rint(2.1) = 2.0000000000000000000000
    
    rounding up:
               pi = 3.1415927410125732421875
    strtof("1.1") = 1.1000000238418579101563
        rint(2.1) = 3.0000000000000000000000
```

### Referências

*   Padrão C23 (ISO/IEC 9899:2024):

    *   7.6/8 Ambiente de ponto flutuante <fenv.h> (p: TBD)

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.6/8 Ambiente de ponto flutuante <fenv.h> (p: 151)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.6/8 Ambiente de ponto flutuante <fenv.h> (p: 207)

*   Padrão C99 (ISO/IEC 9899:1999):

    *   7.6/7 Ambiente de ponto flutuante <fenv.h> (p: 188)

### Veja também

[ fegetroundfesetround](<#/doc/numeric/fenv/feround>)(C99)(C99) | obtém ou define a direção de arredondamento
(função)
[documentação C++](<#/>) para macros de arredondamento de ponto flutuante