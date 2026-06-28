# _Imaginary_I

Definido no cabeçalho [`<complex.h>`](<#/doc/numeric/complex>)

```c
#define _Imaginary_I /* unspecified */  // desde C99
```

A macro `_Imaginary_I` se expande para um valor do tipo `const float _Imaginary` com o valor da unidade imaginária.

Assim como qualquer suporte a números puramente imaginários em C, esta macro é definida apenas se os números imaginários forem suportados.

Um compilador que define `__STDC_IEC_559_COMPLEX__` não é obrigado a suportar números imaginários. POSIX recomenda verificar se a macro `_Imaginary_I` está definida para identificar o suporte a números imaginários. | (desde C99)
(ate C11)
Números imaginários são suportados se `__STDC_IEC_559_COMPLEX__` estiver definido. | (desde C11)

### Notas

Esta macro permite a maneira precisa de montar um número complexo a partir de suas componentes real e imaginária, por exemplo, com `(double [complex](<#/doc/numeric/complex/complex>))((double)x + _Imaginary_I * (double)y)`. Este padrão foi padronizado em C11 como a macro [CMPLX](<#/doc/numeric/complex/CMPLX>). Note que se [_Complex_I](<#/doc/numeric/complex/Complex_I>) for usado em vez disso, esta expressão pode converter zero negativo para zero positivo na posição imaginária.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <complex.h>
    #include <math.h>
    
    int main(void)
    {
        double complex z1 = 0.0 + INFINITY * _Imaginary_I;
        printf("z1 = %.1f%+.1fi\n", creal(z1), cimag(z1));
    
        double complex z2 = 0.0 + INFINITY * _Complex_I;
        printf("z2 = %.1f%+.1fi\n", creal(z2), cimag(z2));
    }
```

Output:
```
    z1 = 0.0+Infi
    z2 = NaN+Infi
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.3.1/5 _Imaginary_I (p: 188)

    

  * G.6/1 _Imaginary_I (p: 537)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.3.1/3 _Imaginary_I (p: 170)

    

  * G.6/1 _Imaginary_I (p: 472)

### Veja também

[ _Complex_I](<#/doc/numeric/complex/Complex_I>)(C99) | a constante da unidade complexa i
(macro constante)
[ I](<#/doc/numeric/complex/I>)(C99) | a constante da unidade complexa ou imaginária i
(macro constante)