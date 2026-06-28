# tanh, tanhf, tanhl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float tanhf( float arg );  // desde C99
double tanh( double arg );
long double tanhl( long double arg );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define tanh( arg )  // desde C99
```

1-3) Calcula a tangente hiperbólica de arg.

4) Macro de tipo genérico: Se o argumento tiver o tipo long double, `tanhl` é chamada. Caso contrário, se o argumento tiver um tipo inteiro ou o tipo double, `tanh` é chamada. Caso contrário, `tanhf` é chamada. Se o argumento for complexo, então a macro invoca a função complexa correspondente ([ctanhf](<#/doc/numeric/complex/ctanh>), [ctanh](<#/doc/numeric/complex/ctanh>), [ctanhl](<#/doc/numeric/complex/ctanh>)).

### Parâmetros

- **arg** — valor de ponto flutuante representando um ângulo hiperbólico

### Valor de retorno

Se nenhum erro ocorrer, a tangente hiperbólica de arg (tanh(arg), ou earg
-e-arg

---
earg
+e-arg

) é retornada.

Se ocorrer um erro de faixa devido a underflow, o resultado correto (após arredondamento) é retornado.

### Tratamento de erros

Erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559),

  * Se o argumento for ±0, ±0 é retornado.
  * Se o argumento for ±∞, ±1 é retornado.
  * Se o argumento for NaN, NaN é retornado.

### Notas

[POSIX especifica](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/tanh.html>) que, em caso de underflow, arg é retornado sem modificações, e se isso não for suportado, um valor definido pela implementação não maior que [DBL_MIN](<#/doc/types/limits>), [FLT_MIN](<#/doc/types/limits>), e [LDBL_MIN](<#/doc/types/limits>) é retornado.

### Exemplo

Execute este código
```
    #include <math.h>
    #include <stdio.h>
    
    int main(void)
    {
        printf("tanh(1) = %f\ntanh(-1) = %f\n", tanh(1), tanh(-1));
        printf("tanh(0.1)*sinh(0.2)-cosh(0.2) = %f\n", tanh(0.1) * sinh(0.2) - cosh(0.2));
        // special values
        printf("tanh(+0) = %f\ntanh(-0) = %f\n", tanh(0.0), tanh(-0.0));
    }
```

Saída:
```
    tanh(1) = 0.761594
    tanh(-1) = -0.761594
    tanh(0.1)*sinh(0.2)-cosh(0.2) = -1.000000
    tanh(+0) = 0.000000
    tanh(-0) = -0.000000
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.12.5.6 As funções tanh (p: TBD)

    

  * 7.25 Matemática de tipo genérico <tgmath.h> (p: TBD)

    

  * F.10.2.6 As funções tanh (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.12.5.6 As funções tanh (p: TBD)

    

  * 7.25 Matemática de tipo genérico <tgmath.h> (p: TBD)

    

  * F.10.2.6 As funções tanh (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.12.5.6 As funções tanh (p: 242)

    

  * 7.25 Matemática de tipo genérico <tgmath.h> (p: 373-375)

    

  * F.10.2.6 As funções tanh (p: 520)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.12.5.6 As funções tanh (p: 222-223)

    

  * 7.22 Matemática de tipo genérico <tgmath.h> (p: 335-337)

    

  * F.9.2.6 As funções tanh (p: 457)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.5.3.3 A função tanh

### Veja também

[ sinhsinhfsinhl](<#/doc/numeric/math/sinh>)(C99)(C99) | calcula o seno hiperbólico (\\({\small\sinh{x} }\\)sinh(x))
(função)
[ coshcoshfcoshl](<#/doc/numeric/math/cosh>)(C99)(C99) | calcula o cosseno hiperbólico (\\({\small\cosh{x} }\\)cosh(x))
(função)
[ atanhatanhfatanhl](<#/doc/numeric/math/atanh>)(C99)(C99)(C99) | calcula a tangente hiperbólica inversa (\\({\small\operatorname{artanh}{x} }\\)artanh(x))
(função)
[ ctanhctanhfctanhl](<#/doc/numeric/complex/ctanh>)(C99)(C99)(C99) | calcula a tangente hiperbólica complexa
(função)
[Documentação C++](<#/>) para tanh