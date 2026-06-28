# cacosf, cacos, cacosl

Definido no cabeçalho [`<complex.h>`](<#/doc/numeric/complex>)

```c
float complex cacosf( float complex z );  // desde C99
double complex cacos( double complex z );  // desde C99
long double complex cacosl( long double complex z );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define acos( z )  // desde C99
```

1-3) Calcula o arco cosseno complexo de `z` com cortes de ramo fora do intervalo [−1,+1] ao longo do eixo real.

4) Macro de tipo genérico: Se `z` tiver o tipo long double [complex](<#/doc/numeric/complex/complex>), `cacosl` é chamada. Se `z` tiver o tipo double [complex](<#/doc/numeric/complex/complex>), `cacos` é chamada. Se `z` tiver o tipo float [complex](<#/doc/numeric/complex/complex>), `cacosf` é chamada. Se `z` for real ou inteiro, a macro invoca a função real correspondente (acosf, [acos](<#/doc/numeric/math/acos>), acosl). Se `z` for imaginário, a macro invoca a versão correspondente para números complexos.

### Parâmetros

- **z** — argumento complexo

### Valor de retorno

Se nenhum erro ocorrer, o arco cosseno complexo de `z` é retornado, no intervalo de uma faixa ilimitada ao longo do eixo imaginário e no intervalo [0; π] ao longo do eixo real.

### Tratamento de erros e valores especiais

Os erros são reportados de forma consistente com [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Se a implementação suportar aritmética de ponto flutuante IEEE,

  * cacos([conj](<#/doc/numeric/complex/conj>)(z)) == [conj](<#/doc/numeric/complex/conj>)(cacos(z))
  * Se `z` for `±0+0i`, o resultado é `π/2-0i`
  * Se `z` for `±0+NaNi`, o resultado é `π/2+NaNi`
  * Se `z` for `x+∞i` (para qualquer x finito), o resultado é `π/2-∞i`
  * Se `z` for `x+NaNi` (para qualquer x finito não nulo), o resultado é `NaN+NaNi` e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) pode ser levantado.
  * Se `z` for `-∞+yi` (para qualquer y finito positivo), o resultado é `π-∞i`
  * Se `z` for `+∞+yi` (para qualquer y finito positivo), o resultado é `+0-∞i`
  * Se `z` for `-∞+∞i`, o resultado é `3π/4-∞i`
  * Se `z` for `+∞+∞i`, o resultado é `π/4-∞i`
  * Se `z` for `±∞+NaNi`, o resultado é `NaN±∞i` (o sinal da parte imaginária é não especificado)
  * Se `z` for `NaN+yi` (para qualquer y finito), o resultado é `NaN+NaNi` e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) pode ser levantado
  * Se `z` for `NaN+∞i`, o resultado é `NaN-∞i`
  * Se `z` for `NaN+NaNi`, o resultado é `NaN+NaNi`

### Notas

O cosseno inverso (ou arco cosseno) é uma função multivalorada e requer um corte de ramo no plano complexo. O corte de ramo é convencionalmente colocado nos segmentos de linha (-∞,-1) e (1,∞) do eixo real.

A definição matemática do valor principal do arco cosseno é acos z = 1
---
2
π + _i_ ln(_i_ z + √1-z2
)

Para qualquer z, acos(z) = π - acos(-z)

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <math.h>
    #include <complex.h>
    
    int main(void)
    {
        double complex z = cacos(-2);
        printf("cacos(-2+0i) = %f%+fi\n", creal(z), cimag(z));
    
        double complex z2 = cacos(conj(-2)); // ou CMPLX(-2, -0.0)
        printf("cacos(-2-0i) (o outro lado do corte) = %f%+fi\n", creal(z2), cimag(z2));
    
        // para qualquer z, acos(z) = pi - acos(-z)
        double pi = acos(-1);
        double complex z3 = ccos(pi-z2);
        printf("ccos(pi - cacos(-2-0i) = %f%+fi\n", creal(z3), cimag(z3));
    }
```

Saída:
```
    cacos(-2+0i) = 3.141593-1.316958i
    cacos(-2-0i) (o outro lado do corte) = 3.141593+1.316958i
    ccos(pi - cacos(-2-0i) = 2.000000+0.000000i
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.3.5.1 As funções cacos (p: 190)

    

  * 7.25 Matemática de tipo genérico <tgmath.h> (p: 373-375)

    

  * G.6.1.1 As funções cacos (p: 539)

    

  * G.7 Matemática de tipo genérico <tgmath.h> (p: 545)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.3.5.1 As funções cacos (p: 172)

    

  * 7.22 Matemática de tipo genérico <tgmath.h> (p: 335-337)

    

  * G.6.1.1 As funções cacos (p: 474)

    

  * G.7 Matemática de tipo genérico <tgmath.h> (p: 480)

### Ver também

[ casincasinfcasinl](<#/doc/numeric/complex/casin>)(C99)(C99)(C99) | calcula o arco seno complexo
(função)
[ catancatanfcatanl](<#/doc/numeric/complex/catan>)(C99)(C99)(C99) | calcula o arco tangente complexo
(função)
[ ccosccosfccosl](<#/doc/numeric/complex/ccos>)(C99)(C99)(C99) | calcula o cosseno complexo
(função)
[ acosacosfacosl](<#/doc/numeric/math/acos>)(C99)(C99) | calcula o arco cosseno (\\({\small\arccos{x} }\\)arccos(x))
(função)
[Documentação C++](<#/>) para acos