# ccosf, ccos, ccosl

Definido no cabeçalho [`<complex.h>`](<#/doc/numeric/complex>)

```c
float complex ccosf( float complex z );  // desde C99
double complex ccos( double complex z );  // desde C99
long double complex ccosl( long double complex z );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define cos( z )  // desde C99
```

1-3) Calcula o cosseno complexo de `z`.

4) Macro genérica de tipo: Se `z` tiver o tipo `long double complex`, `ccosl` é chamada. Se `z` tiver o tipo `double complex`, `ccos` é chamada. Se `z` tiver o tipo `float complex`, `ccosf` é chamada. Se `z` for real ou inteiro, a macro invoca a função real correspondente (cosf, [cos](<#/doc/numeric/math/cos>), cosl). Se `z` for imaginário, a macro invoca a versão real correspondente da função [cosh](<#/doc/numeric/math/cosh>), implementando a fórmula cos(iy) = cosh(y), e o tipo de retorno é real.

### Parâmetros

- **z** — argumento complexo

### Valor de retorno

Se nenhum erro ocorrer, o cosseno complexo de `z` é retornado.

Erros e casos especiais são tratados como se a operação fosse implementada por [ccosh](<#/doc/numeric/complex/ccosh>)(I*z).

### Notas

O cosseno é uma função inteira no plano complexo e não possui cortes de ramificação.

A definição matemática do cosseno é cos z = eiz
+e-iz

---
2

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <math.h>
    #include <complex.h>
    
    int main(void)
    {
        double complex z = ccos(1);  // comporta-se como o cosseno real ao longo da linha real
        printf("cos(1+0i) = %f%+fi ( cos(1)=%f)\n", creal(z), cimag(z), cos(1));
    
        double complex z2 = ccos(I); // comporta-se como o cosh real ao longo da linha imaginária
        printf("cos(0+1i) = %f%+fi (cosh(1)=%f)\n", creal(z2), cimag(z2), cosh(1));
    }
```

Saída:
```
    cos(1+0i) = 0.540302-0.000000i ( cos(1)=0.540302)
    cos(0+1i) = 1.543081-0.000000i (cosh(1)=1.543081)
```

### Referências

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.3.5.4 As funções ccos (p: 191)

    *   7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    *   G.7 Matemática genérica de tipo <tgmath.h> (p: 545)
*   Padrão C99 (ISO/IEC 9899:1999):

    *   7.3.5.4 As funções ccos (p: 173)

    *   7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337)

    *   G.7 Matemática genérica de tipo <tgmath.h> (p: 480)

### Veja também

[ csincsinfcsinl](<#/doc/numeric/complex/csin>)(C99)(C99)(C99) | calcula o seno complexo
(função)
[ ctanctanfctanl](<#/doc/numeric/complex/ctan>)(C99)(C99)(C99) | calcula a tangente complexa
(função)
[ cacoscacosfcacosl](<#/doc/numeric/complex/cacos>)(C99)(C99)(C99) | calcula o arco cosseno complexo
(função)
[ coscosfcosl](<#/doc/numeric/math/cos>)(C99)(C99) | calcula o cosseno (\\({\small\cos{x} }\\)cos(x))
(função)
[Documentação C++](<#/>) para cos