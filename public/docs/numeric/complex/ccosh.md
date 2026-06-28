# ccoshf, ccosh, ccoshl

Definido no cabeçalho [`<complex.h>`](<#/doc/numeric/complex>)

```c
float complex ccoshf( float complex z );  // desde C99
double complex ccosh( double complex z );  // desde C99
long double complex ccoshl( long double complex z );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define cosh( z )  // desde C99
```

1-3) Calcula o cosseno hiperbólico complexo de `z`.

4) Macro de tipo genérico: Se `z` tiver o tipo long double [complex](<#/doc/numeric/complex/complex>), `ccoshl` é chamada. Se `z` tiver o tipo double [complex](<#/doc/numeric/complex/complex>), `ccosh` é chamada. Se `z` tiver o tipo float [complex](<#/doc/numeric/complex/complex>), `ccoshf` é chamada. Se `z` for real ou inteiro, então a macro invoca a função real correspondente (coshf, [cosh](<#/doc/numeric/math/cosh>), coshl). Se `z` for imaginário, então a macro invoca a versão real correspondente da função [cos](<#/doc/numeric/math/cos>), implementando a fórmula cosh(iy) = cos(y), e o tipo de retorno é real.

### Parâmetros

- **z** — argumento complexo

### Valor de retorno

Se nenhum erro ocorrer, o cosseno hiperbólico complexo de `z` é retornado.

### Tratamento de erros e valores especiais

Erros são reportados de forma consistente com [math_errhandling](<#/doc/numeric/math/math_errhandling>)

Se a implementação suporta aritmética de ponto flutuante IEEE,

*   ccosh([conj](<#/doc/numeric/complex/conj>)(z)) == [conj](<#/doc/numeric/complex/conj>)(ccosh(z))
*   ccosh(z) == ccosh(-z)
*   Se `z` for `+0+0i`, o resultado é `1+0i`
*   Se `z` for `+0+∞i`, o resultado é `NaN±0i` (o sinal da parte imaginária é não especificado) e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado
*   Se `z` for `+0+NaNi`, o resultado é `NaN±0i` (o sinal da parte imaginária é não especificado)
*   Se `z` for `x+∞i` (para qualquer x finito não-zero), o resultado é `NaN+NaNi` e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado
*   Se `z` for `x+NaNi` (para qualquer x finito não-zero), o resultado é `NaN+NaNi` e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) pode ser levantado
*   Se `z` for `+∞+0i`, o resultado é `+∞+0i`
*   Se `z` for `+∞+yi` (para qualquer y finito não-zero), o resultado é `+∞cis(y)`
*   Se `z` for `+∞+∞i`, o resultado é `±∞+NaNi` (o sinal da parte real é não especificado) e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado
*   Se `z` for `+∞+NaN`, o resultado é `+∞+NaN`
*   Se `z` for `NaN+0i`, o resultado é `NaN±0i` (o sinal da parte imaginária é não especificado)
*   Se `z` for `NaN+yi` (para qualquer y finito não-zero), o resultado é `NaN+NaNi` e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) pode ser levantado
*   Se `z` for `NaN+NaNi`, o resultado é `NaN+NaNi`

onde cis(y) é cos(y) + i sin(y)

### Notas

A definição matemática do cosseno hiperbólico é cosh z = ez
+e-z
---
2

O cosseno hiperbólico é uma função inteira no plano complexo e não possui cortes de ramo. É periódico em relação à componente imaginária, com período 2πi

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <math.h>
    #include <complex.h>
     
    int main(void)
    {
        double complex z = ccosh(1);  // behaves like real cosh along the real line
        printf("cosh(1+0i) = %f%+fi (cosh(1)=%f)\n", creal(z), cimag(z), cosh(1));
     
        double complex z2 = ccosh(I); // behaves like real cosine along the imaginary line
        printf("cosh(0+1i) = %f%+fi ( cos(1)=%f)\n", creal(z2), cimag(z2), cos(1));
    }
```

Saída:
```
    cosh(1+0i) = 1.543081+0.000000i (cosh(1)=1.543081)
    cosh(0+1i) = 0.540302+0.000000i ( cos(1)=0.540302)
```

### Referências

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.3.6.4 As funções ccosh (p: 193)

    *   7.25 Matemática de tipo genérico <tgmath.h> (p: 373-375)

    *   G.6.2.4 As funções ccosh (p: 541)

    *   G.7 Matemática de tipo genérico <tgmath.h> (p: 545)

*   Padrão C99 (ISO/IEC 9899:1999):

    *   7.3.6.4 As funções ccosh (p: 175)

    *   7.22 Matemática de tipo genérico <tgmath.h> (p: 335-337)

    *   G.6.2.4 As funções ccosh (p: 476)

    *   G.7 Matemática de tipo genérico <tgmath.h> (p: 480)

### Veja também

[ csinhcsinhfcsinhl](<#/doc/numeric/complex/csinh>)(C99)(C99)(C99) | calcula o seno hiperbólico complexo
(função)
[ ctanhctanhfctanhl](<#/doc/numeric/complex/ctanh>)(C99)(C99)(C99) | calcula a tangente hiperbólica complexa
(função)
[ cacoshcacoshfcacoshl](<#/doc/numeric/complex/cacosh>)(C99)(C99)(C99) | calcula o arco cosseno hiperbólico complexo
(função)
[ coshcoshfcoshl](<#/doc/numeric/math/cosh>)(C99)(C99) | calcula o cosseno hiperbólico (\\({\small\cosh{x} }\\)cosh(x))
(função)
[Documentação C++](<#/>) para cosh