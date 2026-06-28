# floor, floorf, floorl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float floorf( float arg );  // desde C99
double floor( double arg );
long double floorl( long double arg );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define floor( arg )  // desde C99
```

1-3) Calcula o maior valor inteiro não maior que arg.

4) Macro genérica de tipo: Se arg tiver o tipo long double, `floorl` é chamada. Caso contrário, se arg tiver um tipo inteiro ou o tipo double, `floor` é chamada. Caso contrário, `floorf` é chamada.

### Parâmetros

- **arg** — valor de ponto flutuante

### Valor de retorno

Se nenhum erro ocorrer, o maior valor inteiro não maior que arg, ou seja ⌊arg⌋, é retornado.

Valor de retorno

Argumento

### Tratamento de erros

Erros são reportados conforme especificado em `[`math_errhandling`](<#/doc/numeric/math/math_errhandling>)`.

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559):

  * O `[`modo de arredondamento`](<#/doc/numeric/fenv/FE_round>)` atual não tem efeito.
  * Se arg for ±∞, ele é retornado, sem modificação.
  * Se arg for ±0, ele é retornado, sem modificação.
  * Se arg for NaN, NaN é retornado.

### Observações

[`FE_INEXACT`](<#/doc/numeric/fenv/FE_exceptions>)` pode ser (mas não é obrigatório ser) levantado ao arredondar um valor finito não inteiro.`

Os maiores valores de ponto flutuante representáveis são inteiros exatos em todos os formatos de ponto flutuante padrão, então esta função nunca transborda por si só; no entanto, o resultado pode transbordar qualquer tipo inteiro (incluindo `[`intmax_t`](<#/doc/types/integer>)`), quando armazenado em uma variável inteira.`

### Exemplo

Execute este código
```c
    #include <math.h>
    #include <stdio.h>
    
    int main(void)
    {
        printf("floor(+2.7) = %+.1f\n", floor(2.7));
        printf("floor(-2.7) = %+.1f\n", floor(-2.7));
        printf("floor(-0.0) = %+.1f\n", floor(-0.0));
        printf("floor(-Inf) = %+f\n",   floor(-INFINITY));
    }
```

Saída possível:
```
    floor(+2.7) = +2.0
    floor(-2.7) = -3.0
    floor(-0.0) = -0.0
    floor(-Inf) = -inf
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.12.9.2 As funções floor (p: TBD)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: TBD)

    

  * F.10.6.2 As funções floor (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.12.9.2 As funções floor (p: TBD)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: TBD)

    

  * F.10.6.2 As funções floor (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.12.9.2 As funções floor (p: 251)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    

  * F.10.6.2 As funções floor (p: 526)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.12.9.2 As funções floor (p: 232)

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337)

    

  * F.9.6.2 As funções floor (p: 463)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.5.6.3 A função floor

### Veja também

[`ceilceilfceill`](<#/doc/numeric/math/ceil>)`(C99)(C99) | calcula o menor inteiro não menor que o valor dado`
(função)
[`trunctruncftruncl`](<#/doc/numeric/math/trunc>)`(C99)(C99)(C99) | arredonda para o inteiro mais próximo não maior em magnitude que o valor dado`
(função)
[`roundroundfroundllroundlroundflroundlllroundllroundfllroundl`](<#/doc/numeric/math/round>)`(C99)(C99)(C99)(C99)(C99)(C99)(C99)(C99)(C99) | arredonda para o inteiro mais próximo, arredondando para longe de zero em casos de meio-ponto`
(função)
[`Documentação C++`](<#/>)` para floor`