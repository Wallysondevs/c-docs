# cabsf, cabs, cabsl

Definido no cabeçalho [`<complex.h>`](<#/doc/numeric/complex>)

```c
float cabsf( float complex z );  // desde C99
double cabs( double complex z );  // desde C99
long double cabsl( long double complex z );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define fabs( z )  // desde C99
```

1-3) Calcula o valor absoluto complexo (também conhecido como norma, módulo ou magnitude) de `z`.

4) Macro genérica de tipo: se `z` tiver o tipo long double [complex](<#/doc/numeric/complex/complex>) ou long double [imaginary](<#/doc/numeric/complex/imaginary>), `cabsl` é chamada. Se `z` tiver o tipo float [complex](<#/doc/numeric/complex/complex>) ou float [imaginary](<#/doc/numeric/complex/imaginary>), `cabsf` é chamada. Se `z` tiver o tipo double [complex](<#/doc/numeric/complex/complex>) ou double [imaginary](<#/doc/numeric/complex/imaginary>), `cabs` é chamada. Para tipos reais e inteiros, a versão correspondente de [fabs](<#/doc/numeric/math/fabs>) é chamada.

### Parâmetros

- **z** — argumento complexo

### Valor de retorno

Se nenhum erro ocorrer, retorna o valor absoluto (norma, magnitude) de `z`.

Erros e casos especiais são tratados como se a função fosse implementada como [hypot](<#/doc/numeric/math/hypot>)([creal](<#/doc/numeric/complex/creal>)(z), [cimag](<#/doc/numeric/complex/cimag>)(z))

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <complex.h>
     
    int main(void)
    {
        double complex z = 1.0 + 1.0*I;
        printf("%.1f%+.1fi cartesian is rho=%f theta=%f polar\n",
               creal(z), cimag(z), cabs(z), carg(z));
    }
```

Saída:
```
    1.0+1.0i cartesian is rho=1.414214 theta=0.785398 polar
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

  * 7.3.8.1 As funções cabs (p: 195)

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

  * G.7 Matemática genérica de tipo <tgmath.h> (p: 545)

  * Padrão C99 (ISO/IEC 9899:1999):

  * 7.3.8.1 As funções cabs (p: 177)

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337)

  * G.7 Matemática genérica de tipo <tgmath.h> (p: 480)

### Veja também

[ cargcargfcargl](<#/doc/numeric/complex/carg>)(C99)(C99)(C99) | calcula o ângulo de fase de um número complexo
(função)
[ abslabsllabs](<#/doc/numeric/math/abs>)(C99) | calcula o valor absoluto de um valor inteiro (\\(\small{|x|}\\)|x|)
(função)
[ fabsfabsffabsl](<#/doc/numeric/math/fabs>)(C99)(C99) | calcula o valor absoluto de um valor de ponto flutuante (\\(\small{|x|}\\)|x|)
(função)
[ hypothypotfhypotl](<#/doc/numeric/math/hypot>)(C99)(C99)(C99) | calcula a raiz quadrada da soma dos quadrados de dois números dados (\\(\scriptsize{\sqrt{x^2+y^2} }\\)√x2
+y2
)
(função)
[Documentação C++](<#/>) para abs