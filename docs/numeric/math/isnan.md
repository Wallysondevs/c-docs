# isnan

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
#define isnan(arg) /* implementation defined */  // desde C99
```

Determina se o número de ponto flutuante `arg` é um valor not-a-number (NaN). A macro retorna um valor inteiro.

[FLT_EVAL_METHOD](<#/doc/types/limits/FLT_EVAL_METHOD>) é ignorado: mesmo que o argumento seja avaliado com mais faixa e precisão do que seu tipo, ele é primeiro convertido para seu tipo semântico, e a classificação é baseada nisso (isso importa se o tipo de avaliação suporta NaNs, enquanto o tipo semântico não).

### Parâmetros

- **arg** — valor de ponto flutuante

### Valor de retorno

Valor inteiro diferente de zero se `arg` for um NaN, ​0​ caso contrário.

### Notas

Existem muitos valores NaN diferentes com bits de sinal e payloads distintos, veja [nan](<#/doc/numeric/math/nan.2>).

Valores NaN nunca se comparam como iguais a si mesmos ou a outros valores NaN. Copiar um NaN pode alterar seu padrão de bits.

Outra forma de testar se um valor de ponto flutuante é NaN é compará-lo consigo mesmo: bool is_nan(double x) { return x != x; }

### Exemplo

Execute este código
```c
    #include <float.h>
    #include <math.h>
    #include <stdio.h>
     
    int main(void)
    {
        printf("isnan(NAN)         = %d\n", isnan(NAN));
        printf("isnan(INFINITY)    = %d\n", isnan(INFINITY));
        printf("isnan(0.0)         = %d\n", isnan(0.0));
        printf("isnan(DBL_MIN/2.0) = %d\n", isnan(DBL_MIN / 2.0));
        printf("isnan(0.0 / 0.0)   = %d\n", isnan(0.0 / 0.0));
        printf("isnan(Inf - Inf)   = %d\n", isnan(INFINITY - INFINITY));
    }
```

Saída possível:
```
    isnan(NAN)         = 1
    isnan(INFINITY)    = 0
    isnan(0.0)         = 0
    isnan(DBL_MIN/2.0) = 0
    isnan(0.0 / 0.0)   = 1
    isnan(Inf - Inf)   = 1
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.12.3.4 A macro isnan (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.12.3.4 A macro isnan (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.12.3.4 A macro isnan (p: 236-237)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.12.3.4 A macro isnan (p: 217)

### Veja também

[ nannanfnanl](<#/doc/numeric/math/nan.2>)(C99)(C99)(C99) | retorna um NaN (not-a-number)
(função)
[ fpclassify](<#/doc/numeric/math/fpclassify>)(C99) | classifica o valor de ponto flutuante fornecido
(macro de função)
[ isfinite](<#/doc/numeric/math/isfinite>)(C99) | verifica se o número fornecido tem valor finito
(macro de função)
[ isinf](<#/doc/numeric/math/isinf>)(C99) | verifica se o número fornecido é infinito
(macro de função)
[ isnormal](<#/doc/numeric/math/isnormal>)(C99) | verifica se o número fornecido é normal
(macro de função)
[ isunordered](<#/doc/numeric/math/isunordered>)(C99) | verifica se dois valores de ponto flutuante são não ordenados
(macro de função)
[Documentação C++](<#/>) para isnan