# ctanf, ctan, ctanl

Definido no cabeçalho [`<complex.h>`](<#/doc/numeric/complex>)

```c
float complex ctanf( float complex z );  // desde C99
double complex ctan( double complex z );  // desde C99
long double complex ctanl( long double complex z );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define tan( z )  // desde C99
```

1-3) Calcula a tangente complexa de `z`.

4) Macro genérica de tipo: Se `z` tiver o tipo long double [complex](<#/doc/numeric/complex/complex>), `ctanl` é chamada. Se `z` tiver o tipo double [complex](<#/doc/numeric/complex/complex>), `ctan` é chamada. Se `z` tiver o tipo float [complex](<#/doc/numeric/complex/complex>), `ctanf` é chamada. Se `z` for real ou inteiro, então a macro invoca a função real correspondente (tanf, [tan](<#/doc/numeric/math/tan>), tanl). Se `z` for imaginário, então a macro invoca a versão real correspondente da função [tanh](<#/doc/numeric/math/tanh>), implementando a fórmula tan(iy) = i tanh(y), e o tipo de retorno é imaginário.

### Parâmetros

- **z** — argumento complexo

### Valor de retorno

Se nenhum erro ocorrer, a tangente complexa de `z` é retornada.

Erros e casos especiais são tratados como se a operação fosse implementada por -i * [ctanh](<#/doc/numeric/complex/ctanh>)(i*z), onde `i` é a unidade imaginária.

### Notas

A tangente é uma função analítica no plano complexo e não possui cortes de ramo. É periódica em relação à componente real, com período πi, e possui polos de primeira ordem ao longo da linha real, nas coordenadas (π(1/2 + n), 0). No entanto, nenhuma representação de ponto flutuante comum é capaz de representar π/2 exatamente, portanto, não há valor do argumento para o qual ocorra um erro de polo.

A definição matemática da tangente é tan z = i(e-iz
-eiz
)
---
e-iz
+eiz

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <math.h>
    #include <complex.h>
    
    int main(void)
    {
        double complex z = ctan(1);  // behaves like real tangent along the real line
        printf("tan(1+0i) = %f%+fi ( tan(1)=%f)\n", creal(z), cimag(z), tan(1));
    
        double complex z2 = ctan(I); // behaves like tanh along the imaginary line 
        printf("tan(0+1i) = %f%+fi (tanh(1)=%f)\n", creal(z2), cimag(z2), tanh(1));
    }
```

Saída:
```
    tan(1+0i) = 1.557408+0.000000i ( tan(1)=1.557408)
    tan(0+1i) = 0.000000+0.761594i (tanh(1)=0.761594)
```

### Referências

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.3.5.6 As funções ctan (p: 192)

    *   7.25 Complexo genérico de tipo <tgmath.h> (p: 373-375)

    *   G.7 Matemática genérica de tipo <tgmath.h> (p: 545)
*   Padrão C99 (ISO/IEC 9899:1999):

    *   7.3.5.6 As funções ctan (p: 174)

    *   7.22 Complexo genérico de tipo <tgcomplex.h> (p: 335-337)

    *   G.7 Matemática genérica de tipo <tgmath.h> (p: 480)

### Veja também

[ ctanhctanhfctanhl](<#/doc/numeric/complex/ctanh>)(C99)(C99)(C99) | calcula a tangente hiperbólica complexa
(função)
[ csincsinfcsinl](<#/doc/numeric/complex/csin>)(C99)(C99)(C99) | calcula o seno complexo
(função)
[ ccosccosfccosl](<#/doc/numeric/complex/ccos>)(C99)(C99)(C99) | calcula o cosseno complexo
(função)
[ catancatanfcatanl](<#/doc/numeric/complex/catan>)(C99)(C99)(C99) | calcula a arcotangente complexa
(função)
[ tantanftanl](<#/doc/numeric/math/tan>)(C99)(C99) | calcula a tangente (\\({\small\tan{x} }\\)tan(x))
(função)
[Documentação C++](<#/>) para tan