# csinf, csin, csinl

Definido no cabeçalho [`<complex.h>`](<#/doc/numeric/complex>)

```c
float complex csinf( float complex z );  // desde C99
double complex csin( double complex z );  // desde C99
long double complex csinl( long double complex z );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define sin( z )  // desde C99
```

1-3) Calcula o seno complexo de `z`.

4) Macro genérica de tipo: Se `z` tiver o tipo long double [complex](<#/doc/numeric/complex/complex>), `csinl` é chamada. Se `z` tiver o tipo double [complex](<#/doc/numeric/complex/complex>), `csin` é chamada, se `z` tiver o tipo float [complex](<#/doc/numeric/complex/complex>), `csinf` é chamada. Se `z` for real ou inteiro, então a macro invoca a função real correspondente (sinf, [sin](<#/doc/numeric/math/sin>), sinl). Se `z` for imaginário, então a macro invoca a versão real correspondente da função [sinh](<#/doc/numeric/math/sinh>), implementando a fórmula sin(iy) = i ∙ sinh(y), e o tipo de retorno da macro é imaginário.

### Parâmetros

- **z** — argumento complexo

### Valor de retorno

Se nenhum erro ocorrer, o seno complexo de `z`.

Erros e casos especiais são tratados como se a operação fosse implementada por -I * [csinh](<#/doc/numeric/complex/csinh>)(I*z)

### Observações

O seno é uma função inteira no plano complexo e não possui cortes de ramificação.

A definição matemática do seno é sin z = eiz
-e-iz
---
2i

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <math.h>
    #include <complex.h>
    
    int main(void)
    {
        double complex z = csin(1);  // behaves like real sine along the real line
        printf("sin(1+0i) = %f%+fi ( sin(1)=%f)\n", creal(z), cimag(z), sin(1));
    
        double complex z2 = csin(I); // behaves like sinh along the imaginary line 
        printf("sin(0+1i) = %f%+fi (sinh(1)=%f)\n", creal(z2), cimag(z2), sinh(1));
    }
```

Saída:
```
    sin(1+0i) = 0.841471+0.000000i ( sin(1)=0.841471)
    sin(0+1i) = 0.000000+1.175201i (sinh(1)=1.175201)
```

### Referências

* Padrão C17 (ISO/IEC 9899:2018):

  * 7.3.5.5 As funções csin (p: 138-139)

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 272-273)

  * G.7 Matemática genérica de tipo <tgmath.h> (p: 397)

* Padrão C11 (ISO/IEC 9899:2011):

  * 7.3.5.5 As funções csin (p: 191-192)

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

  * G.7 Matemática genérica de tipo <tgmath.h> (p: 545)

* Padrão C99 (ISO/IEC 9899:1999):

  * 7.3.5.5 As funções csin (p: 173)

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337)

  * G.7 Matemática genérica de tipo <tgmath.h> (p: 480)

### Veja também

[ ccosccosfccosl](<#/doc/numeric/complex/ccos>)(C99)(C99)(C99) | calcula o cosseno complexo
(função)
[ ctanctanfctanl](<#/doc/numeric/complex/ctan>)(C99)(C99)(C99) | calcula a tangente complexa
(função)
[ casincasinfcasinl](<#/doc/numeric/complex/casin>)(C99)(C99)(C99) | calcula o arco seno complexo
(função)
[ sinsinfsinl](<#/doc/numeric/math/sin>)(C99)(C99) | calcula o seno (\\({\small\sin{x} }\\)sin(x))
(função)
[Documentação C++](<#/>) para sin