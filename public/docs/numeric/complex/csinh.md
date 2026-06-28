# csinhf, csinh, csinhl

Definido no cabeçalho [`<complex.h>`](<#/doc/numeric/complex>)

```c
float complex csinhf( float complex z );  // desde C99
double complex csinh( double complex z );  // desde C99
long double complex csinhl( long double complex z );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define sinh( z )  // desde C99
```

1-3) Calcula o seno hiperbólico complexo de `z`.

4) Macro genérica de tipo: Se `z` tiver o tipo long double [complex](<#/doc/numeric/complex/complex>), `csinhl` é chamada. Se `z` tiver o tipo double [complex](<#/doc/numeric/complex/complex>), `csinh` é chamada. Se `z` tiver o tipo float [complex](<#/doc/numeric/complex/complex>), `csinhf` é chamada. Se `z` for real ou inteiro, então a macro invoca a função real correspondente (sinhf, [sinh](<#/doc/numeric/math/sinh>), sinhl). Se `z` for imaginário, então a macro invoca a versão real correspondente da função [sin](<#/doc/numeric/math/sin>), implementando a fórmula sinh(iy) = i sin(y), e o tipo de retorno é imaginário.

### Parâmetros

- **z** — argumento complexo

### Valor de retorno

Se nenhum erro ocorrer, o seno hiperbólico complexo de `z` é retornado.

### Tratamento de erros e valores especiais

Erros são reportados de forma consistente com [math_errhandling](<#/doc/numeric/math/math_errhandling>)

Se a implementação suportar aritmética de ponto flutuante IEEE,

*   csinh([conj](<#/doc/numeric/complex/conj>)(z)) == [conj](<#/doc/numeric/complex/conj>)(csinh(z))
*   csinh(z) == -csinh(-z)
*   Se `z` for `+0+0i`, o resultado é `+0+0i`.
*   Se `z` for `+0+∞i`, o resultado é `±0+NaNi` (o sinal da parte real é não especificado) e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado.
*   Se `z` for `+0+NaNi`, o resultado é `±0+NaNi`.
*   Se `z` for `x+∞i` (para qualquer x finito positivo), o resultado é `NaN+NaNi` e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado.
*   Se `z` for `x+NaNi` (para qualquer x finito positivo), o resultado é `NaN+NaNi` e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) pode ser levantado.
*   Se `z` for `+∞+0i`, o resultado é `+∞+0i`.
*   Se `z` for `+∞+yi` (para qualquer y finito positivo), o resultado é `+∞cis(y)`.
*   Se `z` for `+∞+∞i`, o resultado é `±∞+NaNi` (o sinal da parte real é não especificado) e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado.
*   Se `z` for `+∞+NaNi`, o resultado é `±∞+NaNi` (o sinal da parte real é não especificado).
*   Se `z` for `NaN+0i`, o resultado é `NaN+0i`.
*   Se `z` for `NaN+yi` (para qualquer y finito não-zero), o resultado é `NaN+NaNi` e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) pode ser levantado.
*   Se `z` for `NaN+NaNi`, o resultado é `NaN+NaNi`.

onde cis(y) é cos(y) + i sin(y)

### Notas

A definição matemática do seno hiperbólico é sinh z = e^z - e^-z / 2

O seno hiperbólico é uma função inteira no plano complexo e não possui cortes de ramificação. É periódico em relação à componente imaginária, com período 2πi.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <math.h>
    #include <complex.h>
    
    int main(void)
    {
        double complex z = csinh(1);  // comporta-se como sinh real ao longo da linha real
        printf("sinh(1+0i) = %f%+fi (sinh(1)=%f)\n", creal(z), cimag(z), sinh(1));
    
        double complex z2 = csinh(I); // comporta-se como seno ao longo da linha imaginária
        printf("sinh(0+1i) = %f%+fi ( sin(1)=%f)\n", creal(z2), cimag(z2), sin(1));
    }
```

Saída:
```
    sinh(1+0i) = 1.175201+0.000000i (sinh(1)=1.175201)
    sinh(0+1i) = 0.000000+0.841471i ( sin(1)=0.841471)
```

### Referências

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.3.6.5 As funções csinh (p: 194)

    *   7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    *   G.6.2.5 As funções csinh (p: 541-542)

    *   G.7 Matemática genérica de tipo <tgmath.h> (p: 545)
*   Padrão C99 (ISO/IEC 9899:1999):

    *   7.3.6.5 As funções csinh (p: 175-176)

    *   7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337)

    *   G.6.2.5 As funções csinh (p: 476-477)

    *   G.7 Matemática genérica de tipo <tgmath.h> (p: 480)

### Veja também

[ ccoshccoshfccoshl](<#/doc/numeric/complex/ccosh>)(C99)(C99)(C99) | calcula o cosseno hiperbólico complexo
(função)
[ ctanhctanhfctanhl](<#/doc/numeric/complex/ctanh>)(C99)(C99)(C99) | calcula a tangente hiperbólica complexa
(função)
[ casinhcasinhfcasinhl](<#/doc/numeric/complex/casinh>)(C99)(C99)(C99) | calcula o seno hiperbólico complexo inverso
(função)
[ sinhsinhfsinhl](<#/doc/numeric/math/sinh>)(C99)(C99) | calcula o seno hiperbólico (sinh(x))
(função)
[Documentação C++](<#/>) para sinh