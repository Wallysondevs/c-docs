# catanhf, catanh, catanhl

Definido no cabeçalho [`<complex.h>`](<#/doc/numeric/complex>)

```c
float complex catanhf( float complex z );  // desde C99
double complex catanh( double complex z );  // desde C99
long double complex catanhl( long double complex z );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define atanh( z )  // desde C99
```

  
1-3) Calcula a tangente hiperbólica de arco complexa de `z` com cortes de ramo fora do intervalo [−1; +1] ao longo do eixo real.

4) Macro genérica de tipo: Se `z` tiver o tipo `long double complex`, `catanhl` é chamada. Se `z` tiver o tipo `double complex`, `catanh` é chamada. Se `z` tiver o tipo `float complex`, `catanhf` é chamada. Se `z` for real ou inteiro, a macro invoca a função real correspondente (atanhf, [atanh](<#/doc/numeric/math/atanh>), atanhl). Se `z` for imaginário, a macro invoca a versão real correspondente de [atan](<#/doc/numeric/math/atan>), implementando a fórmula atanh(iy) = i atan(y), e o tipo de retorno é imaginário.

### Parâmetros

z  |  \-  |  argumento complexo   
  
### Valor de retorno

Se nenhum erro ocorrer, a tangente hiperbólica de arco complexa de `z` é retornada, no intervalo de uma semi-faixa matematicamente ilimitada ao longo do eixo real e no intervalo [−iπ/2; +iπ/2] ao longo do eixo imaginário. 

### Tratamento de erros e valores especiais

Erros são reportados de forma consistente com [math_errhandling](<#/doc/numeric/math/math_errhandling>)

Se a implementação suporta aritmética de ponto flutuante IEEE, 

  * catanh([conj](<#/doc/numeric/complex/conj>)(z)) == [conj](<#/doc/numeric/complex/conj>)(catanh(z))
  * catanh(-z) == -catanh(z)
  * Se `z` for `+0+0i`, o resultado é `+0+0i`
  * Se `z` for `+0+NaNi`, o resultado é `+0+NaNi`
  * Se `z` for `+1+0i`, o resultado é `+∞+0i` e [FE_DIVBYZERO](<#/doc/numeric/fenv/FE_exceptions>) é levantado 
  * Se `z` for `x+∞i` (para qualquer x positivo finito), o resultado é `+0+iπ/2`
  * Se `z` for `x+NaNi` (para qualquer x finito não nulo), o resultado é `NaN+NaNi` e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) pode ser levantado 
  * Se `z` for `+∞+yi` (para qualquer y positivo finito), o resultado é `+0+iπ/2`
  * Se `z` for `+∞+∞i`, o resultado é `+0+iπ/2`
  * Se `z` for `+∞+NaNi`, o resultado é `+0+NaNi`
  * Se `z` for `NaN+yi` (para qualquer y finito), o resultado é `NaN+NaNi` e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) pode ser levantado 
  * Se `z` for `NaN+∞i`, o resultado é `±0+iπ/2` (o sinal da parte real é não especificado) 
  * Se `z` for `NaN+NaNi`, o resultado é `NaN+NaNi`

### Notas

Embora o padrão C nomeie esta função como "tangente hiperbólica de arco complexa", as funções inversas das funções hiperbólicas são as funções de área. Seu argumento é a área de um setor hiperbólico, não um arco. O nome correto é "tangente hiperbólica inversa complexa" e, menos comum, "tangente hiperbólica de área complexa". 

A tangente hiperbólica inversa é uma função multivalorada e requer um corte de ramo no plano complexo. O corte de ramo é convencionalmente colocado nos segmentos de linha (-∞,-1] e [+1,+∞) do eixo real. 

A definição matemática do valor principal da tangente hiperbólica inversa é atanh z = ln(1+z)-ln(z-1)  
---  
2  
. 

  

Para qualquer z, atanh(z) = atan(iz)  
---  
i  
  
### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <complex.h>
    
    int main(void)
    {
        double complex z = catanh(2);
        printf("catanh(+2+0i) = %f%+fi\n", creal(z), cimag(z));
    
        double complex z2 = catanh(conj(2)); // or catanh(CMPLX(2, -0.0)) in C11
        printf("catanh(+2-0i) (the other side of the cut) = %f%+fi\n", creal(z2), cimag(z2));
    
        // for any z, atanh(z) = atan(iz)/i
        double complex z3 = catanh(1+2*I);
        printf("catanh(1+2i) = %f%+fi\n", creal(z3), cimag(z3));
        double complex z4 = catan((1+2*I)*I)/I;
        printf("catan(i * (1+2i))/i = %f%+fi\n", creal(z4), cimag(z4));
    }
```

Saída: 
```
    catanh(+2+0i) = 0.549306+1.570796i
    catanh(+2-0i) (the other side of the cut) = 0.549306-1.570796i
    catanh(1+2i) = 0.173287+1.178097i
    catan(i * (1+2i))/i = 0.173287+1.178097i
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.3.6.3 As funções catanh (p: 193) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375) 

    

  * G.6.2.3 As funções catanh (p: 540-541) 

    

  * G.7 Matemática genérica de tipo <tgmath.h> (p: 545) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.3.6.3 As funções catanh (p: 175) 

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337) 

    

  * G.6.2.3 As funções catanh (p: 475-476) 

    

  * G.7 Matemática genérica de tipo <tgmath.h> (p: 480) 

### Ver também

[ casinhcasinhfcasinhl](<#/doc/numeric/complex/casinh>)(C99)(C99)(C99) |  calcula o seno hiperbólico de arco complexo   
(função)  
[ cacoshcacoshfcacoshl](<#/doc/numeric/complex/cacosh>)(C99)(C99)(C99) |  calcula o cosseno hiperbólico de arco complexo   
(função)  
[ ctanhctanhfctanhl](<#/doc/numeric/complex/ctanh>)(C99)(C99)(C99) |  calcula a tangente hiperbólica complexa   
(função)  
[ atanhatanhfatanhl](<#/doc/numeric/math/atanh>)(C99)(C99)(C99) |  calcula a tangente hiperbólica inversa (\\({\small\operatorname{artanh}{x} }\\)artanh(x))   
(função)  
[Documentação C++](<#/>) para atanh