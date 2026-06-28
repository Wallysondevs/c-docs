# FE_DFL_ENV

Definido no cabeçalho [`<fenv.h>`](<#/doc/numeric/fenv>)

```c
#define FE_DFL_ENV /*implementation defined*/  // desde C99
```

A macro constante **FE_DFL_ENV** se expande para uma expressão do tipo const fenv_t*, que aponta para uma cópia completa do ambiente de ponto flutuante padrão, ou seja, o ambiente como carregado na inicialização do programa.

Macros adicionais que começam com `FE_` seguidas por letras maiúsculas, e que possuem o tipo const fenv_t*, podem ser suportadas por uma implementação.

### Exemplo

Execute este código
```c
    #include <stdio.h>
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
    
    int main()
    {
        printf("On startup:\n");
        show_fe_environment();
    
        // Change environment
        fesetround(FE_DOWNWARD);     // change rounding mode
        feraiseexcept(FE_INVALID);   // raise exception
        printf("\nBefore restoration:\n");
        show_fe_environment();
    
        fesetenv(FE_DFL_ENV);    // restore
        printf("\nAfter restoring default environment:\n");
        show_fe_environment();
    }
```

Saída:
```
    On startup:
    current exceptions raised:  none
    current rounding method:    FE_TONEAREST
    
    Before restoration:
    current exceptions raised:  FE_INVALID
    current rounding method:    FE_DOWNWARD
    
    After restoring default environment:
    current exceptions raised:  none
    current rounding method:    FE_TONEAREST
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.6/9 Ambiente de ponto flutuante <fenv.h> (p: 208) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.6/8 Ambiente de ponto flutuante <fenv.h> (p: 188-189) 

### Veja também

[ fegetenvfesetenv](<#/doc/numeric/fenv/feenv>)(C99) | salva ou restaura o ambiente de ponto flutuante atual
(função)
[ feupdateenv](<#/doc/numeric/fenv/feupdateenv>)(C99) | restaura o ambiente de ponto flutuante e levanta as exceções previamente levantadas
(função)
[documentação C++](<#/>) para FE_DFL_ENV