# catanf, catan, catanl

Definido no cabeçalho [`<complex.h>`](<#/doc/numeric/complex>)

```c
float complex catanf( float complex z );  // desde C99
double complex catan( double complex z );  // desde C99
long double complex catanl( long double complex z );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define atan( z )  // desde C99
```

1-3) Calcula a arcotangente complexa de `z` com cortes de ramo fora do intervalo [−i,+i] ao longo do eixo imaginário.

4) Macro genérica de tipo: Se `z` tiver o tipo long double [complex](<#/doc/numeric/complex/complex>), `catanl` é chamada. Se `z` tiver o tipo double [complex](<#/doc/numeric/complex/complex>), `catan` é chamada. Se `z` tiver o tipo float [complex](<#/doc/numeric/complex/complex>), `catanf` é chamada. Se `z` for real ou inteiro, a macro invoca a função real correspondente (atanf, [atan](<#/doc/numeric/math/atan>), atanl). Se `z` for imaginário, a macro invoca a versão real correspondente da função [atanh](<#/doc/numeric/math/atanh>), implementando a fórmula atan(iy) = i atanh(y), e o tipo de retorno da macro é imaginário.

### Parâmetros

- **z** — argumento complexo

### Valor de retorno

Se nenhum erro ocorrer, a arcotangente complexa de `z` é retornada, no intervalo de uma faixa ilimitada ao longo do eixo imaginário e no intervalo [−π/2; +π/2] ao longo do eixo real.

Erros e casos especiais são tratados como se a operação fosse implementada por -I * [catanh](<#/doc/numeric/complex/catanh>)(I*z).

### Notas

A tangente inversa (ou arcotangente) é uma função multivalorada e requer um corte de ramo no plano complexo. O corte de ramo é convencionalmente colocado nos segmentos de linha (-∞i,-i) e (+i,+∞i) do eixo imaginário.

A definição matemática do valor principal da tangente inversa é atan z = -1
---
2
i [ln(1 - iz) - ln (1 + iz]

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <float.h>
    #include <complex.h>
    
    int main(void)
    {
        double complex z = catan(2*I);
        printf("catan(+0+2i) = %f%+fi\n", creal(z), cimag(z));
    
        double complex z2 = catan(-conj(2*I)); // or CMPLX(-0.0, 2)
        printf("catan(-0+2i) (the other side of the cut) = %f%+fi\n", creal(z2), cimag(z2));
    
        double complex z3 = 2*catan(2*I*DBL_MAX); // or CMPLX(0, INFINITY)
        printf("2*catan(+0+i*Inf) = %f%+fi\n", creal(z3), cimag(z3));
    }
```

Saída:
```
    catan(+0+2i) = 1.570796+0.549306i
    catan(-0+2i) (the other side of the cut) = -1.570796+0.549306i
    2*catan(+0+i*Inf) = 3.141593+0.000000i
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.3.5.3 As funções catan (p: 191)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    

  * G.7 Matemática genérica de tipo <tgmath.h> (p: 545)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.3.5.3 As funções catan (p: 173)

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337)

    

  * G.7 Matemática genérica de tipo <tgmath.h> (p: 480)

### Veja também

[ casincasinfcasinl](<#/doc/numeric/complex/casin>)(C99)(C99)(C99) | calcula o arco seno complexo
(função)
[ cacoscacosfcacosl](<#/doc/numeric/complex/cacos>)(C99)(C99)(C99) | calcula o arco cosseno complexo
(função)
[ ctanctanfctanl](<#/doc/numeric/complex/ctan>)(C99)(C99)(C99) | calcula a tangente complexa
(função)
[ atanatanfatanl](<#/doc/numeric/math/atan>)(C99)(C99) | calcula a arcotangente (\\({\small\arctan{x} }\\)arctan(x))
(função)
[Documentação C++](<#/>) para atan