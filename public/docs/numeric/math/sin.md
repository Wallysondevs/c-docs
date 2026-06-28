# sin, sinf, sinl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float sinf( float arg );  // desde C99
double sin( double arg );
long double sinl( long double arg );  // desde C99
_Decimal32 sind32( _Decimal32 arg );  // desde C23
_Decimal64 sind64( _Decimal64 arg );  // desde C23
_Decimal128 sind128( _Decimal128 arg );  // desde C23
Definido no cabeçalho ``<tgmath.h>``
#define sin( arg )  // desde C99
```

  
1-3) Calcula o seno de arg (medido em radianos).

7) Macro genérica de tipo: Se o argumento tiver o tipo long double, (3) (`sinl`) é chamada. Caso contrário, se o argumento tiver um tipo inteiro ou o tipo double, (2) (`sin`) é chamada. Caso contrário, (1) (`sinf`) é chamada. Se o argumento for complexo, a macro invoca a função complexa correspondente ([csinl](<#/doc/numeric/complex/csin>), [csin](<#/doc/numeric/complex/csin>), [csinf](<#/doc/numeric/complex/csin>)).

As funções (4-6) são declaradas se e somente se a implementação predefinir `__STDC_IEC_60559_DFP__` (ou seja, a implementação suporta números de ponto flutuante decimais).  | (desde C23)  
  
### Parâmetros

arg  |  \-  |  valor de ponto flutuante representando um ângulo em radianos   
  
### Valor de retorno

Se nenhum erro ocorrer, o seno de arg (sin(arg)) no intervalo [-1 ; +1] é retornado.

O resultado pode ter pouca ou nenhuma significância se a magnitude de arg for grande.  | (até C99)  
  
Se ocorrer um erro de domínio, um valor definido pela implementação é retornado (NaN onde suportado).

Se ocorrer um erro de intervalo devido a underflow, o resultado correto (após arredondamento) é retornado.

### Tratamento de erros

Os erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559):

  * se o argumento for ±0, ele é retornado sem modificação;
  * se o argumento for ±∞, NaN é retornado e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado;
  * se o argumento for NaN, NaN é retornado.

### Notas

O caso em que o argumento é infinito não é especificado como um erro de domínio em C, mas é definido como um [erro de domínio em POSIX](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/sin.html>).

POSIX também especifica que, em caso de underflow, arg é retornado sem modificação, e se isso não for suportado, um valor definido pela implementação não maior que [DBL_MIN](<#/doc/types/limits>), [FLT_MIN](<#/doc/types/limits>) e [LDBL_MIN](<#/doc/types/limits>) é retornado.

### Exemplo

Execute este código
```c
    #include <errno.h>
    #include <fenv.h>
    #include <math.h>
    #include <stdio.h>
    
    #ifndef __GNUC__
    #pragma STDC FENV_ACCESS ON
    #endif
    
    int main(void)
    {
        const double pi = acos(-1);
    
        // typical usage
        printf("sin(pi/6) = %f\n", sin(pi / 6));
        printf("sin(pi/2) = %f\n", sin(pi / 2));
        printf("sin(-3*pi/4) = %f\n", sin(-3 * pi / 4));
    
        // special values
        printf("sin(+0) = %f\n", sin(0.0));
        printf("sin(-0) = %f\n", sin(-0.0));
    
        // error handling
        feclearexcept(FE_ALL_EXCEPT);
        printf("sin(INFINITY) = %f\n", sin(INFINITY));
        if (fetestexcept(FE_INVALID))
            puts("    FE_INVALID raised");
    }
```

Saída possível:
```
    sin(pi/6) = 0.500000
    sin(pi/2) = 1.000000
    sin(-3*pi/4) = -0.707107
    sin(+0) = 0.000000
    sin(-0) = -0.000000
    sin(INFINITY) = -nan
        FE_INVALID raised
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.12.4.6 As funções sin (p: TBD) 

    

  * 7.27 Matemática genérica de tipo <tgmath.h> (p: TBD) 

    

  * F.10.1.6 As funções sin (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.12.4.6 As funções sin (p: 175) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 272-273) 

    

  * F.10.1.6 As funções sin (p: 378) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.12.4.6 As funções sin (p: 239-240) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375) 

    

  * F.10.1.6 As funções sin (p: 519) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.12.4.6 As funções sin (p: 220) 

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337) 

    

  * F.9.1.6 As funções sin (p: 456) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.5.2.6 A função sin 

### Ver também

[ coscosfcosl](<#/doc/numeric/math/cos>)(C99)(C99) |  calcula o cosseno (\\({\small\cos{x} }\\)cos(x))   
(função)  
[ tantanftanl](<#/doc/numeric/math/tan>)(C99)(C99) |  calcula a tangente (\\({\small\tan{x} }\\)tan(x))   
(função)  
[ asinasinfasinl](<#/doc/numeric/math/asin>)(C99)(C99) |  calcula o arco seno (\\({\small\arcsin{x} }\\)arcsin(x))   
(função)  
[ csincsinfcsinl](<#/doc/numeric/complex/csin>)(C99)(C99)(C99) |  calcula o seno complexo   
(função)  
[Documentação C++](<#/>) para sin