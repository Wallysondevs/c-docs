# ctanhf, ctanh, ctanhl

Definido no cabeçalho [`<complex.h>`](<#/doc/numeric/complex>)

```c
float complex ctanhf( float complex z );  // desde C99
double complex ctanh( double complex z );  // desde C99
long double complex ctanhl( long double complex z );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define tanh( z )  // desde C99
```

1-3) Calcula a tangente hiperbólica complexa de `z`.

4) Macro genérica de tipo: Se `z` tiver o tipo long double [complex](<#/doc/numeric/complex/complex>), `ctanhl` é chamada. Se `z` tiver o tipo double [complex](<#/doc/numeric/complex/complex>), `ctanh` é chamada. Se `z` tiver o tipo float [complex](<#/doc/numeric/complex/complex>), `ctanhf` é chamada. Se `z` for real ou inteiro, a macro invoca a função real correspondente (tanhf, [tanh](<#/doc/numeric/math/tanh>), tanhl). Se `z` for imaginário, a macro invoca a versão real correspondente da função [tan](<#/doc/numeric/math/tan>), implementando a fórmula tanh(iy) = i tan(y), e o tipo de retorno é imaginário.

### Parâmetros

- **z** — argumento complexo

### Valor de retorno

Se nenhum erro ocorrer, a tangente hiperbólica complexa de `z` é retornada

### Tratamento de erros e valores especiais

Os erros são reportados de forma consistente com [math_errhandling](<#/doc/numeric/math/math_errhandling>)

Se a implementação suportar aritmética de ponto flutuante IEEE,

  * ctanh([conj](<#/doc/numeric/complex/conj>)(z)) == [conj](<#/doc/numeric/complex/conj>)(ctanh(z))
  * ctanh(-z) == -ctanh(z)
  * Se `z` for `+0+0i`, o resultado é `+0+0i`
  * Se `z` for `x+∞i` (para qualquer[1](<#/doc/numeric/complex/ctanh>) x finito), o resultado é `NaN+NaNi` e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado
  * Se `z` for `x+NaN` (para qualquer[2](<#/doc/numeric/complex/ctanh>) x finito), o resultado é `NaN+NaNi` e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) pode ser levantado
  * Se `z` for `+∞+yi` (para qualquer y positivo finito), o resultado é `1+0i`
  * Se `z` for `+∞+∞i`, o resultado é `1±0i` (o sinal da parte imaginária é não especificado)
  * Se `z` for `+∞+NaNi`, o resultado é `1±0i` (o sinal da parte imaginária é não especificado)
  * Se `z` for `NaN+0i`, o resultado é `NaN+0i`
  * Se `z` for `NaN+yi` (para qualquer y não-zero), o resultado é `NaN+NaNi` e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) pode ser levantado
  * Se `z` for `NaN+NaNi`, o resultado é `NaN+NaNi`

  1. [↑](<#/doc/numeric/complex/ctanh>) de acordo com [DR471](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n1892.htm#dr_471>), isso só é válido para x não-zero. Se `z` for `0+∞i`, o resultado deve ser `0+NaNi`
  2. [↑](<#/doc/numeric/complex/ctanh>) de acordo com [DR471](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n1892.htm#dr_471>), isso só é válido para x não-zero. Se `z` for `0+NaNi`, o resultado deve ser `0+NaNi`

### Notas

A definição matemática da tangente hiperbólica é tanh z = ez
-e-z

---
ez
+e-z

A tangente hiperbólica é uma função analítica no plano complexo e não possui cortes de ramo. É periódica em relação à componente imaginária, com período πi, e possui polos de primeira ordem ao longo da linha imaginária, nas coordenadas (0, π(1/2 + n)). No entanto, nenhuma representação comum de ponto flutuante é capaz de representar π/2 exatamente, portanto, não há valor do argumento para o qual ocorra um erro de polo.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <math.h>
    #include <complex.h>
    
    int main(void)
    {
        double complex z = ctanh(1);  // behaves like real tanh along the real line
        printf("tanh(1+0i) = %f%+fi (tanh(1)=%f)\n", creal(z), cimag(z), tanh(1));
    
        double complex z2 = ctanh(I); // behaves like tangent along the imaginary line
        printf("tanh(0+1i) = %f%+fi ( tan(1)=%f)\n", creal(z2), cimag(z2), tan(1));
    }
```

Saída:
```
    tanh(1+0i) = 0.761594+0.000000i (tanh(1)=0.761594)
    tanh(0+1i) = 0.000000+1.557408i ( tan(1)=1.557408)
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.3.6.6 As funções ctanh (p: 194)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    

  * G.6.2.6 As funções ctanh (p: 542)

    

  * G.7 Matemática genérica de tipo <tgmath.h> (p: 545)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.3.6.6 As funções ctanh (p: 176)

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337)

    

  * G.6.2.6 As funções ctanh (p: 477)

    

  * G.7 Matemática genérica de tipo <tgmath.h> (p: 480)

### Ver também

[ csinhcsinhfcsinhl](<#/doc/numeric/complex/csinh>)(C99)(C99)(C99) | calcula o seno hiperbólico complexo
(função)
[ ccoshccoshfccoshl](<#/doc/numeric/complex/ccosh>)(C99)(C99)(C99) | calcula o cosseno hiperbólico complexo
(função)
[ catanhcatanhfcatanhl](<#/doc/numeric/complex/catanh>)(C99)(C99)(C99) | calcula a arco tangente hiperbólica complexa
(função)
[ tanhtanhftanhl](<#/doc/numeric/math/tanh>)(C99)(C99) | calcula a tangente hiperbólica (\\({\small\tanh{x} }\\)tanh(x))
(função)
[Documentação C++](<#/>) para tanh