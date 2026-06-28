# cos, cosf, cosl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float cosf( float arg );  // desde C99
double cos( double arg );
long double cosl( long double arg );  // desde C99
_Decimal32 cosd32( _Decimal32 arg );  // desde C23
_Decimal64 cosd64( _Decimal64 arg );  // desde C23
_Decimal128 cosd128( _Decimal128 arg );  // desde C23
Definido no cabeçalho ``<tgmath.h>``
#define cos( arg )  // desde C99
```

  
1-6) Calcula o cosseno de arg (medido em radianos).

7) Macro genérica de tipo: Se o argumento tiver o tipo long double, (3) (`cosl`) é chamada. Caso contrário, se o argumento tiver um tipo inteiro ou o tipo double, (2) (`cos`) é chamada. Caso contrário, (1) (`cosf`) é chamada. Se o argumento for complexo, então a macro invoca a função complexa correspondente ([ccosf](<#/doc/numeric/complex/ccos>), [ccos](<#/doc/numeric/complex/ccos>), [ccosl](<#/doc/numeric/complex/ccos>)).

As funções (4-6) são declaradas se e somente se a implementação predefinir `__STDC_IEC_60559_DFP__` (ou seja, se a implementação suportar números de ponto flutuante decimais).  | (desde C23)  
  
### Parâmetros

arg  |  \-  |  valor de ponto flutuante representando o ângulo em radianos   
  
### Valor de retorno

Se nenhum erro ocorrer, o cosseno de arg (cos(arg)) no intervalo [-1 ; +1] é retornado. 

O resultado pode ter pouca ou nenhuma significância se a magnitude de arg for grande.  | (até C99)  
  
Se ocorrer um erro de domínio, um valor definido pela implementação é retornado (NaN onde suportado). 

Se ocorrer um erro de intervalo devido a underflow, o resultado correto (após arredondamento) é retornado. 

### Tratamento de erros

Erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>). 

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559): 

  * se o argumento for ±0, o resultado é 1.0; 
  * se o argumento for ±∞, NaN é retornado e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado; 
  * se o argumento for NaN, NaN é retornado. 

### Notas

O caso em que o argumento é infinito não é especificado como um erro de domínio em C, mas é definido como um [erro de domínio no POSIX](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/cos.html>). 

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
        printf("cos(pi/3) = %f\n", cos(pi / 3));
        printf("cos(pi/2) = %f\n", cos(pi / 2));
        printf("cos(-3*pi/4) = %f\n", cos(-3 * pi / 4));
    
        // special values
        printf("cos(+0) = %f\n", cos(0.0));
        printf("cos(-0) = %f\n", cos(-0.0));
    
        // error handling
        feclearexcept(FE_ALL_EXCEPT);
        printf("cos(INFINITY) = %f\n", cos(INFINITY));
        if (fetestexcept(FE_INVALID))
            puts("    FE_INVALID raised");
    }
```

Saída possível: 
```
    cos(pi/3) = 0.500000
    cos(pi/2) = 0.000000
    cos(-3*pi/4) = -0.707107
    cos(+0) = 1.000000
    cos(-0) = 1.000000
    cos(INFINITY) = -nan
        FE_INVALID raised
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.12.4.5 As funções cos (p: TBD) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: TBD) 

    

  * F.10.1.5 As funções cos (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.12.4.5 As funções cos (p: 174) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 272-273) 

    

  * F.10.1.5 As funções cos (p: 378) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.12.4.5 As funções cos (p: 239) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375) 

    

  * F.10.1.5 As funções cos (p: 519) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.12.4.5 As funções cos (p: 220) 

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337) 

    

  * F.9.1.5 As funções cos (p: 456) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.5.2.5 A função cos 

### Veja também

[ sinsinfsinl](<#/doc/numeric/math/sin>)(C99)(C99) |  calcula o seno (\\({\small\sin{x} }\\)sin(x))   
(função)  
[ tantanftanl](<#/doc/numeric/math/tan>)(C99)(C99) |  calcula a tangente (\\({\small\tan{x} }\\)tan(x))   
(função)  
[ acosacosfacosl](<#/doc/numeric/math/acos>)(C99)(C99) |  calcula o arco cosseno (\\({\small\arccos{x} }\\)arccos(x))   
(função)  
[ ccosccosfccosl](<#/doc/numeric/complex/ccos>)(C99)(C99)(C99) |  calcula o cosseno complexo   
(função)  
[Documentação C++](<#/>) para cos