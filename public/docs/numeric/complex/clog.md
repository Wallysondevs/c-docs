# clogf, clog, clogl

Definido no cabeçalho [`<complex.h>`](<#/doc/numeric/complex>)

```c
float complex clogf( float complex z );  // desde C99
double complex clog( double complex z );  // desde C99
long double complex clogl( long double complex z );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define log( z )  // desde C99
```

1-3) Calcula o logaritmo natural complexo (base-_e_) de `z` com corte de ramo ao longo do eixo real negativo.

4) Macro de tipo genérico: Se `z` tiver o tipo long double [complex](<#/doc/numeric/complex/complex>), `clogl` é chamada. Se `z` tiver o tipo double [complex](<#/doc/numeric/complex/complex>), `clog` é chamada. Se `z` tiver o tipo float [complex](<#/doc/numeric/complex/complex>), `clogf` é chamada. Se `z` for real ou inteiro, então a macro invoca a função real correspondente (logf, [log](<#/doc/numeric/math/log>), logl). Se `z` for imaginário, a versão de número complexo correspondente é chamada.

### Parâmetros

- **z** — argumento complexo

### Valor de retorno

Se nenhum erro ocorrer, o logaritmo natural complexo de `z` é retornado, no intervalo de uma faixa no intervalo [−iπ, +iπ] ao longo do eixo imaginário e matematicamente ilimitado ao longo do eixo real.

### Tratamento de erros e valores especiais

Erros são reportados de forma consistente com [math_errhandling](<#/doc/numeric/math/math_errhandling>)

Se a implementação suportar aritmética de ponto flutuante IEEE,

* A função é contínua no corte de ramo, levando em consideração o sinal da parte imaginária.
* clog([conj](<#/doc/numeric/complex/conj>)(z)) == [conj](<#/doc/numeric/complex/conj>)(clog(z))
* Se `z` for `-0+0i`, o resultado é `-∞+πi` e [FE_DIVBYZERO](<#/doc/numeric/fenv/FE_exceptions>) é levantado.
* Se `z` for `+0+0i`, o resultado é `-∞+0i` e [FE_DIVBYZERO](<#/doc/numeric/fenv/FE_exceptions>) é levantado.
* Se `z` for `x+∞i` (para qualquer x finito), o resultado é `+∞+πi/2`
* Se `z` for `x+NaNi` (para qualquer x finito), o resultado é `NaN+NaNi` e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) pode ser levantado.
* Se `z` for `-∞+yi` (para qualquer y positivo finito), o resultado é `+∞+πi`
* Se `z` for `+∞+yi` (para qualquer y positivo finito), o resultado é `+∞+0i`
* Se `z` for `-∞+∞i`, o resultado é `+∞+3πi/4`
* Se `z` for `+∞+∞i`, o resultado é `+∞+πi/4`
* Se `z` for `±∞+NaNi`, o resultado é `+∞+NaNi`
* Se `z` for `NaN+yi` (para qualquer y finito), o resultado é `NaN+NaNi` e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) pode ser levantado.
* Se `z` for `NaN+∞i`, o resultado é `+∞+NaNi`
* Se `z` for `NaN+NaNi`, o resultado é `NaN+NaNi`

### Notas

O logaritmo natural de um número complexo z com componentes de coordenadas polares (r,θ) é igual a ln r + i(θ+2nπ), com o valor principal ln r + iθ

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <math.h>
    #include <complex.h>
    
    int main(void)
    {
        double complex z = clog(I); // r = 1, θ = pi/2
        printf("2*log(i) = %.1f%+fi\n", creal(2*z), cimag(2*z));
    
        double complex z2 = clog(sqrt(2)/2 + sqrt(2)/2*I); // r = 1, θ = pi/4
        printf("4*log(sqrt(2)/2+sqrt(2)i/2) = %.1f%+fi\n", creal(4*z2), cimag(4*z2));
    
        double complex z3 = clog(-1); // r = 1, θ = pi
        printf("log(-1+0i) = %.1f%+fi\n", creal(z3), cimag(z3));
    
        double complex z4 = clog(conj(-1)); // or clog(CMPLX(-1, -0.0)) in C11
        printf("log(-1-0i) (the other side of the cut) = %.1f%+fi\n", creal(z4), cimag(z4));
    }
```

Saída:
```
    2*log(i) = 0.0+3.141593i
    4*log(sqrt(2)/2+sqrt(2)i/2) = 0.0+3.141593i
    log(-1+0i) = 0.0+3.141593i
    log(-1-0i) (the other side of the cut) = 0.0-3.141593i
```

### Referências

* Padrão C11 (ISO/IEC 9899:2011):

  * 7.3.7.2 As funções clog (p: 195)

  * 7.25 Matemática de tipo genérico <tgmath.h> (p: 373-375)

  * G.6.3.2 As funções clog (p: 543-544)

  * G.7 Matemática de tipo genérico <tgmath.h> (p: 545)

* Padrão C99 (ISO/IEC 9899:1999):

  * 7.3.7.2 As funções clog (p: 176-177)

  * 7.22 Matemática de tipo genérico <tgmath.h> (p: 335-337)

  * G.6.3.2 As funções clog (p: 478-479)

  * G.7 Matemática de tipo genérico <tgmath.h> (p: 480)

### Veja também

[ cexpcexpfcexpl](<#/doc/numeric/complex/cexp>)(C99)(C99)(C99) | calcula a exponencial complexa de base-e
(função)
[ loglogflogl](<#/doc/numeric/math/log>)(C99)(C99) | calcula o logaritmo natural (base-_e_) (\\({\small \ln{x} }\\)ln(x))
(função)
[Documentação C++](<#/>) para log
