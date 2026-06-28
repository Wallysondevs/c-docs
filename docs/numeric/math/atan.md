# atan, atanf, atanl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float atanf( float arg );  // desde C99
double atan( double arg );
long double atanl( long double arg );  // desde C99
_Decimal32 atand32( _Decimal32 arg );  // desde C23
_Decimal64 atand64( _Decimal64 arg );  // desde C23
_Decimal128 atand128( _Decimal128 arg );  // desde C23
Definido no cabeçalho ``<tgmath.h>``
#define atan( arg )  // desde C99
```

1-6) Calcula o valor principal do arco tangente de arg.

7) Macro de tipo genérico: Se o argumento tiver o tipo long double, (3) (`atanl`) é chamada. Caso contrário, se o argumento tiver um tipo inteiro ou o tipo double, (2) (`atan`) é chamada. Caso contrário, (1) (`atanf`) é chamada. Se o argumento for complexo, então a macro invoca a função complexa correspondente ([catanf](<#/doc/numeric/complex/catan>), [catan](<#/doc/numeric/complex/catan>), [catanl](<#/doc/numeric/complex/catan>)).

As funções (4-6) são declaradas se e somente se a implementação predefinir `__STDC_IEC_60559_DFP__` (ou seja, a implementação suporta números de ponto flutuante decimais). | (desde C23)

### Parâmetros

- **arg** — valor de ponto flutuante

### Valor de retorno

Se nenhum erro ocorrer, o arco tangente de arg (arctan(arg)) no intervalo [- π
---
2
; +π
---
2
] radianos, é retornado.

Se ocorrer um erro de faixa devido a underflow, o resultado correto (após arredondamento) é retornado.

### Tratamento de erros

Erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559):

  * se o argumento for ±0, ele é retornado sem modificações;
  * se o argumento for +∞, +π/2 é retornado;
  * se o argumento for -∞, -π/2 é retornado;
  * se o argumento for NaN, NaN é retornado.

### Notas

[POSIX especifica](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/atan.html>) que, em caso de underflow, arg é retornado sem modificações, e se isso não for suportado, um valor definido pela implementação não maior que [DBL_MIN](<#/doc/types/limits>), [FLT_MIN](<#/doc/types/limits>), e [LDBL_MIN](<#/doc/types/limits>) é retornado.

### Exemplo

Execute este código
```c
    #include <math.h>
    #include <stdio.h>
    
    int main(void)
    {
        printf("atan(1) = %f, 4*atan(1)=%f\n", atan(1), 4 * atan(1));
        // special values
        printf("atan(Inf) = %f, 2*atan(Inf) = %f\n", atan(INFINITY), 2 * atan(INFINITY));
        printf("atan(-0.0) = %+f, atan(+0.0) = %+f\n", atan(-0.0), atan(0));
    }
```

Saída:
```
    atan(1) = 0.785398, 4*atan(1)=3.141593
    atan(Inf) = 1.570796, 2*atan(Inf) = 3.141593
    atan(-0.0) = -0.000000, atan(+0.0) = +0.000000
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.12.4.3 As funções atan (p: TBD)

    

  * 7.25 Matemática de tipo genérico <tgmath.h> (p: TBD)

    

  * F.10.1.3 As funções atan (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.12.4.3 As funções atan (p: 174)

    

  * 7.25 Matemática de tipo genérico <tgmath.h> (p: 272-273)

    

  * F.10.1.3 As funções atan (p: 378)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.12.4.3 As funções atan (p: 238-239)

    

  * 7.25 Matemática de tipo genérico <tgmath.h> (p: 373-375)

    

  * F.10.1.3 As funções atan (p: 519)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.12.4.3 As funções atan (p: 219)

    

  * 7.22 Matemática de tipo genérico <tgmath.h> (p: 335-337)

    

  * F.9.1.3 As funções atan (p: 456)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.5.2.3 A função atan

### Veja também

[ atan2atan2fatan2l](<#/doc/numeric/math/atan2>)(C99)(C99) | calcula o arco tangente, usando sinais para determinar os quadrantes
(função)
[ asinasinfasinl](<#/doc/numeric/math/asin>)(C99)(C99) | calcula o arco seno (\\({\small\arcsin{x} }\\)arcsin(x))
(função)
[ acosacosfacosl](<#/doc/numeric/math/acos>)(C99)(C99) | calcula o arco cosseno (\\({\small\arccos{x} }\\)arccos(x))
(função)
[ tantanftanl](<#/doc/numeric/math/tan>)(C99)(C99) | calcula a tangente (\\({\small\tan{x} }\\)tan(x))
(função)
[ catancatanfcatanl](<#/doc/numeric/complex/catan>)(C99)(C99)(C99) | calcula o arco tangente complexo
(função)
[Documentação C++](<#/>) para atan