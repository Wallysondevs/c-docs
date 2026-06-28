# nextafter, nextafterf, nextafterl, nexttoward, nexttowardf, nexttowardl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float nextafterf( float from, float to );  // desde C99
double nextafter( double from, double to );  // desde C99
long double nextafterl( long double from, long double to );  // desde C99
float nexttowardf( float from, long double to );  // desde C99
double nexttoward( double from, long double to );  // desde C99
long double nexttowardl( long double from, long double to );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define nextafter(from, to)  // desde C99
#define nexttoward(from, to)  // desde C99
```

1-3) Primeiro, converte ambos os argumentos para o tipo da função, então retorna o próximo valor representável de `from` na direção de `to`. Se `from` for igual a `to`, `to` é retornado.

4-6) Primeiro, converte o primeiro argumento para o tipo da função, então retorna o próximo valor representável de `from` na direção de `to`. Se `from` for igual a `to`, `to` é retornado, convertido de `long double` para o tipo de retorno da função sem perda de faixa ou precisão.

7) Macro genérica de tipo: Se qualquer argumento tiver o tipo `long double`, `nextafterl` é chamada. Caso contrário, se qualquer argumento tiver tipo inteiro ou tipo `double`, `nextafter` é chamada. Caso contrário, `nextafterf` é chamada.

8) Macro genérica de tipo: Se o argumento `from` tiver o tipo `long double`, `nexttowardl` é chamada. Caso contrário, se `from` tiver tipo inteiro ou o tipo `double`, `nexttoward` é chamada. Caso contrário, `nexttowardf` é chamada.

### Parâmetros

- **from, to** — valores de ponto flutuante

### Valor de retorno

Se nenhum erro ocorrer, o próximo valor representável de `from` na direção de `to` é retornado. Se `from` for igual a `to`, então `to` é retornado, convertido para o tipo da função.

Se ocorrer um erro de faixa devido a estouro (overflow), `±[HUGE_VAL](<#/doc/numeric/math/HUGE_VAL>)`, `±HUGE_VALF`, ou `±HUGE_VALL` é retornado (com o mesmo sinal de `from`).

Se ocorrer um erro de faixa devido a subfluxo (underflow), o resultado correto é retornado.

### Tratamento de erros

Erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559),

