# _Complex_I

Definido no cabeçalho [`<complex.h>`](<#/doc/numeric/complex>)

```c
#define _Complex_I /* unspecified */  // desde C99
```

A macro `_Complex_I` se expande para um valor do tipo const float _Complex com o valor da unidade imaginária.

### Notas

Esta macro pode ser usada quando `I` não está disponível, como quando foi indefinida pela aplicação.

Ao contrário de [_Imaginary_I](<#/doc/numeric/complex/Imaginary_I>) e [CMPLX](<#/doc/numeric/complex/CMPLX>), o uso desta macro para construir um número complexo pode perder o sinal de zero na parte imaginária.

### Exemplo

Execute este código
```
    #include <stdio.h>
    #include <complex.h>
    
    #undef I
    #define J _Complex_I // can be used to redefine I
    
    int main(void)
    {
        // can be used to construct a complex number
        double complex z = 1.0 + 2.0 * _Complex_I;
        printf("1.0 + 2.0 * _Complex_I = %.1f%+.1fi\n", creal(z), cimag(z));
    
        // sign of zero may not be preserved
        double complex z2 = 0.0 + -0.0 * _Complex_I;
        printf("0.0 + -0.0 * _Complex_I = %.1f%+.1fi\n", creal(z2), cimag(z2));
    }
```

Saída possível:
```
    1.0 + 2.0 * _Complex_I = 1.0+2.0i
    0.0 + -0.0 * _Complex_I = 0.0+0.0i
```

### Referências

* Padrão C23 (ISO/IEC 9899:2024):
  * 7.3.1/4 _Complex_I (p: TBD)

* Padrão C17 (ISO/IEC 9899:2018):
  * 7.3.1/4 _Complex_I (p: 136)

* Padrão C11 (ISO/IEC 9899:2011):
  * 7.3.1/4 _Complex_I (p: 188)

* Padrão C99 (ISO/IEC 9899:1999):
  * 7.3.1/2 _Complex_I (p: 170)

### Veja também

[ _Imaginary_I](<#/doc/numeric/complex/Imaginary_I>)(C99) | a constante da unidade imaginária i
(constante de macro)
[ I](<#/doc/numeric/complex/I>)(C99) | a constante da unidade complexa ou imaginária i
(constante de macro)