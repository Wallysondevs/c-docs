# acos, acosf, acosl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float acosf( float arg );  // desde C99
double acos( double arg );
long double acosl( long double arg );  // desde C99
_Decimal32 acosd32( _Decimal32 arg );  // desde C23
_Decimal64 acosd64( _Decimal64 arg );  // desde C23
_Decimal128 acosd128( _Decimal128 arg );  // desde C23
Definido no cabeçalho ``<tgmath.h>``
#define acos( arg )  // desde C99
```

1-6) Calcula o valor principal do arco cosseno de arg.

7) Macro de tipo genérico: Se o argumento tiver o tipo long double, (3) (`acosl`) é chamada. Caso contrário, se o argumento tiver um tipo inteiro ou o tipo double, (2) (`acos`) é chamada. Caso contrário, (1) (`acosf`) é chamada. Se o argumento for complexo, então a macro invoca a função complexa correspondente ([cacosf](<#/doc/numeric/complex/cacos>), [cacos](<#/doc/numeric/complex/cacos>), [cacosl](<#/doc/numeric/complex/cacos>)).

As funções (4-6) são declaradas se e somente se a implementação predefinir `__STDC_IEC_60559_DFP__` (ou seja, a implementação suporta números de ponto flutuante decimais). | (desde C23)

### Parâmetros

- **arg** — valor de ponto flutuante

### Valor de retorno

Se nenhum erro ocorrer, o arco cosseno de arg (arccos(arg)) no intervalo [0 ; π] é retornado.

Se ocorrer um erro de domínio, um valor definido pela implementação é retornado (NaN onde suportado).

Se ocorrer um erro de intervalo devido a underflow, o resultado correto (após arredondamento) é retornado.

### Tratamento de erros

Os erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Ocorre um erro de domínio se arg estiver fora do intervalo `[-1.0; 1.0]`.

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559):

  * Se o argumento for +1, o valor `+0` é retornado;
  * Se |arg| > 1, ocorre um erro de domínio e NaN é retornado;
  * Se o argumento for NaN, NaN é retornado.

### Exemplo

Execute este código
```c
    #include <errno.h>
    #include <fenv.h>
    #include <math.h>
    #include <stdio.h>
    #include <string.h>
    
    #ifndef __GNUC__
    #pragma STDC FENV_ACCESS ON
    #endif
    
    int main(void)
    {
        printf("acos(-1) = %f\n", acos(-1));
        printf("acos(0.0) = %f 2*acos(0.0) = %f\n", acos(0), 2 * acos(0));
        printf("acos(0.5) = %f 3*acos(0.5) = %f\n", acos(0.5), 3 * acos(0.5));
        printf("acos(1) = %f\n", acos(1));
    
        // error handling
        errno = 0; feclearexcept(FE_ALL_EXCEPT);
        printf("acos(1.1) = %f\n", acos(1.1));
        if (errno == EDOM)
            perror("    errno == EDOM");
        if (fetestexcept(FE_INVALID))
            puts("    FE_INVALID raised");
    }
```

Saída possível:
```
    acos(-1) = 3.141593
    acos(0.0) = 1.570796 2*acos(0.0) = 3.141593
    acos(0.5) = 1.047198 3*acos(0.5) = 3.141593
    acos(1) = 0.000000
    acos(1.1) = nan
        errno == EDOM: Numerical argument out of domain
        FE_INVALID raised
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.12.4.1 As funções acos (p: TBD)

    

  * 7.25 Matemática de tipo genérico <tgmath.h> (p: TBD)

    

  * F.10.1.1 As funções acos (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.12.4.1 As funções acos (p: 173)

    

  * 7.25 Matemática de tipo genérico <tgmath.h> (p: 272-273)

    

  * F.10.1.1 As funções acos (p: 378)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.12.4.1 As funções acos (p: 238)

    

  * 7.25 Matemática de tipo genérico <tgmath.h> (p: 373-375)

    

  * F.10.1.1 As funções acos (p: 518)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.12.4.1 As funções acos (p: 218)

    

  * 7.22 Matemática de tipo genérico <tgmath.h> (p: 335-337)

    

  * F.9.1.1 As funções acos (p: 455)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.5.2.1 A função acos

### Veja também

[ asinasinfasinl](<#/doc/numeric/math/asin>)(C99)(C99) | calcula o arco seno (\\({\small\arcsin{x} }\\)arcsin(x))
(função)
[ atanatanfatanl](<#/doc/numeric/math/atan>)(C99)(C99) | calcula o arco tangente (\\({\small\arctan{x} }\\)arctan(x))
(função)
[ atan2atan2fatan2l](<#/doc/numeric/math/atan2>)(C99)(C99) | calcula o arco tangente, usando sinais para determinar os quadrantes
(função)
[ coscosfcosl](<#/doc/numeric/math/cos>)(C99)(C99) | calcula o cosseno (\\({\small\cos{x} }\\)cos(x))
(função)
[ cacoscacosfcacosl](<#/doc/numeric/complex/cacos>)(C99)(C99)(C99) | calcula o arco cosseno complexo
(função)
[Documentação C++](<#/>) para acos