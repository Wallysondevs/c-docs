# cacoshf, cacosh, cacoshl

Definido no cabeçalho [`<complex.h>`](<#/doc/numeric/complex>)

```c
float complex cacoshf( float complex z );  // desde C99
double complex cacosh( double complex z );  // desde C99
long double complex cacoshl( long double complex z );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define acosh( z )  // desde C99
```

1-3) Calcula o cosseno hiperbólico de arco complexo de um valor complexo `z` com corte de ramo em valores menores que 1 ao longo do eixo real.

4) Macro genérica de tipo: Se `z` tiver o tipo long double [complex](<#/doc/numeric/complex/complex>), `cacoshl` é chamada. Se `z` tiver o tipo double [complex](<#/doc/numeric/complex/complex>), `cacosh` é chamada. Se `z` tiver o tipo float [complex](<#/doc/numeric/complex/complex>), `cacoshf` é chamada. Se `z` for real ou inteiro, então a macro invoca a função real correspondente (acoshf, [acosh](<#/doc/numeric/math/acosh>), acoshl). Se `z` for imaginário, então a macro invoca a versão correspondente de número complexo e o tipo de retorno é complexo.

### Parâmetros

- **z** — argumento complexo

### Valor de retorno

O cosseno hiperbólico de arco complexo de `z` no intervalo [0; ∞) ao longo do eixo real e no intervalo [−iπ; +iπ] ao longo do eixo imaginário.

### Tratamento de erros e valores especiais

Erros são reportados de forma consistente com [math_errhandling](<#/doc/numeric/math/math_errhandling>)

Se a implementação suportar aritmética de ponto flutuante IEEE,

*   cacosh([conj](<#/doc/numeric/complex/conj>)(z)) == [conj](<#/doc/numeric/complex/conj>)(cacosh(z))
*   Se `z` for `±0+0i`, o resultado é `+0+iπ/2`
*   Se `z` for `+x+∞i` (para qualquer x finito), o resultado é `+∞+iπ/2`
*   Se `z` for `+x+NaNi` (para x finito não-zero), o resultado é `NaN+NaNi` e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) pode ser levantado.
*   Se `z` for `0+NaNi`, o resultado é `NaN±iπ/2`, onde o sinal da parte imaginária é não especificado
*   Se `z` for `-∞+yi` (para qualquer y finito positivo), o resultado é `+∞+iπ`
*   Se `z` for `+∞+yi` (para qualquer y finito positivo), o resultado é `+∞+0i`
*   Se `z` for `-∞+∞i`, o resultado é `+∞+3iπ/4`
*   Se `z` for `+∞+∞i`, o resultado é `+∞+iπ/4`
*   Se `z` for `±∞+NaNi`, o resultado é `+∞+NaNi`
*   Se `z` for `NaN+yi` (para qualquer y finito), o resultado é `NaN+NaNi` e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) pode ser levantado.
*   Se `z` for `NaN+∞i`, o resultado é `+∞+NaNi`
*   Se `z` for `NaN+NaNi`, o resultado é `NaN+NaNi`

### Notas

Embora o padrão C nomeie esta função como "cosseno hiperbólico de arco complexo", as funções inversas das funções hiperbólicas são as funções de área. Seu argumento é a área de um setor hiperbólico, não um arco. O nome correto é "cosseno hiperbólico inverso complexo" e, menos comum, "cosseno hiperbólico de área complexo".

O cosseno hiperbólico inverso é uma função multivalorada e requer um corte de ramo no plano complexo. O corte de ramo é convencionalmente colocado no segmento de linha (-∞,+1) do eixo real.

A definição matemática do valor principal do cosseno hiperbólico inverso é acosh z = ln(z + √z+1 √z-1)

Para qualquer z, acosh(z) = √z-1
---
√1-z
acos(z), ou simplesmente i acos(z) na metade superior do plano complexo.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <complex.h>
    
    int main(void)
    {
        double complex z = cacosh(0.5);
        printf("cacosh(+0.5+0i) = %f%+fi\n", creal(z), cimag(z));
    
        double complex z2 = conj(0.5); // or cacosh(CMPLX(0.5, -0.0)) in C11
        printf("cacosh(+0.5-0i) (the other side of the cut) = %f%+fi\n", creal(z2), cimag(z2));
    
        // in upper half-plane, acosh(z) = i*acos(z) 
        double complex z3 = casinh(1+I);
        printf("casinh(1+1i) = %f%+fi\n", creal(z3), cimag(z3));
        double complex z4 = I*casin(1+I);
        printf("I*asin(1+1i) = %f%+fi\n", creal(z4), cimag(z4));
    }
```

Saída:
```
    cacosh(+0.5+0i) = 0.000000-1.047198i
    cacosh(+0.5-0i) (the other side of the cut) = 0.500000-0.000000i
    casinh(1+1i) = 1.061275+0.666239i
    I*asin(1+1i) = -1.061275+0.666239i
```

### Referências

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.3.6.1 As funções cacosh (p: 192)

    *   7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    *   G.6.2.1 As funções cacosh (p: 539-540)

    *   G.7 Matemática genérica de tipo <tgmath.h> (p: 545)
*   Padrão C99 (ISO/IEC 9899:1999):

    *   7.3.6.1 As funções cacosh (p: 174)

    *   7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337)

    *   G.6.2.1 As funções cacosh (p: 474-475)

    *   G.7 Matemática genérica de tipo <tgmath.h> (p: 480)

### Veja também

[ cacoscacosfcacosl](<#/doc/numeric/complex/cacos>)(C99)(C99)(C99) | calcula o cosseno de arco complexo
(função)
[ casinhcasinhfcasinhl](<#/doc/numeric/complex/casinh>)(C99)(C99)(C99) | calcula o seno hiperbólico de arco complexo
(função)
[ catanhcatanhfcatanhl](<#/doc/numeric/complex/catanh>)(C99)(C99)(C99) | calcula a tangente hiperbólica de arco complexo
(função)
[ ccoshccoshfccoshl](<#/doc/numeric/complex/ccosh>)(C99)(C99)(C99) | calcula o cosseno hiperbólico complexo
(função)
[ acoshacoshfacoshl](<#/doc/numeric/math/acosh>)(C99)(C99)(C99) | calcula o cosseno hiperbólico inverso (\\({\small\operatorname{arcosh}{x} }\\)arcosh(x))
(função)
[Documentação C++](<#/>) para acosh