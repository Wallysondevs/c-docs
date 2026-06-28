# cprojf, cproj, cprojl

Definido no cabeçalho [`<complex.h>`](<#/doc/numeric/complex>)

```c
float complex cprojf( float complex z );  // desde C99
double complex cproj( double complex z );  // desde C99
long double complex cprojl( long double complex z );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define cproj( z )  // desde C99
```

1-3) Calcula a projeção de `z` na esfera de Riemann.

4) Macro genérica por tipo: se `z` tiver o tipo long double [complex](<#/doc/numeric/complex/complex>), long double [imaginary](<#/doc/numeric/complex/imaginary>), ou long double, `cprojl` é chamada. Se `z` tiver o tipo float [complex](<#/doc/numeric/complex/complex>), float [imaginary](<#/doc/numeric/complex/imaginary>), ou float, `cprojf` é chamada. Se `z` tiver o tipo double [complex](<#/doc/numeric/complex/complex>), double [imaginary](<#/doc/numeric/complex/imaginary>), double, ou qualquer tipo inteiro, `cproj` é chamada.

Para a maioria dos `z`, cproj(z)==z, mas todas as infinitudes complexas, mesmo os números onde um componente é infinito e o outro é NaN, tornam-se infinito real positivo, INFINITY+0.0*I ou INFINITY-0.0*I. O sinal do componente imaginário (zero) é o sinal de [cimag](<#/doc/numeric/complex/cimag>)(z).

### Parâmetros

- **z** — argumento complexo

### Valor de retorno

A projeção de `z` na esfera de Riemann.

Esta função é totalmente especificada para todas as entradas possíveis e não está sujeita a quaisquer erros descritos em [math_errhandling](<#/doc/numeric/math/math_errhandling>)

### Observações

A função `cproj` ajuda a modelar a esfera de Riemann mapeando todas as infinitudes para uma (com ou sem o sinal do zero imaginário), e deve ser usada logo antes de qualquer operação, especialmente comparações, que possam produzir resultados espúrios para qualquer uma das outras infinitudes.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <complex.h>
    #include <math.h>
    
    int main(void)
    {
        double complex z1 = cproj(1 + 2*I);
        printf("cproj(1+2i) = %.1f%+.1fi\n", creal(z1),cimag(z1));
    
        double complex z2 = cproj(INFINITY+2.0*I);
        printf("cproj(Inf+2i) = %.1f%+.1fi\n", creal(z2),cimag(z2));
    
        double complex z3 = cproj(INFINITY-2.0*I);
        printf("cproj(Inf-2i) = %.1f%+.1fi\n", creal(z3),cimag(z3));
    }
```

Saída:
```
    cproj(1+2i) = 1.0+2.0i
    cproj(Inf+2i) = inf+0.0i
    cproj(Inf-2i) = inf-0.0i
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.3.9.5 As funções cproj (p: 198)

    

  * 7.25 Matemática genérica por tipo <tgmath.h> (p: 373-375)

    

  * G.7 Matemática genérica por tipo <tgmath.h> (p: 545)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.3.9.4 As funções cproj (p: 179)

    

  * 7.22 Matemática genérica por tipo <tgmath.h> (p: 335-337)

    

  * G.7 Matemática genérica por tipo <tgmath.h> (p: 480)

### Veja também

[Documentação C++](<#/>) para proj
---