# hypot, hypotf, hypotl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float hypotf( float x, float y );  // desde C99
double hypot( double x, double y );  // desde C99
long double hypotl( long double x, long double y );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define hypot( x, y )  // desde C99
```

  
1-3) Calcula a raiz quadrada da soma dos quadrados de x e y, sem estouro ou subfluxo indevido em estágios intermediários do cálculo.

4) Macro genérica por tipo: Se qualquer argumento tiver o tipo long double, a versão long double da função é chamada. Caso contrário, se qualquer argumento tiver um tipo inteiro ou o tipo double, a versão double da função é chamada. Caso contrário, a versão float da função é chamada.

O valor calculado por esta função é o comprimento da hipotenusa de um triângulo retângulo com lados de comprimento x e y, ou a distância do ponto (x, y) da origem (0, 0), ou a magnitude de um número complexo `x+_i_ y`. 

### Parâmetros

x  |  \-  |  valor de ponto flutuante   
y  |  \-  |  valor de ponto flutuante   
  
### Valor de retorno

Se nenhum erro ocorrer, a hipotenusa de um triângulo retângulo, \\(\scriptsize{\sqrt{x^2+y^2} }\\)√x2  
+y2  
, é retornada. 

Se ocorrer um erro de faixa devido a estouro, [+HUGE_VAL](<#/doc/numeric/math/HUGE_VAL>), `+HUGE_VALF`, ou `+HUGE_VALL` é retornado. 

Se ocorrer um erro de faixa devido a subfluxo, o resultado correto (após arredondamento) é retornado. 

### Tratamento de erros

Erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>). 

Se a implementação suporta aritmética de ponto flutuante IEEE (IEC 60559), 

  * hypot(x, y), hypot(y, x) e hypot(x, -y) são equivalentes 
  * se um dos argumentos for ±0, `hypot` é equivalente a [fabs](<#/doc/numeric/math/fabs>) chamado com o argumento não-zero 
  * se um dos argumentos for ±∞, `hypot` retorna +∞ mesmo que o outro argumento seja NaN 
  * caso contrário, se qualquer um dos argumentos for NaN, NaN é retornado. 

### Notas

Implementações geralmente garantem precisão de menos de 1 ulp ([unidades no último lugar](<https://en.wikipedia.org/wiki/Unit_in_the_last_place> "enwiki:Unit in the last place")): [GNU](<https://sourceware.org/git/?p=glibc.git;a=blob_plain;f=sysdeps/ieee754/dbl-64/e_hypot.c>), [BSD](<https://www.freebsd.org/cgi/cvsweb.cgi/src/lib/msun/src/e_hypot.c>). 

hypot(x, y) is equivalent to [cabs](<#/doc/numeric/complex/cabs>)(x + I*y). 

[POSIX especifica](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/hypot.html>) que o subfluxo pode ocorrer apenas quando ambos os argumentos são subnormais e o resultado correto também é subnormal (isso proíbe implementações ingênuas). 

hypot(INFINITY, NAN) returns +∞, but [sqrt](<#/doc/numeric/math/sqrt>)(INFINITY * INFINITY + NAN * NAN) returns NaN. 

### Exemplo

Execute este código
```c
    #include <errno.h>
    #include <fenv.h>
    #include <float.h>
    #include <math.h>
    #include <stdio.h>
    // #pragma STDC FENV_ACCESS ON
     
    int main(void)
    {
        // typical usage
        printf("(1,1) cartesian is (%f,%f) polar\n", hypot(1,1), atan2(1, 1));
     
        // special values
        printf("hypot(NAN,INFINITY) = %f\n", hypot(NAN, INFINITY));
     
        // error handling
        errno = 0;
        feclearexcept(FE_ALL_EXCEPT);
        printf("hypot(DBL_MAX,DBL_MAX) = %f\n", hypot(DBL_MAX, DBL_MAX));
        if (errno == ERANGE)
            perror("    errno == ERANGE");
        if (fetestexcept(FE_OVERFLOW))
            puts("    FE_OVERFLOW raised");
    }
```

Saída possível: 
```
    (1,1) cartesian is (1.414214,0.785398) polar
    hypot(NAN,INFINITY) = inf
    hypot(DBL_MAX,DBL_MAX) = inf
        errno == ERANGE: Numerical result out of range
        FE_OVERFLOW raised
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.12.7.3 As funções hypot (p: TBD) 

    

  * 7.25 Matemática genérica por tipo <tgmath.h> (p: TBD) 

    

  * F.10.4.3 As funções hypot (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.12.7.3 As funções hypot (p: 181) 

    

  * 7.25 Matemática genérica por tipo <tgmath.h> (p: 272-273) 

    

  * F.10.4.3 As funções hypot (p: 382) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.12.7.3 As funções hypot (p: 248) 

    

  * 7.25 Matemática genérica por tipo <tgmath.h> (p: 373-375) 

    

  * F.10.4.3 As funções hypot (p: 524) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.12.7.3 As funções hypot (p: 229) 

    

  * 7.22 Matemática genérica por tipo <tgmath.h> (p: 335-337) 

    

  * F.9.4.3 As funções hypot (p: 461) 

### Ver também

[ powpowfpowl](<#/doc/numeric/math/pow>)(C99)(C99) |  calcula um número elevado a uma dada potência (\\(\small{x^y}\\)xy)   
(função)  
[ sqrtsqrtfsqrtl](<#/doc/numeric/math/sqrt>)(C99)(C99) |  calcula a raiz quadrada (\\(\small{\sqrt{x} }\\)√x)   
(função)  
[ cbrtcbrtfcbrtl](<#/doc/numeric/math/cbrt>)(C99)(C99)(C99) |  calcula a raiz cúbica (\\(\small{\sqrt[3]{x} }\\)3√x)   
(função)  
[ cabscabsfcabsl](<#/doc/numeric/complex/cabs>)(C99)(C99)(C99) |  calcula a magnitude de um número complexo   
(função)  
[Documentação C++](<#/>) para hypot