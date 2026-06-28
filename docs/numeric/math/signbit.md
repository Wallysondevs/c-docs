# signbit

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
#define signbit( arg ) /* implementation defined */  // desde C99
```

Determina se o número de ponto flutuante fornecido arg é negativo. A macro retorna um valor inteiro.

### Parâmetros

- **arg** — valor de ponto flutuante

### Valor de retorno

Valor inteiro diferente de zero se arg for negativo, ​0​ caso contrário.

### Notas

Esta macro detecta o bit de sinal de zeros, infinitos e NaNs. Juntamente com [copysign](<#/doc/numeric/math/copysign>), esta macro é uma das únicas duas maneiras portáteis de examinar o sinal de um NaN.

### Exemplo

Execute este código
```c
    #include <math.h>
    #include <stdio.h>
    
    int main(void)
    {
        printf("signbit(+0.0) = %d\n", signbit(+0.0));
        printf("signbit(-0.0) = %d\n", signbit(-0.0));
    }
```

Saída possível:
```
    signbit(+0.0) = 0
    signbit(-0.0) = 128
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.12.3.6 A macro signbit (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.12.3.6 A macro signbit (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.12.3.6 A macro signbit (p: 237)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.12.3.6 A macro signbit (p: 218)

### Veja também

[ fabsfabsffabsl](<#/doc/numeric/math/fabs>)(C99)(C99) | calcula o valor absoluto de um valor de ponto flutuante (\\(\small{|x|}\\)|x|)
(função)
[ copysigncopysignfcopysignl](<#/doc/numeric/math/copysign>)(C99)(C99)(C99) | produz um valor com a magnitude de um dado valor e o sinal de outro dado valor
(função)
[Documentação C++](<#/>) para signbit