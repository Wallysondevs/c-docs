# csqrtf, csqrt, csqrtl

Definido no cabeçalho [`<complex.h>`](<#/doc/numeric/complex>)

```c
float complex csqrtf( float complex z );  // desde C99
double complex csqrt( double complex z );  // desde C99
long double complex csqrtl( long double complex z );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define sqrt( z )  // desde C99
```

1-3) Calcula a raiz quadrada complexa de `z` com o corte de ramo ao longo do eixo real negativo.

4) Macro genérica de tipo: Se `z` tiver o tipo long double [complex](<#/doc/numeric/complex/complex>), `csqrtl` é chamada. Se `z` tiver o tipo double [complex](<#/doc/numeric/complex/complex>), `csqrt` é chamada. Se `z` tiver o tipo float [complex](<#/doc/numeric/complex/complex>), `csqrtf` é chamada. Se `z` for real ou inteiro, então a macro invoca a função real correspondente (sqrtf, [sqrt](<#/doc/numeric/math/sqrt>), sqrtl). Se `z` for imaginário, a versão de número complexo correspondente é chamada.

### Parâmetros

- **z** — argumento complexo

### Valor de retorno

Se nenhum erro ocorrer, retorna a raiz quadrada de `z`, no intervalo do semiplano direito, incluindo o eixo imaginário ([0; +∞) ao longo do eixo real e (−∞; +∞) ao longo do eixo imaginário.)

### Tratamento de erros e valores especiais

Os erros são reportados de forma consistente com [math_errhandling](<#/doc/numeric/math/math_errhandling>)

Se a implementação suportar aritmética de ponto flutuante IEEE,

*   A função é contínua no corte de ramo, levando em consideração o sinal da parte imaginária.
*   csqrt([conj](<#/doc/numeric/complex/conj>)(z)) == [conj](<#/doc/numeric/complex/conj>)(csqrt(z))
*   Se `z` for `±0+0i`, o resultado é `+0+0i`
*   Se `z` for `x+∞i`, o resultado é `+∞+∞i` mesmo que x seja NaN
*   Se `z` for `x+NaNi`, o resultado é `NaN+NaNi` (a menos que x seja ±∞) e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) pode ser levantado
*   Se `z` for `-∞+yi`, o resultado é `+0+∞i` para y positivo finito
*   Se `z` for `+∞+yi`, o resultado é `+∞+0i)` para y positivo finito
*   Se `z` for `-∞+NaNi`, o resultado é `NaN±∞i` (sinal da parte imaginária não especificado)
*   Se `z` for `+∞+NaNi`, o resultado é `+∞+NaNi`
*   Se `z` for `NaN+yi`, o resultado é `NaN+NaNi` e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) pode ser levantado
*   Se `z` for `NaN+NaNi`, o resultado é `NaN+NaNi`

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <complex.h>
    
    int main(void)
    {
        double complex z1 = csqrt(-4);
        printf("Square root of -4 is %.1f%+.1fi\n", creal(z1), cimag(z1));
    
        double complex z2 = csqrt(conj(-4)); // or, in C11, CMPLX(-4, -0.0)
        printf("Square root of -4-0i, the other side of the cut, is "
               "%.1f%+.1fi\n", creal(z2), cimag(z2));
    }
```

Saída:
```
    Square root of -4 is 0.0+2.0i
    Square root of -4-0i, the other side of the cut, is 0.0-2.0i
```

### Referências

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.3.8.3 As funções csqrt (p: 196)

    *   7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    *   G.6.4.2 As funções csqrt (p: 544)

    *   G.7 Matemática genérica de tipo <tgmath.h> (p: 545)

*   Padrão C99 (ISO/IEC 9899:1999):

    *   7.3.8.3 As funções csqrt (p: 178)

    *   7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337)

    *   G.6.4.2 As funções csqrt (p: 479)

    *   G.7 Matemática genérica de tipo <tgmath.h> (p: 480)

### Ver também

[ cpowcpowfcpowl](<#/doc/numeric/complex/cpow>)(C99)(C99)(C99) | calcula a função de potência complexa
(função)
[ sqrtsqrtfsqrtl](<#/doc/numeric/math/sqrt>)(C99)(C99) | calcula a raiz quadrada (\\(\small{\sqrt{x} }\\)√x)
(função)
[Documentação C++](<#/>) para sqrt