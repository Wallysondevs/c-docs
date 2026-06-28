# feholdexcept

Definido no cabeçalho [`<fenv.h>`](<#/doc/numeric/fenv>)

```c
int feholdexcept( fenv_t* envp );  // desde C99
```

Primeiro, salva o ambiente de ponto flutuante atual no objeto apontado por `envp` (similar a [fegetenv](<#/doc/numeric/fenv/feenv>)), então limpa todas as flags de status de ponto flutuante, e então instala o modo sem interrupção: futuras exceções de ponto flutuante não interromperão a execução (não serão capturadas), até que o ambiente de ponto flutuante seja restaurado por [feupdateenv](<#/doc/numeric/fenv/feupdateenv>) ou [fesetenv](<#/doc/numeric/fenv/feenv>).

Esta função pode ser usada no início de uma sub-rotina que deve ocultar as exceções de ponto flutuante que ela pode levantar do chamador. Se apenas algumas exceções devem ser suprimidas, enquanto outras devem ser reportadas, o modo sem interrupção é geralmente encerrado com uma chamada a [feupdateenv](<#/doc/numeric/fenv/feupdateenv>) após limpar as exceções indesejadas.

### Parâmetros

- **envp** — ponteiro para o objeto do tipo fenv_t onde o ambiente de ponto flutuante será armazenado

### Valor de retorno

`0` em caso de sucesso, diferente de zero caso contrário.

### Exemplo

Execute este código
```c
    #include <stdio.h>
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
    
    double x2 (double x)   /* times two */
    {
        fenv_t curr_excepts;
    
        /* Save and clear current f-p environment. */
        feholdexcept(&curr_excepts);
    
        /* Raise inexact and overflow exceptions. */
        printf("In x2():  x = %f\n", x=x*2.0);
        show_fe_exceptions();
        feclearexcept(FE_INEXACT);   /* hide inexact exception from caller */
    
        /* Merge caller's exceptions (FE_INVALID)        */
        /* with remaining x2's exceptions (FE_OVERFLOW). */
        feupdateenv(&curr_excepts);
        return x;
    }
    
    int main(void)
    {    
        feclearexcept(FE_ALL_EXCEPT);
        feraiseexcept(FE_INVALID);   /* some computation with invalid argument */
        show_fe_exceptions();
        printf("x2(DBL_MAX) = %f\n", x2(DBL_MAX));
        show_fe_exceptions();
    
        return 0;
    }
```

Saída:
```
    current exceptions raised:  FE_INVALID
    In x2():  x = inf
    current exceptions raised:  FE_INEXACT FE_OVERFLOW
    x2(DBL_MAX) = inf
    current exceptions raised:  FE_INVALID FE_OVERFLOW
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.6.4.2 A função feholdexcept (p: 213-214)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.6.4.2 A função feholdexcept (p: 194-195)

### Veja também

[ feupdateenv](<#/doc/numeric/fenv/feupdateenv>)(C99) | restaura o ambiente de ponto flutuante e levanta as exceções previamente levantadas
(função)
[ fegetenvfesetenv](<#/doc/numeric/fenv/feenv>)(C99) | salva ou restaura o ambiente de ponto flutuante atual
(função)
[ FE_DFL_ENV](<#/doc/numeric/fenv/FE_DFL_ENV>)(C99) | ambiente de ponto flutuante padrão
(macro constante)
[Documentação C++](<#/>) para feholdexcept