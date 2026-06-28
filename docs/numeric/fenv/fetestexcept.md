# fetestexcept

Definido no cabeçalho [`<fenv.h>`](<#/doc/numeric/fenv>)

```c
int fetestexcept( int excepts );  // desde C99
```

Determina quais do subconjunto especificado de exceções de ponto flutuante estão atualmente ativadas. O argumento `excepts` é um OR bit a bit das [macros de exceção de ponto flutuante](<#/doc/numeric/fenv/FE_exceptions>).

### Parâmetros

- **excepts** — máscara de bits listando os sinalizadores de exceção a serem testados

### Valor de retorno

OR bit a bit das macros de exceção de ponto flutuante que estão incluídas em `excepts` e correspondem às exceções de ponto flutuante atualmente ativadas.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <math.h>
    #include <fenv.h>
    #include <float.h>
    
    #pragma STDC FENV_ACCESS ON
    
    void show_fe_exceptions(void)
    {
        printf("current exceptions raised: ");
        if(fetestexcept(FE_DIVBYZERO))     printf(" FE_DIVBYZERO");
        if(fetestexcept(FE_INEXACT))       printf(" FE_INEXACT");
        if(fetestexcept(FE_INVALID))       printf(" FE_INVALID");
        if(fetestexcept(FE_OVERFLOW))      printf(" FE_OVERFLOW");
        if(fetestexcept(FE_UNDERFLOW))     printf(" FE_UNDERFLOW");
        if(fetestexcept(FE_ALL_EXCEPT)==0) printf(" none");
        printf("\n");
    }
    
    int main(void)
    {
        /* Show default set of exception flags. */
        show_fe_exceptions();
    
        /* Perform some computations which raise exceptions. */
        printf("1.0/0.0     = %f\n", 1.0/0.0);        /* FE_DIVBYZERO            */
        printf("1.0/10.0    = %f\n", 1.0/10.0);       /* FE_INEXACT              */
        printf("sqrt(-1)    = %f\n", sqrt(-1));       /* FE_INVALID              */
        printf("DBL_MAX*2.0 = %f\n", DBL_MAX*2.0);    /* FE_INEXACT FE_OVERFLOW  */
        printf("nextafter(DBL_MIN/pow(2.0,52),0.0) = %.1f\n",
               nextafter(DBL_MIN/pow(2.0,52),0.0));   /* FE_INEXACT FE_UNDERFLOW */
        show_fe_exceptions();
    
        return 0;
    }
```

Saída:
```
    current exceptions raised:  none
    1.0/0.0     = inf
    1.0/10.0    = 0.100000
    sqrt(-1)    = -nan
    DBL_MAX*2.0 = inf
    nextafter(DBL_MIN/pow(2.0,52),0.0) = 0.0
    current exceptions raised:  FE_DIVBYZERO FE_INEXACT FE_INVALID FE_OVERFLOW FE_UNDERFLOW
```

### Referências

*   Padrão C11 (ISO/IEC 9899:2011):
    *   7.6.2.5 A função fetestexcept (p: 211-212)
*   Padrão C99 (ISO/IEC 9899:1999):
    *   7.6.2.5 A função fetestexcept (p: 192-193)

### Veja também

[ feclearexcept](<#/doc/numeric/fenv/feclearexcept>)(C99) | limpa os sinalizadores de status de ponto flutuante especificados
(função)
[Documentação C++](<#/>) para fetestexcept