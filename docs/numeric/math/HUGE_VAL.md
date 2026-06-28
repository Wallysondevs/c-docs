# HUGE_VALF, HUGE_VAL, HUGE_VALL

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
#define HUGE_VALF /*definido pela implementação*/  // desde C99
#define HUGE_VAL /*definido pela implementação*/
#define HUGE_VALL /*definido pela implementação*/  // desde C99
```

As macros `HUGE_VALF`, `HUGE_VAL` e `HUGE_VALL` expandem-se para expressões constantes de ponto flutuante positivas que se comparam como iguais aos valores retornados por funções e operadores de ponto flutuante em caso de estouro (veja [`math_errhandling`](<#/doc/numeric/math/math_errhandling>)).

Constante | Explicação
`HUGE_VALF` | Expande-se para uma expressão float positiva que indica estouro
`HUGE_VAL` | Expande-se para uma expressão double positiva que indica estouro, não necessariamente representável como um float
`HUGE_VALL` | Expande-se para uma expressão long double positiva que indica estouro, não necessariamente representável como um float ou double

Em implementações que suportam infinitos de ponto flutuante, essas macros sempre se expandem para os infinitos positivos de float, double e long double, respectivamente.

### Exemplo

Execute este código
```
    #include <math.h>
    #include <stdio.h>
     
    int main(void)
    {
        const double result = 1.0 / 0.0;
        printf("1.0/0.0 == %f\n", result);
        if (result == HUGE_VAL)
            puts("1.0/0.0 == HUGE_VAL");
    }
```

Saída possível:
```
    1.0/0.0 == inf
    1.0/0.0 == HUGE_VAL
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.12/3 HUGE_VAL, HUGE_VALF, HUGE_VALL (p: TBD)

    

  * F.10/2 HUGE_VAL, HUGE_VALF, HUGE_VALL (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.12/3 HUGE_VAL, HUGE_VALF, HUGE_VALL (p: TBD)

    

  * F.10/2 HUGE_VAL, HUGE_VALF, HUGE_VALL (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.12/3 HUGE_VAL, HUGE_VALF, HUGE_VALL (p: 231)

    

  * F.10/2 HUGE_VAL, HUGE_VALF, HUGE_VALL (p: 517)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.12/3 HUGE_VAL, HUGE_VALF, HUGE_VALL (p: 212)

    

  * F.9/2 HUGE_VAL, HUGE_VALF, HUGE_VALL (p: 454)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.5 HUGE_VAL

### Veja também

[ INFINITY](<#/doc/numeric/math/INFINITY>)(C99) | avalia para infinito positivo ou o valor garantido para causar estouro em um float
(macro constante)
[documentação C++](<#/>) para HUGE_VAL