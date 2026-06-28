# cpowf, cpow, cpowl

Definido no cabeçalho [`<complex.h>`](<#/doc/numeric/complex>)

```c
float complex cpowf( float complex x, float complex y );  // desde C99
double complex cpow( double complex x, double complex y );  // desde C99
long double complex cpowl( long double complex x, long double complex y );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define pow( x, y )  // desde C99
```

1-3) Calcula a função de potência complexa xy
, com o corte de ramo para o primeiro parâmetro ao longo do eixo real negativo.

4) Macro genérica de tipo: Se qualquer argumento tiver o tipo long double [complex](<#/doc/numeric/complex/complex>), `cpowl` é chamada. Se qualquer argumento tiver o tipo double [complex](<#/doc/numeric/complex/complex>), `cpow` é chamada. Se qualquer argumento tiver o tipo float [complex](<#/doc/numeric/complex/complex>), `cpowf` é chamada. Se os argumentos forem reais ou inteiros, então a macro invoca a função real correspondente (powf, [pow](<#/doc/numeric/math/pow>), powl). Se qualquer argumento for imaginário, a versão de número complexo correspondente é chamada.

### Parâmetros

- **x, y** — argumento complexo

### Valor de retorno

Se nenhum erro ocorrer, a potência complexa xy
, é retornada.

Erros e casos especiais são tratados como se a operação fosse implementada por [cexp](<#/doc/numeric/complex/cexp>)(y*[clog](<#/doc/numeric/complex/clog>)(x)), exceto que a implementação pode tratar casos especiais com mais cuidado.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <complex.h>
    
    int main(void)
    {    
        double complex z = cpow(1.0+2.0*I, 2);
        printf("(1+2i)^2 = %.1f%+.1fi\n", creal(z), cimag(z));
    
        double complex z2 = cpow(-1, 0.5);
        printf("(-1+0i)^0.5 = %.1f%+.1fi\n", creal(z2), cimag(z2));
    
        double complex z3 = cpow(conj(-1), 0.5); // outro lado do corte
        printf("(-1-0i)^0.5 = %.1f%+.1fi\n", creal(z3), cimag(z3));
    
        double complex z4 = cpow(I, I); // i^i = exp(-pi/2)
        printf("i^i = %f%+fi\n", creal(z4), cimag(z4));
    }
```

Saída:
```
    (1+2i)^2 = -3.0+4.0i
    (-1+0i)^0.5 = 0.0+1.0i
    (-1-0i)^0.5 = 0.0-1.0i
    i^i = 0.207880+0.000000i
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.3.8.2 As funções cpow (p: 195-196) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375) 

    

  * G.6.4.1 As funções cpow (p: 544) 

    

  * G.7 Matemática genérica de tipo <tgmath.h> (p: 545) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.3.8.2 As funções cpow (p: 177) 

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337) 

    

  * G.6.4.1 As funções cpow (p: 479) 

    

  * G.7 Matemática genérica de tipo <tgmath.h> (p: 480) 

### Veja também

[ csqrtcsqrtfcsqrtl](<#/doc/numeric/complex/csqrt>)(C99)(C99)(C99) | calcula a raiz quadrada complexa
(função)
[ powpowfpowl](<#/doc/numeric/math/pow>)(C99)(C99) | calcula um número elevado à potência dada (\\(\small{x^y}\\)xy)
(função)
[documentação C++](<#/>) para pow