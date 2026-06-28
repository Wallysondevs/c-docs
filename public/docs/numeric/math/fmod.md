# fmod, fmodf, fmodl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float fmodf( float x, float y );  // desde C99
double fmod( double x, double y );
long double fmodl( long double x, long double y );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define fmod( x, y )  // desde C99
```

1-3) Calcula o resto de ponto flutuante da operação de divisão x / y.

4) Macro genérica de tipo: Se qualquer argumento tiver o tipo long double, `fmodl` é chamada. Caso contrário, se qualquer argumento tiver tipo inteiro ou tipo double, `fmod` é chamada. Caso contrário, `fmodf` é chamada.

O resto de ponto flutuante da operação de divisão x / y calculado por esta função é exatamente o valor x - n * y, onde `n` é x / y com sua parte fracionária truncada.

O valor retornado tem o mesmo sinal que x e é menor ou igual a y em magnitude.

### Parâmetros

- **x, y** — valores de ponto flutuante

### Valor de retorno

Em caso de sucesso, retorna o resto de ponto flutuante da divisão x / y conforme definido acima.

Se ocorrer um erro de domínio, um valor definido pela implementação é retornado (NaN onde suportado).

Se ocorrer um erro de faixa devido a underflow, o resultado correto (após arredondamento) é retornado.

### Tratamento de erros

Os erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).

Um erro de domínio pode ocorrer se y for zero.

Se a implementação suporta aritmética de ponto flutuante IEEE (IEC 60559):

  * Se x for ±0 e y não for zero, ±0 é retornado.
  * Se x for ±∞ e y não for NaN, NaN é retornado e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado.
  * Se y for ±0 e x não for NaN, NaN é retornado e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado.
  * Se y for ±∞ e x for finito, x é retornado.
  * Se qualquer um dos argumentos for NaN, NaN é retornado.

### Notas

[POSIX exige](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/fmod.html>) que um erro de domínio ocorra se x for infinito ou y for zero.

`fmod`, mas não [remainder](<#/doc/numeric/math/remainder>), é útil para fazer o encapsulamento silencioso de tipos de ponto flutuante para tipos inteiros sem sinal: (0.0 <= (y = fmod([rint](<#/doc/numeric/math/rint>)(x), 65536.0 )) ? y : 65536.0 + y) está no intervalo `[`-0.0`, `65535.0`]`, que corresponde a unsigned short, mas [remainder](<#/doc/numeric/math/remainder>)([rint](<#/doc/numeric/math/rint>)(x), 65536.0) está no intervalo `[`-32767.0`, `+32768.0`]`, que está fora do intervalo de signed short.

A versão double de `fmod` se comporta como se fosse implementada da seguinte forma:
```c
    double fmod(double x, double y)
    {
    #pragma STDC FENV_ACCESS ON
        double result = remainder(fabs(x), (y = fabs(y)));
        if (signbit(result))
            result += y;
        return copysign(result, x);
    }
```

### Exemplo

Execute este código
```c
    #include <fenv.h>
    #include <math.h>
    #include <stdio.h>
    
    // #pragma STDC FENV_ACCESS ON
    
    int main(void)
    {
        printf("fmod(+5.1, +3.0) = %.1f\n", fmod(5.1, 3));
        printf("fmod(-5.1, +3.0) = %.1f\n", fmod(-5.1, 3));
        printf("fmod(+5.1, -3.0) = %.1f\n", fmod(5.1, -3));
        printf("fmod(-5.1, -3.0) = %.1f\n", fmod(-5.1, -3));
    
        // special values
        printf("fmod(+0.0, 1.0) = %.1f\n", fmod(0, 1));
        printf("fmod(-0.0, 1.0) = %.1f\n", fmod(-0.0, 1));
        printf("fmod(+5.1, Inf) = %.1f\n", fmod(5.1, INFINITY));
    
        // error handling
        feclearexcept(FE_ALL_EXCEPT);
        printf("fmod(+5.1, 0) = %.1f\n", fmod(5.1, 0));
        if (fetestexcept(FE_INVALID))
            puts("    FE_INVALID raised");
    }
```

Saída possível:
```
    fmod(+5.1, +3.0) = 2.1
    fmod(-5.1, +3.0) = -2.1
    fmod(+5.1, -3.0) = 2.1
    fmod(-5.1, -3.0) = -2.1
    fmod(+0.0, 1.0) = 0.0
    fmod(-0.0, 1.0) = -0.0
    fmod(+5.1, Inf) = 5.1
    fmod(+5.1, 0) = nan
        FE_INVALID raised
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.12.10.1 As funções fmod (p: TBD)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: TBD)

    

  * F.10.7.1 As funções fmod (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.12.10.1 As funções fmod (p: 185)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 274-275)

    

  * F.10.7.1 As funções fmod (p: 385)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.12.10.1 As funções fmod (p: 254)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    

  * F.10.7.1 As funções fmod (p: 528)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.12.10.1 As funções fmod (p: 235)

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337)

    

  * F.9.7.1 As funções fmod (p: 465)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.5.6.4 A função fmod

### Veja também

[ divldivlldiv](<#/doc/numeric/math/div>)(C99) | calcula quociente e resto da divisão inteira
(função)
[ remainderremainderfremainderl](<#/doc/numeric/math/remainder>)(C99)(C99)(C99) | calcula o resto com sinal da operação de divisão de ponto flutuante
(função)
[ remquoremquofremquol](<#/doc/numeric/math/remquo>)(C99)(C99)(C99) | calcula o resto com sinal, bem como os três últimos bits da operação de divisão
(função)
[Documentação C++](<#/>) para fmod