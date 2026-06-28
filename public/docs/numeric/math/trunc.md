# trunc, truncf, truncl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
`float truncf( float arg );`  // desde C99
`double trunc( double arg );`  // desde C99
`long double truncl( long double arg );`  // desde C99
Definido no cabeçalho ``<tgmath.h>``
`#define trunc( arg )`  // desde C99
```

1-3) Calcula o inteiro mais próximo não maior em magnitude que arg.

4) Macro genérica de tipo: Se arg tiver o tipo `long double`, `truncl` é chamada. Caso contrário, se arg tiver um tipo inteiro ou o tipo `double`, `trunc` é chamada. Caso contrário, `truncf` é chamada.

### Parâmetros

- **arg** — valor de ponto flutuante

### Valor de retorno

Se nenhum erro ocorrer, o valor inteiro mais próximo não maior em magnitude que arg (em outras palavras, arg arredondado em direção a zero), é retornado.

Valor de retorno

Argumento

### Tratamento de erros

Erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Se a implementação suporta aritmética de ponto flutuante IEEE (IEC 60559):

*   O [modo de arredondamento](<#/doc/numeric/fenv/FE_round>) atual não tem efeito.
*   Se arg for ±∞, ele é retornado, inalterado.
*   Se arg for ±0, ele é retornado, inalterado.
*   Se arg for NaN, NaN é retornado.

### Observações

[`FE_INEXACT`](<#/doc/numeric/fenv/FE_exceptions>) pode ser (mas não é obrigatório ser) levantado ao truncar um valor finito não inteiro.

Os maiores valores de ponto flutuante representáveis são inteiros exatos em todos os formatos padrão de ponto flutuante, então esta função nunca transborda por si só; no entanto, o resultado pode transbordar qualquer tipo inteiro (incluindo [`intmax_t`](<#/doc/types/integer>)), quando armazenado em uma variável inteira.

A conversão implícita de tipos de ponto flutuante para tipos inteiros também arredonda em direção a zero, mas é limitada aos valores que podem ser representados pelo tipo de destino.

### Exemplo

Execute este código
```c
    #include <math.h>
    #include <stdio.h>
    
    int main(void)
    {
        printf("trunc(+2.7) = %+.1f\n", trunc(+2.7));
        printf("trunc(-2.7) = %+.1f\n", trunc(-2.7));
        printf("trunc(-0.0) = %+.1f\n", trunc(-0.0));
        printf("trunc(-Inf) = %+f\n",   trunc(-INFINITY));
    }
```

Saída possível:
```
    trunc(+2.7) = +2.0
    trunc(-2.7) = -2.0
    trunc(-0.0) = -0.0
    trunc(-Inf) = -inf
```

### Referências

*   Padrão C23 (ISO/IEC 9899:2024):

    *   7.12.9.8 As funções trunc (p: TBD)

    *   7.25 Matemática genérica de tipo <tgmath.h> (p: TBD)

    *   F.10.6.8 As funções trunc (p: TBD)

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.12.9.8 As funções trunc (p: TBD)

    *   7.25 Matemática genérica de tipo <tgmath.h> (p: TBD)

    *   F.10.6.8 As funções trunc (p: TBD)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.12.9.8 As funções trunc (p: 253-254)

    *   7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    *   F.10.6.8 As funções trunc (p: 528)

*   Padrão C99 (ISO/IEC 9899:1999):

    *   7.12.9.8 As funções trunc (p: 234)

    *   7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337)

    *   F.9.6.8 As funções trunc (p: 464)

### Veja também

[`floorfloorffloorl`](<#/doc/numeric/math/floor>)(C99)(C99) | calcula o maior inteiro não maior que o valor dado
(função)
[`ceilceilfceill`](<#/doc/numeric/math/ceil>)(C99)(C99) | calcula o menor inteiro não menor que o valor dado
(função)
[`roundroundfroundllroundlroundflroundlllroundllroundfllroundl`](<#/doc/numeric/math/round>)(C99)(C99)(C99)(C99)(C99)(C99)(C99)(C99)(C99) | arredonda para o inteiro mais próximo, arredondando para longe de zero em casos de meio termo
(função)
[documentação C++](<#/>) para trunc