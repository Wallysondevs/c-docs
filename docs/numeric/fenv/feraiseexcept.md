# feraiseexcept

Definido no cabeçalho [`<fenv.h>`](<#/doc/numeric/fenv>)

```c
int feraiseexcept( int excepts );  // desde C99
```

Tenta levantar todas as exceções de ponto flutuante listadas em `excepts` (um OR bit a bit das [macros de exceção de ponto flutuante](<#/doc/numeric/fenv/FE_exceptions>)). Se uma das exceções for [FE_OVERFLOW](<#/doc/numeric/fenv/FE_exceptions>) ou [FE_UNDERFLOW](<#/doc/numeric/fenv/FE_exceptions>), esta função pode adicionalmente levantar [FE_INEXACT](<#/doc/numeric/fenv/FE_exceptions>). A ordem em que as exceções são levantadas é não especificada, exceto que [FE_OVERFLOW](<#/doc/numeric/fenv/FE_exceptions>) e [FE_UNDERFLOW](<#/doc/numeric/fenv/FE_exceptions>) são sempre levantadas antes de [FE_INEXACT](<#/doc/numeric/fenv/FE_exceptions>).

### Parâmetros

- **excepts** — máscara de bits listando os sinalizadores de exceção a serem levantados

### Valor de retorno

​0​ se todas as exceções listadas foram levantadas, valor diferente de zero caso contrário.

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
        feclearexcept(FE_ALL_EXCEPT);
        printf("\n");
    }
    
    double some_computation(void)
    {
        /* Computation reaches a state that causes overflow. */
        int r = feraiseexcept(FE_OVERFLOW | FE_INEXACT);
        printf("feraiseexcept() %s\n", (r?"fails":"succeeds"));
        return 0.0;
    }
    
    int main(void)
    {
        some_computation();
        show_fe_exceptions();
    
        return 0;
    }
```

Saída:
```
    feraiseexcept() succeeds
    current exceptions raised:  FE_INEXACT FE_OVERFLOW
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.6.2.3 A função feraiseexcept (p: 210)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.6.2.3 A função feraiseexcept (p: 191)

### Veja também

[ feclearexcept](<#/doc/numeric/fenv/feclearexcept>)(C99) | limpa os sinalizadores de status de ponto flutuante especificados
(função)
[ fetestexcept](<#/doc/numeric/fenv/fetestexcept>)(C99) | determina quais dos sinalizadores de status de ponto flutuante especificados estão definidos
(função)
[Documentação C++](<#/>) para feraiseexcept