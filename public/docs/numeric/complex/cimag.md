# cimagf, cimag, cimagl

Definido no cabeçalho [`<complex.h>`](<#/doc/numeric/complex>)

```c
float cimagf( float complex z );  // desde C99
double cimag( double complex z );  // desde C99
long double cimagl( long double complex z );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define cimag( z )  // desde C99
```

  
1-3) Retorna a parte imaginária de `z`.

4) Macro de tipo genérico: se `z` tiver o tipo long double [complex](<#/doc/numeric/complex/complex>), long double [imaginary](<#/doc/numeric/complex/imaginary>), ou long double, `cimagl` é chamada. Se `z` tiver o tipo float [complex](<#/doc/numeric/complex/complex>), float [imaginary](<#/doc/numeric/complex/imaginary>), ou float, `cimagf` é chamada. Se `z` tiver o tipo double [complex](<#/doc/numeric/complex/complex>), double [imaginary](<#/doc/numeric/complex/imaginary>), double, ou qualquer tipo inteiro, `cimag` é chamada.

### Parâmetros

z  |  \-  |  argumento complexo   
  
### Valor de retorno

A parte imaginária de `z`. 

Esta função é totalmente especificada para todas as entradas possíveis e não está sujeita a quaisquer erros descritos em [math_errhandling](<#/doc/numeric/math/math_errhandling>)

### Notas

Para qualquer variável complexa `z`, z == [creal](<#/doc/numeric/complex/creal>)(z) + I*cimag(z). 

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <complex.h>
     
    int main(void)
    {    
        double complex z = 1.0 + 2.0*I;
        printf("%f%+fi\n", creal(z), cimag(z));
    }
```

Saída: 
```
    1.000000+2.000000i
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.3.9.2 As funções cimag (p: 197) 

    

  * 7.25 Matemática de tipo genérico <tgmath.h> (p: 373-375) 

    

  * G.7 Matemática de tipo genérico <tgmath.h> (p: 545) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.3.9.2 As funções cimag (p: 178-179) 

    

  * 7.22 Matemática de tipo genérico <tgmath.h> (p: 335-337) 

    

  * G.7 Matemática de tipo genérico <tgmath.h> (p: 480) 

### Veja também

[ crealcrealfcreall](<#/doc/numeric/complex/creal>)(C99)(C99)(C99) |  calcula a parte real de um número complexo   
(função)  
[Documentação C++](<#/>) para imag