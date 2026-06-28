# cexpf, cexp, cexpl

Definido no cabeçalho [`<complex.h>`](<#/doc/numeric/complex>)

```c
float complex cexpf( float complex z );  // desde C99
double complex cexp( double complex z );  // desde C99
long double complex cexpl( long double complex z );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define exp( z )  // desde C99
```

1-3) Calcula a exponencial complexa de base _e_ de `z`.

4) Macro genérica de tipo: Se `z` tiver o tipo long double [complex](<#/doc/numeric/complex/complex>), `cexpl` é chamada. Se `z` tiver o tipo double [complex](<#/doc/numeric/complex/complex>), `cexp` é chamada. Se `z` tiver o tipo float [complex](<#/doc/numeric/complex/complex>), `cexpf` é chamada. Se `z` for real ou inteiro, então a macro invoca a função real correspondente (expf, [exp](<#/doc/numeric/math/exp>), expl). Se `z` for imaginário, a versão correspondente com argumento complexo é chamada.

### Parâmetros

- **z** — argumento complexo

### Valor de retorno

Se nenhum erro ocorrer, _e_ elevado à potência de `z`, \\(\small e^z\\)ez
é retornado.

### Tratamento de erros e valores especiais

Os erros são reportados de forma consistente com [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Se a implementação suportar aritmética de ponto flutuante IEEE,

  * cexp([conj](<#/doc/numeric/complex/conj>)(z)) == [conj](<#/doc/numeric/complex/conj>)(cexp(z))
  * Se `z` for `±0+0i`, o resultado é `1+0i`
  * Se `z` for `x+∞i` (para qualquer x finito), o resultado é `NaN+NaNi` e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado.
  * Se `z` for `x+NaNi` (para qualquer x finito), o resultado é `NaN+NaNi` e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) pode ser levantado.
  * Se `z` for `+∞+0i`, o resultado é `+∞+0i`
  * Se `z` for `-∞+yi` (para qualquer y finito), o resultado é `+0cis(y)`
  * Se `z` for `+∞+yi` (para qualquer y finito não nulo), o resultado é `+∞cis(y)`
  * Se `z` for `-∞+∞i`, o resultado é `±0±0i` (os sinais são não especificados)
  * Se `z` for `+∞+∞i`, o resultado é `±∞+NaNi` e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado (o sinal da parte real é não especificado)
  * Se `z` for `-∞+NaNi`, o resultado é `±0±0i` (os sinais são não especificados)
  * Se `z` for `+∞+NaNi`, o resultado é `±∞+NaNi` (o sinal da parte real é não especificado)
  * Se `z` for `NaN+0i`, o resultado é `NaN+0i`
  * Se `z` for `NaN+yi` (para qualquer y não nulo), o resultado é `NaN+NaNi` e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) pode ser levantado
  * Se `z` for `NaN+NaNi`, o resultado é `NaN+NaNi`

onde \\(\small{\rm cis}(y)\\)cis(y) é \\(\small \cos(y)+{\rm i}\sin(y)\\)cos(y) + i sin(y)

### Notas

A função exponencial complexa \\(\small e^z\\)ez para \\(\small z = x + {\rm i}y\\)z = x+iy é igual a \\(\small e^x {\rm cis}(y)\\)ex cis(y), ou seja, \\(\small e^x (\cos(y)+{\rm i}\sin(y))\\)ex (cos(y) + i sin(y))

A função exponencial é uma _função inteira_ no plano complexo e não possui cortes de ramo.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <math.h>
    #include <complex.h>
    
    int main(void)
    {
        double PI = acos(-1);
        double complex z = cexp(I * PI); // Euler's formula
        printf("exp(i*pi) = %.1f%+.1fi\n", creal(z), cimag(z));
    
    }
```

Saída:
```
    exp(i*pi) = -1.0+0.0i
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.3.7.1 As funções cexp (p: 194)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    

  * G.6.3.1 As funções cexp (p: 543)

    

  * G.7 Matemática genérica de tipo <tgmath.h> (p: 545)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.3.7.1 As funções cexp (p: 176)

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337)

    

  * G.6.3.1 As funções cexp (p: 478)

    

  * G.7 Matemática genérica de tipo <tgmath.h> (p: 480)

### Veja também

[ clogclogfclogl](<#/doc/numeric/complex/clog>)(C99)(C99)(C99) | calcula o logaritmo natural complexo
(função)
[ expexpfexpl](<#/doc/numeric/math/exp>)(C99)(C99) | calcula _e_ elevado à potência dada (\\({\small e^x}\\)ex)
(função)
[documentação C++](<#/>) para exp