# fegetenv, fesetenv

Definido no cabeçalho [`<fenv.h>`](<#/doc/numeric/fenv>)

```c
int fegetenv( fenv_t* envp );  // desde C99
int fesetenv( const fenv_t* envp );  // desde C99
```

1) Tenta armazenar o status do ambiente de ponto flutuante no objeto apontado por `envp`.

2) Tenta estabelecer o ambiente de ponto flutuante a partir do objeto apontado por `envp`. O valor desse objeto deve ter sido obtido anteriormente por uma chamada a [feholdexcept](<#/doc/numeric/fenv/feholdexcept>) ou `fegetenv` ou ser uma macro constante de ponto flutuante. Se alguma das flags de status de ponto flutuante estiver definida em `envp`, elas se tornam definidas no ambiente (e podem então ser testadas com [fetestexcept](<#/doc/numeric/fenv/fetestexcept>)), mas as exceções de ponto flutuante correspondentes não são levantadas (a execução continua ininterrupta)

### Parâmetros

- **envp** — ponteiro para o objeto do tipo fenv_t que contém o status do ambiente de ponto flutuante

### Valor de retorno

​0​ em caso de sucesso, diferente de zero caso contrário.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <math.h>
    #include <fenv.h>
    
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
    
    void show_fe_rounding_method(void)
    {
        printf("current rounding method:    ");
        switch (fegetround()) {
               case FE_TONEAREST:  printf ("FE_TONEAREST");  break;
               case FE_DOWNWARD:   printf ("FE_DOWNWARD");   break;
               case FE_UPWARD:     printf ("FE_UPWARD");     break;
               case FE_TOWARDZERO: printf ("FE_TOWARDZERO"); break;
               default:            printf ("unknown");
        };
        printf("\n");
    }
    
    void show_fe_environment(void)
    {
        show_fe_exceptions();
        show_fe_rounding_method();
    }    
    
    int main(void)
    {
        fenv_t curr_env;
        int rtn;
    
        /* Show default environment. */
        show_fe_environment();
        printf("\n");
    
        /* Perform some computation under default environment. */
        printf("+11.5 -> %+4.1f\n", rint(+11.5)); /* midway between two integers */
        printf("+12.5 -> %+4.1f\n", rint(+12.5)); /* midway between two integers */
        show_fe_environment();
        printf("\n");
    
        /* Save current environment. */
        rtn = fegetenv(&curr_env);
    
        /* Perform some computation with new rounding method. */
        feclearexcept(FE_ALL_EXCEPT);
        fesetround(FE_DOWNWARD);
        printf("1.0/0.0 = %f\n", 1.0/0.0);
        printf("+11.5 -> %+4.1f\n", rint(+11.5));
        printf("+12.5 -> %+4.1f\n", rint(+12.5));
        show_fe_environment();
        printf("\n");
    
        /* Restore previous environment. */
        rtn = fesetenv(&curr_env);
        show_fe_environment();
    
        return 0;
    }
```

Saída:
```
    current exceptions raised: none
    current rounding method:   FE_TONEAREST
    
    +11.5 -> +12.0
    +12.5 -> +12.0
    current exceptions raised: FE_INEXACT
    current rounding method:   FE_TONEAREST
    
    1.0/0.0 = inf
    +11.5 -> +11.0
    +12.5 -> +12.0
    current exceptions raised: FE_DIVBYZERO FE_INEXACT
    current rounding method:   FE_DOWNWARD
    
    current exceptions raised: FE_INEXACT
    current rounding method:   FE_TONEAREST
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.6.4.1 A função fegetenv (p: 213)

    

  * 7.6.4.3 A função fesetenv (p: 214)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.6.4.1 A função fegetenv (p: 194)

    

  * 7.6.4.3 A função fesetenv (p: 195)

### Veja também

[ feholdexcept](<#/doc/numeric/fenv/feholdexcept>)(C99) | salva o ambiente, limpa todas as flags de status e ignora todos os erros futuros
(função)
[ feupdateenv](<#/doc/numeric/fenv/feupdateenv>)(C99) | restaura o ambiente de ponto flutuante e levanta as exceções previamente levantadas
(função)
[ FE_DFL_ENV](<#/doc/numeric/fenv/FE_DFL_ENV>)(C99) | ambiente de ponto flutuante padrão
(macro constante)
[Documentação C++](<#/>) para fegetenv, fesetenv