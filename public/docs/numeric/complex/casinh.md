# casinhf, casinh, casinhl

Definido no cabeçalho [`<complex.h>`](<#/doc/numeric/complex>)

```c
float complex casinhf( float complex z );  // desde C99
double complex casinh( double complex z );  // desde C99
long double complex casinhl( long double complex z );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define asinh( z )  // desde C99
```

  
1-3) Calcula o seno hiperbólico de arco complexo de `z` com cortes de ramo fora do intervalo [−i; +i] ao longo do eixo imaginário.

4) Macro genérica de tipo: Se `z` tiver o tipo long double [complex](<#/doc/numeric/complex/complex>), `casinhl` é chamada. Se `z` tiver o tipo double [complex](<#/doc/numeric/complex/complex>), `casinh` é chamada. Se `z` tiver o tipo float [complex](<#/doc/numeric/complex/complex>), `casinhf` é chamada. Se `z` for real ou inteiro, então a macro invoca a função real correspondente (asinhf, [asinh](<#/doc/numeric/math/asinh>), asinhl). Se `z` for imaginário, então a macro invoca a versão real correspondente da função [asin](<#/doc/numeric/math/asin>), implementando a fórmula asinh(iy) = i asin(y), e o tipo de retorno é imaginário.

### Parâmetros

z  |  \-  |  argumento complexo   
  
### Valor de retorno

Se nenhum erro ocorrer, o seno hiperbólico de arco complexo de `z` é retornado, no intervalo de uma faixa matematicamente ilimitada ao longo do eixo real e no intervalo [−iπ/2; +iπ/2] ao longo do eixo imaginário. 

### Tratamento de erros e valores especiais

Erros são reportados de forma consistente com [math_errhandling](<#/doc/numeric/math/math_errhandling>)

Se a implementação suportar aritmética de ponto flutuante IEEE, 

  * casinh([conj](<#/doc/numeric/complex/conj>)(z)) == [conj](<#/doc/numeric/complex/conj>)(casinh(z))
  * casinh(-z) == -casinh(z)
  * Se `z` for `+0+0i`, o resultado é `+0+0i`
  * Se `z` for `x+∞i` (para qualquer x finito positivo), o resultado é `+∞+π/2`
  * Se `z` for `x+NaNi` (para qualquer x finito), o resultado é `NaN+NaNi` e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) pode ser levantado 
  * Se `z` for `+∞+yi` (para qualquer y finito positivo), o resultado é `+∞+0i`
  * Se `z` for `+∞+∞i`, o resultado é `+∞+iπ/4`
  * Se `z` for `+∞+NaNi`, o resultado é `+∞+NaNi`
  * Se `z` for `NaN+0i`, o resultado é `NaN+0i`
  * Se `z` for `NaN+yi` (para qualquer y finito não nulo), o resultado é `NaN+NaNi` e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) pode ser levantado 
  * Se `z` for `NaN+∞i`, o resultado é `±∞+NaNi` (o sinal da parte real é não especificado) 
  * Se `z` for `NaN+NaNi`, o resultado é `NaN+NaNi`

### Notas

Embora o padrão C nomeie esta função como "seno hiperbólico de arco complexo", as funções inversas das funções hiperbólicas são as funções de área. Seu argumento é a área de um setor hiperbólico, não um arco. O nome correto é "seno hiperbólico inverso complexo" e, menos comum, "seno hiperbólico de área complexo". 

O seno hiperbólico inverso é uma função multivalorada e requer um corte de ramo no plano complexo. O corte de ramo é convencionalmente colocado nos segmentos de linha (-_i_ ∞,-_i_) e (_i_ ,_i_ ∞) do eixo imaginário. 

A definição matemática do valor principal do seno hiperbólico inverso é asinh z = ln(z + √1+z2  
)

Para qualquer z, asinh(z) = asin(iz)  
---  
i  
  
### Exemplo

Execute este código
```
    #include <stdio.h>
    #include <complex.h>
     
    int main(void)
    {
        double complex z = casinh(0+2*I);
        printf("casinh(+0+2i) = %f%+fi\n", creal(z), cimag(z));
     
        double complex z2 = casinh(-conj(2*I)); // or casinh(CMPLX(-0.0, 2)) in C11
        printf("casinh(-0+2i) (the other side of the cut) = %f%+fi\n", creal(z2), cimag(z2));
     
        // for any z, asinh(z) = asin(iz)/i
        double complex z3 = casinh(1+2*I);
        printf("casinh(1+2i) = %f%+fi\n", creal(z3), cimag(z3));
        double complex z4 = casin((1+2*I)*I)/I;
        printf("casin(i * (1+2i))/i = %f%+fi\n", creal(z4), cimag(z4));
    }
```

Output: 
```
    casinh(+0+2i) = 1.316958+1.570796i
    casinh(-0+2i) (the other side of the cut) = -1.316958+1.570796i
    casinh(1+2i) = 1.469352+1.063440i
    casin(i * (1+2i))/i =  1.469352+1.063440i
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.3.6.2 As funções casinh (p: 192-193) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375) 

    

  * G.6.2.2 As funções casinh (p: 540) 

    

  * G.7 Matemática genérica de tipo <tgmath.h> (p: 545) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.3.6.2 As funções casinh (p: 174-175) 

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337) 

    

  * G.6.2.2 As funções casinh (p: 475) 

    

  * G.7 Matemática genérica de tipo <tgmath.h> (p: 480) 

### Veja também

[ cacoshcacoshfcacoshl](<#/doc/numeric/complex/cacosh>)(C99)(C99)(C99) |  calcula o cosseno hiperbólico de arco complexo   
(função)  
[ catanhcatanhfcatanhl](<#/doc/numeric/complex/catanh>)(C99)(C99)(C99) |  calcula a tangente hiperbólica de arco complexo   
(função)  
[ csinhcsinhfcsinhl](<#/doc/numeric/complex/csinh>)(C99)(C99)(C99) |  calcula o seno hiperbólico complexo   
(função)  
[ asinhasinhfasinhl](<#/doc/numeric/math/asinh>)(C99)(C99)(C99) |  calcula o seno hiperbólico inverso (\\({\small\operatorname{arsinh}{x} }\\)arsinh(x))   
(função)  
[Documentação C++](<#/>) para asinh