# atan2, atan2f, atan2l

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float atan2f( float y, float x );  // desde C99
double atan2( double y, double x );
long double atan2l( long double y, long double x );  // desde C99
_Decimal32 atan2d32( _Decimal32 y, _Decimal32 x );  // desde C23
_Decimal64 atan2d64( _Decimal64 y, _Decimal64 x );  // desde C23
_Decimal128 atan2d128( _Decimal128 y, _Decimal128 x );  // desde C23
Definido no cabeçalho ``<tgmath.h>``
#define atan2( y, x )  // desde C99
```

  
1-6) Calcula o arco tangente de y / x usando os sinais dos argumentos para determinar o quadrante correto.

7) Macro genérica de tipo: Se qualquer argumento tiver o tipo `long double`, (3) (`atan2l`) é chamada. Caso contrário, se qualquer argumento tiver um tipo inteiro ou o tipo `double`, (2) (`atan2`) é chamada. Caso contrário, (1) (`atan2f`) é chamada.

As funções (4-6) são declaradas se e somente se a implementação predefinir `__STDC_IEC_60559_DFP__` (ou seja, se a implementação suportar números de ponto flutuante decimais).  | (desde C23)  
  
### Parâmetros

x, y  |  \-  |  valor de ponto flutuante   
  
### Valor de retorno

Se nenhum erro ocorrer, o arco tangente de y / x (arctan(y  
---  
x  
)) no intervalo [-π ; +π] radianos é retornado. 

Argumento Y

Valor de retorno

Argumento X

Se ocorrer um erro de domínio, um valor definido pela implementação é retornado. 

Se ocorrer um erro de intervalo devido a underflow, o resultado correto (após arredondamento) é retornado. 

### Tratamento de erros

Erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>). 

Erro de domínio pode ocorrer se x e y forem ambos zero. 

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559): 

  * Se x e y forem ambos zero, erro de domínio _não_ ocorre; 
  * Se x e y forem ambos zero, erro de intervalo também não ocorre; 
  * Se y for zero, erro de polo não ocorre; 
  * Se y for `±0` e x for negativo ou `-0`, `±π` é retornado; 
  * Se y for `±0` e x for positivo ou `+0`, `±0` é retornado; 
  * Se y for `±∞` e x for finito, `±π/2` é retornado; 
  * Se y for `±∞` e x for `-∞`, `±3π/4` é retornado; 
  * Se y for `±∞` e x for `+∞`, `±π/4` é retornado; 
  * Se x for `±0` e y for negativo, `-π/2` é retornado; 
  * Se x for `±0` e y for positivo, `+π/2` é retornado; 
  * Se x for `-∞` e y for finito e positivo, `+π` é retornado; 
  * Se x for `-∞` e y for finito e negativo, `-π` é retornado; 
  * Se x for `+∞` e y for finito e positivo, `+0` é retornado; 
  * Se x for `+∞` e y for finito e negativo, `-0` é retornado; 
  * Se x for NaN ou y for NaN, NaN é retornado. 

### Notas

`atan2(y, x)` é equivalente a [`carg`](<#/doc/numeric/complex/carg>)(x + I*y). 

[POSIX especifica](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/atan2.html>) que, em caso de underflow, y / x é o valor retornado, e se isso não for suportado, um valor definido pela implementação não maior que [`DBL_MIN`](<#/doc/types/limits>), [`FLT_MIN`](<#/doc/types/limits>), e [`LDBL_MIN`](<#/doc/types/limits>) é retornado. 

### Exemplo

Execute este código
```c
    #include <math.h>
    #include <stdio.h>
    
    int main(void)
    {
        // uso normal: os sinais dos dois argumentos determinam o quadrante
        // atan2(1,1) = +pi/4, Quad I
        printf("(+1,+1) cartesian is (%f,%f) polar\n", hypot( 1, 1), atan2( 1, 1));
        // atan2(1, -1) = +3pi/4, Quad II
        printf("(+1,-1) cartesian is (%f,%f) polar\n", hypot( 1,-1), atan2( 1,-1));
        // atan2(-1,-1) = -3pi/4, Quad III
        printf("(-1,-1) cartesian is (%f,%f) polar\n", hypot(-1,-1), atan2(-1,-1));
        // atan2(-1,-1) = -pi/4, Quad IV
        printf("(-1,+1) cartesian is (%f,%f) polar\n", hypot(-1, 1), atan2(-1, 1));
    
        // valores especiais
        printf("atan2(0, 0) = %f atan2(0, -0)=%f\n", atan2(0,0), atan2(0,-0.0));
        printf("atan2(7, 0) = %f atan2(7, -0)=%f\n", atan2(7,0), atan2(7,-0.0));
    }
```

Saída: 
```
    (+1,+1) cartesian is (1.414214,0.785398) polar
    (+1,-1) cartesian is (1.414214,2.356194) polar
    (-1,-1) cartesian is (1.414214,-2.356194) polar
    (-1,+1) cartesian is (1.414214,-0.785398) polar
    atan2(0, 0) = 0.000000 atan2(0, -0)=3.141593
    atan2(7, 0) = 1.570796 atan2(7, -0)=1.570796
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.12.4.4 As funções atan2 (p: TBD) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: TBD) 

    

  * F.10.1.4 As funções atan2 (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.12.4.4 As funções atan2 (p: 174) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 272-273) 

    

  * F.10.1.4 As funções atan2 (p: 378) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.12.4.4 As funções atan2 (p: 239) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375) 

    

  * F.10.1.4 As funções atan2 (p: 519) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.12.4.4 As funções atan2 (p: 219) 

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337) 

    

  * F.9.1.4 As funções atan2 (p: 456) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.5.2.4 A função atan2 

### Veja também

[ asinasinfasinl](<#/doc/numeric/math/asin>)(C99)(C99) |  calcula o arco seno (\\({\small\arcsin{x} }\\)arcsin(x))   
(função)  
[ acosacosfacosl](<#/doc/numeric/math/acos>)(C99)(C99) |  calcula o arco cosseno (\\({\small\arccos{x} }\\)arccos(x))   
(função)  
[ atanatanfatanl](<#/doc/numeric/math/atan>)(C99)(C99) |  calcula o arco tangente (\\({\small\arctan{x} }\\)arctan(x))   
(função)  
[ cargcargfcargl](<#/doc/numeric/complex/carg>)(C99)(C99)(C99) |  calcula o ângulo de fase de um número complexo   
(função)  
[Documentação C++](<#/>) para atan2