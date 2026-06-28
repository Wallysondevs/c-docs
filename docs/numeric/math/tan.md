# tan, tanf, tanl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)`

```c
float tanf( float arg );  // desde C99
double tan( double arg );
long double tanl( long double arg );  // desde C99
_Decimal32 tand32( _Decimal32 arg );  // desde C23
_Decimal64 tand64( _Decimal64 arg );  // desde C23
_Decimal128 tand128( _Decimal128 arg );  // desde C23
Definido no cabeçalho `<tgmath.h>``
#define tan( arg )  // desde C99
```

  
1-6) Calcula a tangente de arg (medida em radianos).

7) Macro genérica de tipo: Se o argumento tiver o tipo long double, (3) (`tanl`) é chamada. Caso contrário, se o argumento tiver um tipo inteiro ou o tipo double, (2) (`tan`) é chamada. Caso contrário, (1) (`tanf`) é chamada. Se o argumento for complexo, a macro invoca a função complexa correspondente ([ctanf](<#/doc/numeric/complex/ctan>), [ctan](<#/doc/numeric/complex/ctan>), [ctanl](<#/doc/numeric/complex/ctan>)).

As funções (4-6) são declaradas se e somente se a implementação predefinir `__STDC_IEC_60559_DFP__` (ou seja, a implementação suporta números de ponto flutuante decimais).  | (desde C23)  
  
### Parâmetros

arg  |  \-  |  valor de ponto flutuante representando o ângulo em radianos   
  
### Valor de retorno

Se nenhum erro ocorrer, a tangente de arg (tan(arg)) é retornada. 

O resultado pode ter pouca ou nenhuma significância se a magnitude de arg for grande.  | (ate C99)  
  
Se ocorrer um erro de domínio, um valor definido pela implementação é retornado (NaN onde suportado). 

Se ocorrer um erro de intervalo devido a underflow, o resultado correto (após arredondamento) é retornado. 

### Tratamento de erros

Os erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>). 

Se a implementação suporta aritmética de ponto flutuante IEEE (IEC 60559): 

  * se o argumento for ±0, ele é retornado sem modificação; 
  * se o argumento for ±∞, NaN é retornado e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado; 
  * se o argumento for NaN, NaN é retornado. 

### Notas

O caso em que o argumento é infinito não é especificado como um erro de domínio em C, mas é definido como um [erro de domínio no POSIX](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/tan.html>). 

A função possui polos matemáticos em π(1/2 + n); no entanto, nenhuma representação comum de ponto flutuante é capaz de representar `π/2` exatamente, portanto, não há valor do argumento para o qual ocorra um erro de polo. 

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
        printf("tan(pi*1/4) = %+f\n", tan(pi * 1 / 4)); //   45 deg
        printf("tan(pi*3/4) = %+f\n", tan(pi * 3 / 4)); //  135 deg
        printf("tan(pi*5/4) = %+f\n", tan(pi * 5 / 4)); // -135 deg
        printf("tan(pi*7/4) = %+f\n", tan(pi * 7 / 4)); //  -45 deg
     
        // special values
        printf("tan(+0) = %f\n", tan(0.0));
        printf("tan(-0) = %f\n", tan(-0.0));
     
        // error handling
        feclearexcept(FE_ALL_EXCEPT);
        printf("tan(INFINITY) = %f\n", tan(INFINITY));
        if (fetestexcept(FE_INVALID))
            puts("    FE_INVALID raised");
    }
```

Saída possível: 
```
    tan(pi*1/4) = +1.000000
    tan(pi*3/4) = -1.000000
    tan(pi*5/4) = +1.000000
    tan(pi*7/4) = -1.000000
    tan(+0) = 0.000000
    tan(-0) = -0.000000
    tan(INFINITY) = -nan
        FE_INVALID raised
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.12.4.7 As funções tan (p: TBD) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: TBD) 

    

  * F.10.1.7 As funções tan (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.12.4.7 As funções tan (p: 175) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 272-273) 

    

  * F.10.1.7 As funções tan (p: 378) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.12.4.7 As funções tan (p: 240) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375) 

    

  * F.10.1.7 As funções tan (p: 519) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.12.4.7 As funções tan (p: 220) 

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337) 

    

  * F.9.1.7 As funções tan (p: 457) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.5.2.7 A função tan 

### Veja também

[ sinsinfsinl](<#/doc/numeric/math/sin>)(C99)(C99) |  calcula o seno (\\({\small\sin{x} }\\)sin(x))   
(função)  
[ coscosfcosl](<#/doc/numeric/math/cos>)(C99)(C99) |  calcula o cosseno (\\({\small\cos{x} }\\)cos(x))   
(função)  
[ atanatanfatanl](<#/doc/numeric/math/atan>)(C99)(C99) |  calcula o arco tangente (\\({\small\arctan{x} }\\)arctan(x))   
(função)  
[ ctanctanfctanl](<#/doc/numeric/complex/ctan>)(C99)(C99)(C99) |  calcula a tangente complexa   
(função)  
[Documentação C++](<#/>) para tan