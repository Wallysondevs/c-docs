# CMPLXF, CMPLX, CMPLXL

Definido no cabeçalho [`<complex.h>`](<#/doc/numeric/complex>)

```c
float complex CMPLXF( float real, float imag );  // desde C11
double complex CMPLX( double real, double imag );  // desde C11
long double complex CMPLXL( long double real, long double imag );  // desde C11
```

Cada uma dessas macros se expande para uma expressão que avalia para o valor do tipo complexo especificado, com a parte real tendo o valor de `real` (convertido para o tipo de argumento especificado) e a parte imaginária tendo o valor de `imag` (convertido para o tipo de argumento especificado).

As expressões são adequadas para uso como inicializadores para objetos com duração de armazenamento estática ou de thread, desde que as expressões `real` e `imag` também sejam adequadas.

### Parâmetros

- **real** — a parte real do número complexo a ser retornado
- **imag** — a parte imaginária do número complexo a ser retornado

### Valor de retorno

Um número complexo composto por `real` e `imag` como as partes real e imaginária.

### Notas

Essas macros são implementadas como se os tipos imaginários fossem suportados (mesmo que não sejam suportados de outra forma e [_Imaginary_I](<#/doc/numeric/complex/Imaginary_I>) seja de fato indefinido) e como se definidas da seguinte forma:
```c
    #define CMPLX(x, y) ((double complex)((double)(x) + _Imaginary_I * (double)(y)))
    #define CMPLXF(x, y) ((float complex)((float)(x) + _Imaginary_I * (float)(y)))
    #define CMPLXL(x, y) ((long double complex)((long double)(x) + \
                          _Imaginary_I * (long double)(y)))
```

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <complex.h>
     
    int main(void)
    {
        double complex z = CMPLX(0.0, -0.0);
        printf("z = %.1f%+.1fi\n", creal(z), cimag(z));
    }
```

Saída:
```
    z = 0.0-0.0i
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.3.9.3 As macros CMPLX (p: 197)

### Veja também

[_Imaginary_I](<#/doc/numeric/complex/Imaginary_I>)(C99) | a constante da unidade imaginária i
(macro constante)
[Documentação C++](<#/>) para complex