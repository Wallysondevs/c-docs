# FE_DIVBYZERO, FE_INEXACT, FE_INVALID, FE_OVERFLOW, FE_UNDERFLOW, FE_ALL_EXCEPT

Definido no cabeçalho [`<fenv.h>`](<../fenv.html> "c/numeric/fenv")

```c
#define FE_DIVBYZERO /*potência de 2 definida pela implementação*/  // desde C99
#define FE_INEXACT /*potência de 2 definida pela implementação*/  // desde C99
#define FE_INVALID /*potência de 2 definida pela implementação*/  // desde C99
#define FE_OVERFLOW /*potência de 2 definida pela implementação*/  // desde C99
#define FE_UNDERFLOW /*potência de 2 definida pela implementação*/  // desde C99
#define FE_ALL_EXCEPT FE_DIVBYZERO
FE_INVALID
FE_UNDERFLOW  // desde C99
```

Todas essas constantes de macro (exceto **FE_ALL_EXCEPT**) se expandem para expressões constantes inteiras que são potências distintas de 2, as quais identificam unicamente todas as exceções de ponto flutuante suportadas. Cada macro é definida apenas se for suportada.

A constante de macro **FE_ALL_EXCEPT**, que se expande para o OR bit a bit de todas as outras `FE_*`, é sempre definida e é zero se as exceções de ponto flutuante não forem suportadas pela implementação.

Constante | Explicação
`FE_DIVBYZERO` | ocorreu um erro de polo em uma operação de ponto flutuante anterior
`FE_INEXACT` | resultado inexato: arredondamento foi necessário para armazenar o resultado de uma operação de ponto flutuante anterior
`FE_INVALID` | ocorreu um erro de domínio em uma operação de ponto flutuante anterior
`FE_OVERFLOW` | o resultado de uma operação de ponto flutuante anterior era muito grande para ser representável
`FE_UNDERFLOW` | o resultado de uma operação de ponto flutuante anterior era subnormal com perda de precisão
`FE_ALL_EXCEPT` | OR bit a bit de todas as exceções de ponto flutuante suportadas

A implementação pode definir constantes de macro adicionais em `<fenv.h>` para identificar exceções de ponto flutuante adicionais. Todas essas constantes começam com `FE_` seguidas por pelo menos uma letra maiúscula.

Consulte [math_errhandling](<../math/math_errhandling.html> "c/numeric/math/math errhandling")` para mais detalhes.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <math.h>
    #include <float.h>
    #include <fenv.h>
    
    #pragma STDC FENV_ACCESS ON
    void show_fe_exceptions(void)
    {
        printf("exceptions raised:");
        if(fetestexcept(FE_DIVBYZERO)) printf(" FE_DIVBYZERO");
        if(fetestexcept(FE_INEXACT))   printf(" FE_INEXACT");
        if(fetestexcept(FE_INVALID))   printf(" FE_INVALID");
        if(fetestexcept(FE_OVERFLOW))  printf(" FE_OVERFLOW");
        if(fetestexcept(FE_UNDERFLOW)) printf(" FE_UNDERFLOW");
        feclearexcept(FE_ALL_EXCEPT);
        printf("\n");
    }
    
    int main(void)
    {
        printf("MATH_ERREXCEPT is %s\n",
               math_errhandling & MATH_ERREXCEPT ? "set" : "not set");
    
        printf("0.0/0.0 = %f\n", 0.0/0.0);
        show_fe_exceptions();
    
        printf("1.0/0.0 = %f\n", 1.0/0.0);
        show_fe_exceptions();
    
        printf("1.0/10.0 = %f\n", 1.0/10.0);
        show_fe_exceptions();
    
        printf("sqrt(-1) = %f\n", sqrt(-1));
        show_fe_exceptions();
    
        printf("DBL_MAX*2.0 = %f\n", DBL_MAX*2.0);
        show_fe_exceptions();
    
        printf("nextafter(DBL_MIN/pow(2.0,52),0.0) = %.1f\n",
                          nextafter(DBL_MIN/pow(2.0,52),0.0));
        show_fe_exceptions();
    }
```

Saída possível:
```
    MATH_ERREXCEPT is set
    0.0/0.0 = nan
    exceptions raised: FE_INVALID
    1.0/0.0 = inf
    exceptions raised: FE_DIVBYZERO
    1.0/10.0 = 0.100000
    exceptions raised: FE_INEXACT
    sqrt(-1) = -nan
    exceptions raised: FE_INVALID
    DBL_MAX*2.0 = inf
    exceptions raised: FE_INEXACT FE_OVERFLOW
    nextafter(DBL_MIN/pow(2.0,52),0.0) = 0.0
    exceptions raised: FE_INEXACT FE_UNDERFLOW
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.6/6 Ambiente de ponto flutuante <fenv.h> (p: 207)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.6/5 Ambiente de ponto flutuante <fenv.h> (p: 188)

### Veja também

`math_errhandling` / `MATH_ERRNO` / `MATH_ERREXCEPT` (C99) | define o mecanismo de tratamento de erros usado pelas funções matemáticas comuns
(constante de macro)
[documentação C++](<../../../cpp/numeric/fenv/FE_exceptions.html> "cpp/numeric/fenv/FE exceptions")` para macros de exceção de ponto flutuante