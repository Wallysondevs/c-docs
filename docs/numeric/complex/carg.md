# cargf, carg, cargl

Definido no cabeçalho [`<complex.h>`](<#/doc/numeric/complex>)

```c
float cargf( float complex z );  // desde C99
double carg( double complex z );  // desde C99
long double cargl( long double complex z );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define carg( z )  // desde C99
```

1-3) Calcula o argumento (também chamado de ângulo de fase) de `z`, com um corte de ramo ao longo do eixo real negativo.

4) Macro genérica de tipo: se `z` tem o tipo long double [complex](<#/doc/numeric/complex/complex>), long double [imaginary](<#/doc/numeric/complex/imaginary>), ou long double, `cargl` é chamada. Se `z` tem o tipo float [complex](<#/doc/numeric/complex/complex>), float [imaginary](<#/doc/numeric/complex/imaginary>), ou float, `cargf` é chamada. Se `z` tem o tipo double [complex](<#/doc/numeric/complex/complex>), double [imaginary](<#/doc/numeric/complex/imaginary>), double, ou qualquer tipo inteiro, `carg` é chamada.

### Parâmetros

- **z** — argumento complexo

### Valor de retorno

Se nenhum erro ocorrer, retorna o ângulo de fase de `z` no intervalo [−π; π].

Erros e casos especiais são tratados como se a função fosse implementada como [atan2](<#/doc/numeric/math/atan2>)([cimag](<#/doc/numeric/complex/cimag>)(z), [creal](<#/doc/numeric/complex/creal>)(z))

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <complex.h>
    
    int main(void) 
    {
        double complex z1 = 1.0+0.0*I;
        printf("phase angle of %.1f%+.1fi is %f\n", creal(z1), cimag(z1), carg(z1));
    
        double complex z2 = 0.0+1.0*I;
        printf("phase angle of %.1f%+.1fi is %f\n", creal(z2), cimag(z2), carg(z2));
    
        double complex z3 = -1.0+0.0*I;
        printf("phase angle of %.1f%+.1fi is %f\n", creal(z3), cimag(z3), carg(z3));
    
        double complex z4 = conj(z3); // or CMPLX(-1, -0.0)
        printf("phase angle of %.1f%+.1fi (the other side of the cut) is %f\n",
                 creal(z4), cimag(z4), carg(z4));
    }
```

Saída:
```
    phase angle of 1.0+0.0i is 0.000000
    phase angle of 0.0+1.0i is 1.570796
    phase angle of -1.0+0.0i is 3.141593
    phase angle of -1.0-0.0i (the other side of the cut) is -3.141593
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.3.9.1 As funções carg (p: 196)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    

  * G.7 Matemática genérica de tipo <tgmath.h> (p: 545)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.3.9.1 As funções carg (p: 178)

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337)

    

  * G.7 Matemática genérica de tipo <tgmath.h> (p: 480)

### Veja também

[ cabscabsfcabsl](<#/doc/numeric/complex/cabs>)(C99)(C99)(C99) | calcula a magnitude de um número complexo
(função)
[ atan2atan2fatan2l](<#/doc/numeric/math/atan2>)(C99)(C99) | calcula o arco tangente, usando sinais para determinar os quadrantes
(função)
[documentação C++](<#/>) para arg