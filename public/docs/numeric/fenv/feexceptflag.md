# fegetexceptflag, fesetexceptflag

Definido no cabeçalho [`<fenv.h>`](<#/doc/numeric/fenv>)

```c
int fegetexceptflag( fexcept_t* flagp, int excepts );  // desde C99
int fesetexceptflag( const fexcept_t* flagp, int excepts );  // desde C99
```

1) Tenta obter o conteúdo completo das flags de exceção de ponto flutuante que estão listadas no argumento de máscara de bits `excepts`, que é um OR bit a bit das [macros de exceção de ponto flutuante](<#/doc/numeric/fenv/FE_exceptions>).

2) Tenta copiar o conteúdo completo das flags de exceção de ponto flutuante que estão listadas em `excepts` de `flagp` para o ambiente de ponto flutuante. Não levanta nenhuma exceção, apenas modifica as flags.

O conteúdo completo de uma flag de exceção de ponto flutuante não é necessariamente um valor booleano indicando se a exceção foi levantada ou limpa. Por exemplo, pode ser uma struct que inclui o status booleano e o endereço do código que acionou a exceção. Essas funções obtêm todo esse conteúdo e o obtêm/armazenam em `flagp` em formato definido pela implementação.

### Parâmetros

- **flagp** — ponteiro para um objeto fexcept_t onde as flags serão armazenadas ou lidas
- **excepts** — máscara de bits listando as flags de exceção a serem obtidas/definidas

### Valor de retorno

​0​ em caso de sucesso, diferente de zero caso contrário.

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
    
    int main(void)
    {
        fexcept_t excepts;
    
        /* Setup a "current" set of exception flags. */
        feraiseexcept(FE_INVALID);
        show_fe_exceptions();
    
        /* Save current exception flags. */
        fegetexceptflag(&excepts,FE_ALL_EXCEPT);
    
        /* Temporarily raise two other exceptions. */
        feclearexcept(FE_ALL_EXCEPT);
        feraiseexcept(FE_OVERFLOW | FE_INEXACT);
        show_fe_exceptions();
    
        /* Restore previous exception flags. */
        fesetexceptflag(&excepts,FE_ALL_EXCEPT);
        show_fe_exceptions();
    
        return 0;
    }
```

Saída:
```
    current exceptions raised: FE_INVALID
    current exceptions raised: FE_INEXACT FE_OVERFLOW
    current exceptions raised: FE_INVALID
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.6.2.2 A função fegetexceptflag (p: 210)

    

  * 7.6.2.4 A função fesetexceptflag (p: 211)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.6.2.2 A função fegetexceptflag (p: 191)

    

  * 7.6.2.4 A função fesetexceptflag (p: 192)

### Veja também

[documentação C++](<#/>) para fegetexceptflag, fesetexceptflag
---