*   se `from` for finito, mas o resultado esperado for um infinito, levanta [FE_INEXACT](<#/doc/numeric/fenv/FE_exceptions>) e [FE_OVERFLOW](<#/doc/numeric/fenv/FE_exceptions>).
*   se `from` não for igual a `to` e o resultado for subnormal ou zero, levanta [FE_INEXACT](<#/doc/numeric/fenv/FE_exceptions>) e [FE_UNDERFLOW](<#/doc/numeric/fenv/FE_exceptions>).
*   em qualquer caso, o valor retornado é independente do modo de arredondamento atual.
*   se `from` ou `to` for NaN, NaN é retornado.

### Observações

[POSIX especifica](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/nextafter.html>) que as condições de estouro e subfluxo são erros de faixa ([errno](<#/doc/error/errno>) pode ser definido).

IEC 60559 recomenda que `from` seja retornado sempre que `from == to`. Essas funções retornam `to` em vez disso, o que torna o comportamento em torno de zero consistente: `nextafter(-0.0, +0.0)` retorna +0.0 e `nextafter(+0.0, -0.0)` retorna -0.0.

`nextafter` é tipicamente implementada pela manipulação da representação IEEE ([glibc](<https://github.com/bminor/glibc/blob/master/math/s_nextafter.c>) [musl](<https://github.com/ifduyue/musl/blob/master/src/math/nextafter.c>)).

### Exemplo

Run this code
```c
    #include <fenv.h>
    #include <float.h>
    #include <math.h>
    #include <stdio.h>
    
    int main(void)
    {
        float from1 = 0, to1 = nextafterf(from1, 1);
        printf("The next representable float after %.2f is %.20g (%a)\n", from1, to1, to1);
    
        float from2 = 1, to2 = nextafterf(from2, 2);
        printf("The next representable float after %.2f is %.20f (%a)\n", from2, to2, to2);
    
        double from3 = nextafter(0.1, 0), to3 = 0.1;
        printf("The number 0.1 lies between two valid doubles:\n"
               "   %.56f (%a)\nand %.55f  (%a)\n", from3, from3, to3, to3);
    
        // difference between nextafter and nexttoward:
        long double dir = nextafterl(from1, 1); // first subnormal long double
        float x = nextafterf(from1, dir); // first converts dir to float, giving 0
        printf("Using nextafter, next float after %.2f (%a) is %.20g (%a)\n",
               from1, from1, x, x);
        x = nexttowardf(from1, dir);
        printf("Using nexttoward, next float after %.2f (%a) is %.20g (%a)\n",
               from1, from1, x, x);
    
        // special values
        {
            #pragma STDC FENV_ACCESS ON
            feclearexcept(FE_ALL_EXCEPT);
            double from4 = DBL_MAX, to4 = nextafter(from4, INFINITY);
            printf("The next representable double after %.2g (%a) is %.23f (%a)\n",
                   from4, from4, to4, to4);
            if(fetestexcept(FE_OVERFLOW)) puts("   raised FE_OVERFLOW");
            if(fetestexcept(FE_INEXACT)) puts("   raised FE_INEXACT");
        } // end FENV_ACCESS block
    
        float from5 = 0.0, to5 = nextafter(from5, -0.0);
        printf("nextafter(+0.0, -0.0) gives %.2g (%a)\n", to5, to5);
    }
```

Output:
```
    The next representable float after 0.00 is 1.4012984643248170709e-45 (0x1p-149)
    The next representable float after 1.00 is 1.00000011920928955078 (0x1.000002p+0)
    The number 0.1 lies between two valid doubles:
        0.09999999999999999167332731531132594682276248931884765625 (0x1.9999999999999p-4)
    and 0.1000000000000000055511151231257827021181583404541015625  (0x1.999999999999ap-4)
    Using nextafter, next float after 0.00 (0x0p+0) is 0 (0x0p+0)
    Using nexttoward, next float after 0.00 (0x0p+0) is 1.4012984643248170709e-45 (0x1p-149)
    The next representable double after 1.8e+308 (0x1.fffffffffffffp+1023) is inf (inf)
       raised FE_OVERFLOW
       raised FE_INEXACT
    nextafter(+0.0, -0.0) gives -0 (-0x0p+0)
```

### Referências

*   Padrão C23 (ISO/IEC 9899:2024):

    *   7.12.11.3 As funções nextafter (p: TBD)

    *   7.12.11.4 As funções nexttoward (p: TBD)

    *   7.25 Matemática genérica de tipo <tgmath.h> (p: TBD)

    *   F.10.8.3 As funções nextafter (p: TBD)

    *   F.10.8.4 As funções nexttoward (p: TBD)
*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.12.11.3 As funções nextafter (p: 187)

    *   7.12.11.4 As funções nexttoward (p: 187)

    *   7.25 Matemática genérica de tipo <tgmath.h> (p: 272-273)

    *   F.10.8.3 As funções nextafter (p: 386)

    *   F.10.8.4 As funções nexttoward (p: 386)
*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.12.11.3 As funções nextafter (p: 256)

    *   7.12.11.4 As funções nexttoward (p: 257)

    *   7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    *   F.10.8.3 As funções nextafter (p: 529)

    *   F.10.8.4 As funções nexttoward (p: 529)
*   Padrão C99 (ISO/IEC 9899:1999):

    *   7.12.11.3 As funções nextafter (p: 237)

    *   7.12.11.4 As funções nexttoward (p: 238)

    *   7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337)

    *   F.9.8.3 As funções nextafter (p: 466)

    *   F.9.8.4 As funções nexttoward (p: 466)

### Veja também

[Documentação C++](<#/>) para nextafter
---