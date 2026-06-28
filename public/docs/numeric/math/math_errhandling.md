# MATH_ERRNO, MATH_ERREXCEPT, math_errhandling

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
#define MATH_ERRNO 1  // desde C99
#define MATH_ERREXCEPT 2  // desde C99
#define math_errhandling /*implementation defined*/  // desde C99
```

A constante de macro `math_errhandling` se expande para uma expressão do tipo int que é igual a `MATH_ERRNO`, ou igual a `MATH_ERREXCEPT`, ou igual ao seu OR bit a bit (MATH_ERRNO | MATH_ERREXCEPT).

O valor de `math_errhandling` indica o tipo de tratamento de erro que é realizado pelos operadores de ponto flutuante e [funções](<#/doc/numeric/math>):

Constante | Explicação
`MATH_ERREXCEPT` | indica que exceções de ponto flutuante são usadas: pelo menos [FE_DIVBYZERO](<#/doc/numeric/fenv/FE_exceptions>), [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>), e [FE_OVERFLOW](<#/doc/numeric/fenv/FE_exceptions>) são definidas em `<fenv.h>`.
`MATH_ERRNO` | indica que operações de ponto flutuante usam a variável [errno](<#/doc/error/errno>) para reportar erros.

Se a implementação suporta aritmética de ponto flutuante IEEE (IEC 60559), math_errhandling & MATH_ERREXCEPT é requerido ser diferente de zero.

As seguintes condições de erro de ponto flutuante são reconhecidas:

Condição | Explicação | errno | exceção de ponto flutuante | Exemplo
Erro de domínio | o argumento está fora do intervalo no qual a operação é matematicamente definida (a descrição de [cada função](<#/doc/numeric/math>) lista os erros de domínio requeridos) | [EDOM](<#/doc/error/errno_macros>) | [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) | [acos](<#/doc/numeric/math/acos>)(2)
Erro de polo | o resultado matemático da função é exatamente infinito ou indefinido | [ERANGE](<#/doc/error/errno_macros>) | [FE_DIVBYZERO](<#/doc/numeric/fenv/FE_exceptions>) | [log](<#/doc/numeric/math/log>)(0.0), 1.0/0.0
Erro de faixa devido a estouro | o resultado matemático é finito, mas se torna infinito após o arredondamento, ou se torna o maior valor finito representável após o arredondamento para baixo | [ERANGE](<#/doc/error/errno_macros>) | [FE_OVERFLOW](<#/doc/numeric/fenv/FE_exceptions>) | [pow](<#/doc/numeric/math/pow>)([DBL_MAX](<#/doc/types/limits>),2)
Erro de faixa devido a subfluxo | o resultado é diferente de zero, mas se torna zero após o arredondamento, ou se torna subnormal com perda de precisão | [ERANGE](<#/doc/error/errno_macros>) ou inalterado (definido pela implementação) | [FE_UNDERFLOW](<#/doc/numeric/fenv/FE_exceptions>) ou nada (definido pela implementação) | DBL_TRUE_MIN/2
Resultado inexato | o resultado precisa ser arredondado para caber no tipo de destino | inalterado | [FE_INEXACT](<#/doc/numeric/fenv/FE_exceptions>) ou nada (não especificado) | [sqrt](<#/doc/numeric/math/sqrt>)(2), 1.0/10.0

### Notas

Se [FE_INEXACT](<#/doc/numeric/fenv/FE_exceptions>) é levantado pelas funções da biblioteca matemática é não especificado em geral, mas pode ser explicitamente especificado na descrição da função (por exemplo, [rint](<#/doc/numeric/math/rint>) vs [nearbyint](<#/doc/numeric/math/nearbyint>)).

Antes do C99, exceções de ponto flutuante não eram especificadas, [EDOM](<#/doc/error/errno_macros>) era requerido para qualquer erro de domínio, [ERANGE](<#/doc/error/errno_macros>) era requerido para estouros e definido pela implementação para subfluxos.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <fenv.h>
    #include <math.h>
    #include <errno.h>
    #pragma STDC FENV_ACCESS ON
    int main(void)
    {
        printf("MATH_ERRNO is %s\n", math_errhandling & MATH_ERRNO ? "set" : "not set");
        printf("MATH_ERREXCEPT is %s\n",
               math_errhandling & MATH_ERREXCEPT ? "set" : "not set");
        feclearexcept(FE_ALL_EXCEPT);
        errno = 0;
        printf("log(0) = %f\n", log(0));
        if(errno == ERANGE)
            perror("errno == ERANGE");
        if(fetestexcept(FE_DIVBYZERO))
            puts("FE_DIVBYZERO (pole error) reported");
    }
```

Saída possível:
```
    MATH_ERRNO is set
    MATH_ERREXCEPT is set
    log(0) = -inf
    errno = ERANGE: Numerical result out of range
    FE_DIVBYZERO (pole error) reported
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.12/9 MATH_ERRNO, MATH_ERREXCEPT, math_errhandling (p: 170)

    

  * F.10/4 MATH_ERREXCEPT, math_errhandling (p: 377)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.12/9 MATH_ERRNO, MATH_ERREXCEPT, math_errhandling (p: 233)

    

  * F.10/4 MATH_ERREXCEPT, math_errhandling (p: 517)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.12/9 MATH_ERRNO, MATH_ERREXCEPT, math_errhandling (p: 214)

    

  * F.9/4 MATH_ERREXCEPT, math_errhandling> (p: 454)

### Veja também

[ FE_ALL_EXCEPTFE_DIVBYZEROFE_INEXACTFE_INVALIDFE_OVERFLOWFE_UNDERFLOW](<#/doc/numeric/fenv/FE_exceptions>)(C99) | exceções de ponto flutuante
(constante de macro)
[ errno](<#/doc/error/errno>) | macro que se expande para uma variável de número de erro thread-local compatível com POSIX
(variável de macro)
[Documentação C++](<#/>) para math_errhandling