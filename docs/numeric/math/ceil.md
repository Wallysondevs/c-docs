# ceil, ceilf, ceill

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float ceilf( float arg );  // desde C99
double ceil( double arg );
long double ceill( long double arg );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define ceil( arg )  // desde C99
```

1-3) Calcula o menor valor inteiro não menor que arg.

4) Macro genérica de tipo: Se arg tiver o tipo long double, `ceill` é chamada. Caso contrário, se arg tiver um tipo inteiro ou o tipo double, `ceil` é chamada. Caso contrário, `ceilf` é chamada.

### Parâmetros

- **arg** — valor de ponto flutuante

### Valor de retorno

Se nenhum erro ocorrer, o menor valor inteiro não menor que arg, ou seja ⌈arg⌉, é retornado.

Valor de retorno

Argumento

### Tratamento de erros

Os erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Se a implementação suporta aritmética de ponto flutuante IEEE (IEC 60559):

*   O [modo de arredondamento](<#/doc/numeric/fenv/FE_round>) atual não tem efeito.
*   Se arg for ±∞, ele é retornado, inalterado.
*   Se arg for ±0, ele é retornado, inalterado.
*   Se arg for NaN, NaN é retornado.

### Observações

[FE_INEXACT](<#/doc/numeric/fenv/FE_exceptions>) pode ser (mas não é obrigatório ser) levantado ao arredondar um valor finito não inteiro.

Os maiores valores de ponto flutuante representáveis são inteiros exatos em todos os formatos de ponto flutuante padrão, então esta função nunca transborda por si só; no entanto, o resultado pode transbordar qualquer tipo inteiro (incluindo [intmax_t](<#/doc/types/integer>)), quando armazenado em uma variável inteira.

Esta função (para argumento double) se comporta como se (exceto pela liberdade de não levantar [FE_INEXACT](<#/doc/numeric/fenv/FE_exceptions>)) implementada por
```c
    #include <fenv.h>
    #include <math.h>
    #pragma STDC FENV_ACCESS ON
    
    double ceil(double x)
    {
        double result;
        int save_round = fegetround();
        fesetround(FE_UPWARD);
        result = rint(x); // or nearbyint
        fesetround(save_round);
        return result;
    }
```

### Exemplo

Execute este código
```c
    #include <math.h>
    #include <stdio.h>
    
    int main(void)
    {
        printf("ceil(+2.4) = %+.1f\n", ceil(2.4));
        printf("ceil(-2.4) = %+.1f\n", ceil(-2.4));
        printf("ceil(-0.0) = %+.1f\n", ceil(-0.0));
        printf("ceil(-Inf) = %+f\n",   ceil(-INFINITY));
    }
```

Saída possível:
```
    ceil(+2.4) = +3.0
    ceil(-2.4) = -2.0
    ceil(-0.0) = -0.0
    ceil(-Inf) = -inf
```

### Referências

*   Padrão C23 (ISO/IEC 9899:2024):

    *   7.12.9.1 As funções ceil (p: TBD)

    *   7.25 Matemática genérica de tipo <tgmath.h> (p: TBD)

    *   F.10.6.1 As funções ceil (p: TBD)

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.12.9.1 As funções ceil (p: TBD)

    *   7.25 Matemática genérica de tipo <tgmath.h> (p: TBD)

    *   F.10.6.1 As funções ceil (p: TBD)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.12.9.1 As funções ceil (p: 251)

    *   7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    *   F.10.6.1 As funções ceil (p: 526)

*   Padrão C99 (ISO/IEC 9899:1999):

    *   7.12.9.1 As funções ceil (p: 231-232)

    *   7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337)

    *   F.9.6.1 As funções ceil (p: 462-463)

*   Padrão C89/C90 (ISO/IEC 9899:1990):

    *   4.5.6.1 A função ceil

### Veja também

[ floorfloorffloorl](<#/doc/numeric/math/floor>)(C99)(C99) | calcula o maior inteiro não maior que o valor dado
(função) |
[ trunctruncftruncl](<#/doc/numeric/math/trunc>)(C99)(C99)(C99) | arredonda para o inteiro mais próximo não maior em magnitude que o valor dado
(função) |
[ roundroundfroundllroundlroundflroundlllroundllroundfllroundl](<#/doc/numeric/math/round>)(C99)(C99)(C99)(C99)(C99)(C99)(C99)(C99)(C99) | arredonda para o inteiro mais próximo, arredondando para longe de zero em casos de meio termo
(função) |
[ nearbyintnearbyintfnearbyintl](<#/doc/numeric/math/nearbyint>)(C99)(C99)(C99) | arredonda para um inteiro usando o modo de arredondamento atual
(função) |
[ rintrintfrintllrintlrintflrintlllrintllrintfllrintl](<#/doc/numeric/math/rint>)(C99)(C99)(C99)(C99)(C99)(C99)(C99)(C99)(C99) | arredonda para um inteiro usando o modo de arredondamento atual com exceção se o resultado for diferente
(função) |
[Documentação C++](<#/>) para ceil