# conjf, conj, conjl

Definido no cabeçalho [`<complex.h>`](<#/doc/numeric/complex>)

```c
float complex conjf( float complex z );  // desde C99
double complex conj( double complex z );  // desde C99
long double complex conjl( long double complex z );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define conj( z )  // desde C99
```

1-3) Calcula o [conjugado complexo](<https://en.wikipedia.org/wiki/Complex_conjugate> "enwiki:Complex conjugate") de `z` invertendo o sinal da parte imaginária.

4) Macro genérica de tipo: se `z` tiver o tipo long double [complex](<#/doc/numeric/complex/complex>), long double [imaginary](<#/doc/numeric/complex/imaginary>), ou long double, `conjl` é chamada. Se `z` tiver o tipo float [complex](<#/doc/numeric/complex/complex>), float [imaginary](<#/doc/numeric/complex/imaginary>), ou float, `conjf` é chamada. Se `z` tiver o tipo double [complex](<#/doc/numeric/complex/complex>), double [imaginary](<#/doc/numeric/complex/imaginary>), double, ou qualquer tipo inteiro, `conj` é chamada.

### Parâmetros

- **z** — argumento complexo

### Valor de retorno

O conjugado complexo de `z`.

### Notas

Em implementações C99 que não implementam I como [_Imaginary_I](<#/doc/numeric/complex/Imaginary_I>), `conj` pode ser usada para obter números complexos com parte imaginária zero negativa. Em C11, a macro [CMPLX](<#/doc/numeric/complex/CMPLX>) é usada para esse propósito.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <complex.h>
    
    int main(void)
    {
        double complex z = 1.0 + 2.0*I;
        double complex z2 = conj(z);
        printf("The conjugate of %.1f%+.1fi is %.1f%+.1fi\n",
                creal(z), cimag(z), creal(z2), cimag(z2));
    
        printf("Their product is %.1f%+.1fi\n", creal(z*z2), cimag(z*z2));
    }
```

Saída:
```
    The conjugate of 1.0+2.0i is 1.0-2.0i
    Their product is 5.0+0.0i
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.3.9.4 As funções conj (p: 198)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    

  * G.7 Matemática genérica de tipo <tgmath.h> (p: 545)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.3.9.3 As funções conj (p: 179)

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337)

    

  * G.7 Matemática genérica de tipo <tgmath.h> (p: 480)

### Veja também

[Documentação C++](<#/>) para conj
---