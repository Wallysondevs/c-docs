# I

Definido no cabeçalho [`<complex.h>`](<#/doc/numeric/complex>)

```c
#define I /* unspecified */  // desde C99
```

A macro `I` se expande para [_Complex_I](<#/doc/numeric/complex/Complex_I>) ou [_Imaginary_I](<#/doc/numeric/complex/Imaginary_I>). Se a implementação não suportar tipos imaginários, então a macro sempre se expande para [_Complex_I](<#/doc/numeric/complex/Complex_I>).

Um programa pode desdefinir e talvez redefinir a macro I.

### Notas

A macro não é nomeada i, que é o nome da unidade imaginária em matemática, porque o nome `i` já era usado em muitos programas C, por exemplo, como uma variável de contador de loop.

A macro I é frequentemente usada para formar números complexos, com expressões como x + y*I. Se `I` for definida como [_Complex_I](<#/doc/numeric/complex/Complex_I>), então tal expressão pode criar um valor com componente imaginário `+0.0` mesmo quando `y` for `-0.0`, o que é significativo para funções de números complexos com cortes de ramo. A macro [CMPLX](<#/doc/numeric/complex/CMPLX>) fornece uma maneira de construir um número complexo precisamente.

O GCC fornece uma extensão não-portável que permite que constantes imaginárias sejam especificadas com o sufixo `i` em literais inteiros: `1.0fi`, `1.0i` e `1.0li` são unidades imaginárias em GNU C. Uma abordagem similar faz parte do C++ padrão a partir do C++14 (`1.0if`, `1.0i` e `1.0il` são as unidades imaginárias em C++)

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <complex.h>
    
    int main(void)
    {
        printf("I = %.1f%+.1fi\n", creal(I), cimag(I));
    
        double complex z1 = I * I;     // unidade imaginária ao quadrado
        printf("I * I = %.1f%+.1fi\n", creal(z1), cimag(z1));
    
        double complex z = 1.0 + 2.0*I; // forma usual de criar um número complexo pré-C11
        printf("z = %.1f%+.1fi\n", creal(z), cimag(z));
    }
```

Saída:
```
    I = 0.0+1.0i
    I * I = -1.0+0.0i
    z = 1.0+2.0i
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

  * 7.3.1/6 I (p: 188)

  * G.6/1 I (p: 537)

  * Padrão C99 (ISO/IEC 9899:1999):

  * 7.3.1/4 I (p: 170)

  * G.6/1 I (p: 472)

### Veja também

[ _Imaginary_I](<#/doc/numeric/complex/Imaginary_I>)(C99) | a constante da unidade imaginária i
(macro constante)
[ _Complex_I](<#/doc/numeric/complex/Complex_I>)(C99) | a constante da unidade complexa i
(macro constante)
[ CMPLXCMPLXFCMPLXL](<#/doc/numeric/complex/CMPLX>)(C11)(C11)(C11) | constrói um número complexo a partir de partes real e imaginária
(macro de função)
[documentação C++](<../../../cpp/numeric/complex/operator_q__q_i.html> "cpp/numeric/complex/operator""i") para operator""i