# remainder, remainderf, remainderl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float remainderf( float x, float y );  // desde C99
double remainder( double x, double y );  // desde C99
long double remainderl( long double x, long double y );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define remainder( x, y )  // desde C99
```

1-3) Calcula o resto IEEE da operação de divisão de ponto flutuante x/y.

4) Macro genérica de tipo: Se qualquer argumento tiver o tipo long double, `remainderl` é chamada. Caso contrário, se qualquer argumento tiver um tipo inteiro ou o tipo double, `remainder` é chamada. Caso contrário, `remainderf` é chamada.

O resto IEEE de ponto flutuante da operação de divisão x/y calculado por esta função é exatamente o valor x - n * y, onde o valor `n` é o valor inteiro mais próximo do valor exato x/y. Quando |n-x/y| = ½, o valor `n` é escolhido para ser par.

Em contraste com [fmod()](<#/doc/numeric/math/fmod>), o valor retornado não é garantido ter o mesmo sinal que x.

Se o valor retornado for ​0​, ele terá o mesmo sinal que x.

### Parâmetros

- **x, y** — valores de ponto flutuante

### Valor de retorno

Se bem-sucedido, retorna o resto IEEE de ponto flutuante da divisão x/y conforme definido acima.

Se ocorrer um erro de domínio, um valor definido pela implementação é retornado (NaN onde suportado).

Se ocorrer um erro de intervalo devido a underflow, o resultado correto é retornado.

Se y for zero, mas o erro de domínio não ocorrer, zero é retornado.

### Tratamento de erros

Os erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Um erro de domínio pode ocorrer se y for zero.

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559),

  * O [modo de arredondamento](<#/doc/numeric/fenv/FE_round>) atual não tem efeito.
  * [FE_INEXACT](<#/doc/numeric/fenv/FE_exceptions>) nunca é levantado, o resultado é sempre exato.
  * Se x for ±∞ e y não for NaN, NaN é retornado e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado.
  * Se y for ±0 e x não for NaN, NaN é retornado e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado.
  * Se qualquer um dos argumentos for NaN, NaN é retornado.

### Notas

[POSIX exige](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/remainder.html>) que um erro de domínio ocorra se x for infinito ou y for zero.

[fmod](<#/doc/numeric/math/fmod>), mas não `remainder`, é útil para fazer o "wrapping" silencioso de tipos de ponto flutuante para tipos inteiros sem sinal: (0.0 <= (y = [fmod](<#/doc/numeric/math/fmod>)([rint](<#/doc/numeric/math/rint>)(x), 65536.0)) ? y : 65536.0 + y) está no intervalo `[`-0.0`, `65535.0`]`, que corresponde a unsigned short, mas remainder([rint](<#/doc/numeric/math/rint>)(x), 65536.0) está no intervalo `[`-32767.0`, `+32768.0`]`, que está fora do intervalo de signed short.

### Exemplo

Execute este código
```c
    #include <fenv.h>
    #include <math.h>
    #include <stdio.h>
    // #pragma STDC FENV_ACCESS ON
     
    int main(void)
    {
        printf("remainder(+5.1, +3.0) = %.1f\n", remainder(5.1, 3));
        printf("remainder(-5.1, +3.0) = %.1f\n", remainder(-5.1, 3));
        printf("remainder(+5.1, -3.0) = %.1f\n", remainder(5.1, -3));
        printf("remainder(-5.1, -3.0) = %.1f\n", remainder(-5.1, -3));
     
        // special values
        printf("remainder(-0.0, 1.0) = %.1f\n", remainder(-0.0, 1));
        printf("remainder(+5.1, Inf) = %.1f\n", remainder(5.1, INFINITY));
     
        // error handling
        feclearexcept(FE_ALL_EXCEPT);
        printf("remainder(+5.1, 0) = %.1f\n", remainder(5.1, 0));
        if (fetestexcept(FE_INVALID))
            puts("    FE_INVALID raised");
    }
```

Saída:
```
    remainder(+5.1, +3.0) = -0.9
    remainder(-5.1, +3.0) = 0.9
    remainder(+5.1, -3.0) = -0.9
    remainder(-5.1, -3.0) = 0.9
    remainder(+0.0, 1.0) = 0.0
    remainder(-0.0, 1.0) = -0.0
    remainder(+5.1, Inf) = 5.1
    remainder(+5.1, 0) = -nan
        FE_INVALID raised
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.12.10.2 As funções remainder (p: TBD)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: TBD)

    

  * F.10.7.2 As funções remainder (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.12.10.2 As funções remainder (p: 185-186)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 272-273)

    

  * F.10.7.2 As funções remainder (p: 385)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.12.10.2 As funções remainder (p: 254-255)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    

  * F.10.7.2 As funções remainder (p: 529)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.12.10.2 As funções remainder (p: 235)

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337)

    

  * F.9.7.2 As funções remainder (p: 465)

### Veja também

[ divldivlldiv](<#/doc/numeric/math/div>)(C99) | calcula quociente e resto da divisão inteira
(função)
[ fmodfmodffmodl](<#/doc/numeric/math/fmod>)(C99)(C99) | calcula o resto da operação de divisão de ponto flutuante
(função)
[ remquoremquofremquol](<#/doc/numeric/math/remquo>)(C99)(C99)(C99) | calcula o resto com sinal, bem como os três últimos bits da operação de divisão
(função)
[Documentação C++](<#/>) para remainder