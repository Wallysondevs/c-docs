# asin, asinf, asinl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float asinf( float arg );  // desde C99
double asin( double arg );
long double asinl( long double arg );  // desde C99
_Decimal32 asind32( _Decimal32 arg );  // desde C23
_Decimal64 asind64( _Decimal64 arg );  // desde C23
_Decimal128 asind128( _Decimal128 arg );  // desde C23
Definido no cabeçalho ``<tgmath.h>``
#define asin( arg )  // desde C99
```

  
1-6) Calcula os valores principais do arco seno de arg.

7) Macro genérica de tipo: Se o argumento tiver o tipo long double, (3) (`asinl`) é chamada. Caso contrário, se o argumento tiver um tipo inteiro ou o tipo double, (2) (`asin`) é chamada. Caso contrário, (1) (`asinf`) é chamada. Se o argumento for complexo, a macro invoca a função complexa correspondente ([casinf](<#/doc/numeric/complex/casin>), [casin](<#/doc/numeric/complex/casin>), [casinl](<#/doc/numeric/complex/casin>)).

As funções (4-6) são declaradas se e somente se a implementação predefinir `__STDC_IEC_60559_DFP__` (ou seja, a implementação suporta números de ponto flutuante decimais).  | (desde C23)  
  
### Parâmetros

arg  |  \-  |  valor de ponto flutuante   
  
### Valor de retorno

Se nenhum erro ocorrer, o arco seno de arg (arcsin(arg)) no intervalo [-π  
---  
2  
; +π  
---  
2  
], é retornado. 

Se ocorrer um erro de domínio, um valor definido pela implementação é retornado (NaN onde suportado). 

Se ocorrer um erro de intervalo devido a underflow, o resultado correto (após arredondamento) é retornado. 

### Tratamento de erros

Os erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>). 

Ocorre um erro de domínio se arg estiver fora do intervalo `[-1.0; 1.0]`. 

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559): 

  * se o argumento for ±0, ele é retornado sem modificações; 
  * se |arg| > 1, ocorre um erro de domínio e NaN é retornado; 
  * se o argumento for NaN, NaN é retornado. 

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
        printf("asin( 1.0) = %+f, 2*asin( 1.0)=%+f\n", asin(1), 2 * asin(1));
        printf("asin(-0.5) = %+f, 6*asin(-0.5)=%+f\n", asin(-0.5), 6 * asin(-0.5));
    
        // special values
        printf("asin(0.0) = %1f, asin(-0.0)=%f\n", asin(+0.0), asin(-0.0));
    
        // error handling
        errno = 0; feclearexcept(FE_ALL_EXCEPT);
        printf("asin(1.1) = %f\n", asin(1.1));
        if (errno == EDOM)
            perror("    errno == EDOM");
        if (fetestexcept(FE_INVALID))
            puts("    FE_INVALID raised");
    }
```

Saída possível: 
```
    asin( 1.0) = +1.570796, 2*asin( 1.0)=+3.141593
    asin(-0.5) = -0.523599, 6*asin(-0.5)=-3.141593
    asin(0.0) = 0.000000, asin(-0.0)=-0.000000
    asin(1.1) = nan
        errno == EDOM: Numerical argument out of domain
        FE_INVALID raised
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.12.4.2 As funções asin (p: TBD) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: TBD) 

    

  * F.10.1.2 As funções asin (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.12.4.2 As funções asin (p: 174) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 272-273) 

    

  * F.10.1.2 As funções asin (p: 378) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.12.4.2 As funções asin (p: 238) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375) 

    

  * F.10.1.2 As funções asin (p: 518) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.12.4.2 As funções asin (p: 219) 

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337) 

    

  * F.9.1.2 As funções asin (p: 456) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.5.2.2 A função asin 

### Veja também

[ acosacosfacosl](<#/doc/numeric/math/acos>)(C99)(C99) |  calcula o arco cosseno (\\({\small\arccos{x} }\\)arccos(x))   
(função)  
[ atanatanfatanl](<#/doc/numeric/math/atan>)(C99)(C99) |  calcula o arco tangente (\\({\small\arctan{x} }\\)arctan(x))   
(função)  
[ atan2atan2fatan2l](<#/doc/numeric/math/atan2>)(C99)(C99) |  calcula o arco tangente, usando sinais para determinar os quadrantes   
(função)  
[ sinsinfsinl](<#/doc/numeric/math/sin>)(C99)(C99) |  calcula o seno (\\({\small\sin{x} }\\)sin(x))   
(função)  
[ casincasinfcasinl](<#/doc/numeric/complex/casin>)(C99)(C99)(C99) |  calcula o arco seno complexo   
(função)  
[Documentação C++](<#/>) para asin