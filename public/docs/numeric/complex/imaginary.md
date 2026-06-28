# imaginary

Definido no cabeçalho [`<complex.h>`](<#/doc/numeric/complex>)

```c
#define imaginary _Imaginary  // desde C99
```

Esta macro se expande para a palavra-chave [`_Imaginary`](<#/doc/keyword/_Imaginary>).

Esta é uma macro de conveniência que possibilita o uso de float imaginary, double imaginary e long double imaginary como uma forma alternativa de escrever os três tipos C puramente imaginários float _Imaginary, double _Imaginary e long double _Imaginary.

Assim como qualquer suporte a números puramente imaginários em C, esta macro é definida apenas se os números imaginários forem suportados.

Um compilador que define __STDC_IEC_559_COMPLEX__ não é obrigado a suportar números imaginários. POSIX recomenda verificar se a macro [_Imaginary_I](<#/doc/numeric/complex/Imaginary_I>) está definida para identificar o suporte a números imaginários. | (desde C99)
(ate C11)
Números imaginários são suportados se __STDC_IEC_559_COMPLEX__ for definido. | (desde C11)

### Notas

Programas podem indefinir e talvez redefinir a macro imaginary.

Até o momento, apenas o compilador C da Oracle é conhecido por ter implementado tipos imaginários.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <complex.h>
    
    int main(void)
    {
        double imaginary i = -2.0*I; // pure imaginary
        double f = 1.0; // pure real
        double complex z = f + i; // complex number
        printf("z = %.1f%+.1fi\n", creal(z), cimag(z));
    }
```

Saída:
```
    z = 1.0-2.0i
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.3.1/5 imaginary (p: 136)

    

  * G.6/1 imaginary (p: 391-392)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.3.1/5 imaginary (p: 188)

    

  * G.6/1 imaginary (p: 537)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.3.1/3 imaginary (p: 170)

    

  * G.6/1 imaginary (p: 472)

### Veja também

[ complex](<#/doc/numeric/complex/complex>)(C99) | macro de tipo complexo
(macro de palavra-chave)