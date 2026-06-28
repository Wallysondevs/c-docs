# casinf, casin, casinl

Definido no cabeçalho [`<complex.h>`](<#/doc/numeric/complex>)

```c
float complex casinf( float complex z );  // desde C99
double complex casin( double complex z );  // desde C99
long double complex casinl( long double complex z );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define asin( z )  // desde C99
```

1-3) Calcula o arco seno complexo de `z` com cortes de ramo fora do intervalo [−1,+1] ao longo do eixo real.

4) Macro genérica de tipo: Se `z` tiver o tipo long double [complex](<#/doc/numeric/complex/complex>), `casinl` é chamada. Se `z` tiver o tipo double [complex](<#/doc/numeric/complex/complex>), `casin` é chamada. Se `z` tiver o tipo float [complex](<#/doc/numeric/complex/complex>), `casinf` é chamada. Se `z` for real ou inteiro, então a macro invoca a função real correspondente (asinf, [asin](<#/doc/numeric/math/asin>), asinl). Se `z` for imaginário, então a macro invoca a versão real correspondente da função [asinh](<#/doc/numeric/math/asinh>), implementando a fórmula \\(\small \arcsin({\rm i}y) = {\rm i}{\rm arsinh}(y)\\)arcsin(iy) = i arsinh(y), e o tipo de retorno da macro é imaginário.

### Parâmetros

- **z** — argumento complexo

### Valor de retorno

Se nenhum erro ocorrer, o arco seno complexo de `z` é retornado, no intervalo de uma faixa ilimitada ao longo do eixo imaginário e no intervalo [−π/2; +π/2] ao longo do eixo real.

Erros e casos especiais são tratados como se a operação fosse implementada por -I * [casinh](<#/doc/numeric/complex/casinh>)(I*z)

### Observações

O seno inverso (ou arco seno) é uma função multivalorada e requer um corte de ramo no plano complexo. O corte de ramo é convencionalmente colocado nos segmentos de linha (-∞,-1) e (1,∞) do eixo real.

A definição matemática do valor principal do arco seno é \\(\small \arcsin z = -{\rm i}\ln({\rm i}z+\sqrt{1-z^2})\\)arcsin z = -_i_ ln(_i_ z + √1-z2

Para qualquer z, \\(\small{ \arcsin(z) = \arccos(-z) - \frac{\pi}{2} }\\)arcsin(z) = acos(-z) - π
---

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <math.h>
    #include <complex.h>
    
    int main(void)
    {
        double complex z = casin(-2);
        printf("casin(-2+0i) = %f%+fi\n", creal(z), cimag(z));
    
        double complex z2 = casin(conj(-2)); // or CMPLX(-2, -0.0)
        printf("casin(-2-0i) (the other side of the cut) = %f%+fi\n", creal(z2), cimag(z2));
    
        // for any z, asin(z) = acos(-z) - pi/2
        double pi = acos(-1);
        double complex z3 = csin(cacos(conj(-2))-pi/2);
        printf("csin(cacos(-2-0i)-pi/2) = %f%+fi\n", creal(z3), cimag(z3));
    }
```

Saída:
```
    casin(-2+0i) = -1.570796+1.316958i
    casin(-2-0i) (the other side of the cut) = -1.570796-1.316958i
    csin(cacos(-2-0i)-pi/2) = 2.000000+0.000000i
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.3.5.2 As funções casin (p: 190)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    

  * G.7 Matemática genérica de tipo <tgmath.h> (p: 545)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.3.5.2 As funções casin (p: 172)

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337)

    

  * G.7 Matemática genérica de tipo <tgmath.h> (p: 480)

### Veja também

[ cacoscacosfcacosl](<#/doc/numeric/complex/cacos>)(C99)(C99)(C99) | calcula o arco cosseno complexo
(função)
[ catancatanfcatanl](<#/doc/numeric/complex/catan>)(C99)(C99)(C99) | calcula o arco tangente complexo
(função)
[ csincsinfcsinl](<#/doc/numeric/complex/csin>)(C99)(C99)(C99) | calcula o seno complexo
(função)
[ asinasinfasinl](<#/doc/numeric/math/asin>)(C99)(C99) | calcula o arco seno (\\({\small\arcsin{x} }\\)arcsin(x))
(função)
[Documentação C++](<#/>) para asin