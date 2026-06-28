# frexp, frexpf, frexpl

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float frexpf( float arg, int* exp );  // desde C99
double frexp( double arg, int* exp );
long double frexpl( long double arg, int* exp );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define frexp( arg, exp )  // desde C99
```

  
1-3) Decompõe o valor de ponto flutuante `x` fornecido em uma fração normalizada e uma potência integral de dois.

4) Macro genérica de tipo: Se `arg` tiver o tipo long double, `frexpl` é chamada. Caso contrário, se `arg` tiver um tipo inteiro ou o tipo double, `frexp` é chamada. Caso contrário, `frexpf` é chamada, respectivamente.

### Parâmetros

- **arg** — valor de ponto flutuante
- **exp** — ponteiro para o valor inteiro onde o expoente será armazenado

### Valor de retorno

Se `arg` for zero, retorna zero e armazena zero em `*exp`.

Caso contrário (se `arg` não for zero), se nenhum erro ocorrer, retorna o valor `x` no intervalo `(-1;-0.5], [0.5; 1)` e armazena um valor inteiro em *[exp](<#/doc/numeric/math/exp>) tal que x×2(*exp) =arg.

Se o valor a ser armazenado em `*exp` estiver fora do intervalo de int, o comportamento é não especificado.

Se `arg` não for um número de ponto flutuante, o comportamento é não especificado.

### Tratamento de erros

Esta função não está sujeita a nenhum erro especificado em `[`math_errhandling`](<#/doc/numeric/math/math_errhandling>)`.

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559),

  * Se `arg` for ±0, ele é retornado, inalterado, e `0` é armazenado em *[exp](<#/doc/numeric/math/exp>).
  * Se `arg` for ±∞, ele é retornado, e um valor não especificado é armazenado em *[exp](<#/doc/numeric/math/exp>).
  * Se `arg` for NaN, NaN é retornado, e um valor não especificado é armazenado em *[exp](<#/doc/numeric/math/exp>).
  * Nenhuma exceção de ponto flutuante é levantada.
  * Se `[`FLT_RADIX`](<#/doc/types/limits>)` for 2 (ou uma potência de 2), o valor retornado é exato, `[`o modo de arredondamento atual`](<#/doc/numeric/fenv/FE_round>)` é ignorado.

### Notas

Em um sistema binário (onde `[`FLT_RADIX`](<#/doc/types/limits>)` é 2), `frexp` pode ser implementada como
```c
    {
        *exp = (value == 0) ? 0 : (int)(1 + logb(value));
        return scalbn(value, -(*exp));
    }
```

A função `frexp`, juntamente com sua dual, `[`ldexp`](<#/doc/numeric/math/ldexp>)`, pode ser usada para manipular a representação de um número de ponto flutuante sem manipulações diretas de bits.

### Exemplo

Execute este código
```c
    #include <float.h>
    #include <math.h>
    #include <stdio.h>
     
    int main(void)
    {
        double f = 123.45;
        printf("Given the number %.2f or %a in hex,\n", f, f);
     
        double f3;
        double f2 = modf(f, &f3);
        printf("modf() makes %.0f + %.2f\n", f3, f2);
     
        int i;
        f2 = frexp(f, &i);
        printf("frexp() makes %f * 2^%d\n", f2, i);
     
        i = ilogb(f);
        printf("logb()/ilogb() make %f * %d^%d\n", f/scalbn(1.0, i), FLT_RADIX, i);
    }
```

Saída possível:
```
    Given the number 123.45 or 0x1.edccccccccccdp+6 in hex,
    modf() makes 123 + 0.45
    frexp() makes 0.964453 * 2^7
    logb()/ilogb() make 1.92891 * 2^6
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.12.6.4 As funções frexp (p: TBD)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: TBD)

    

  * F.10.3.4 As funções frexp (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.12.6.4 As funções frexp (p: TBD)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: TBD)

    

  * F.10.3.4 As funções frexp (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.12.6.4 As funções frexp (p: 243)

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375)

    

  * F.10.3.4 As funções frexp (p: 521)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.12.6.4 As funções frexp (p: 224)

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337)

    

  * F.9.3.4 As funções frexp (p: 458)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.5.4.2 A função frexp

### Veja também

[ ldexpldexpfldexpl](<#/doc/numeric/math/ldexp>)(C99)(C99) | multiplica um número por 2 elevado a uma potência
(função)
[ logblogbflogbl](<#/doc/numeric/math/logb>)(C99)(C99)(C99) | extrai o expoente do número fornecido
(função)
[ ilogbilogbfilogbl](<#/doc/numeric/math/ilogb>)(C99)(C99)(C99) | extrai o expoente do número fornecido
(função)
[ modfmodffmodfl](<#/doc/numeric/math/modf>)(C99)(C99) | divide um número em partes inteira e fracionária
(função)
[Documentação C++](<#/>) para frexp