# atexit

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
int atexit( void (*func)(void) );
```

Registra a função apontada por `func` para ser chamada na terminação normal do programa (via [exit()](<#/doc/program/exit>) ou retornando de `main()`). As funções serão chamadas na ordem inversa em que foram registradas, ou seja, a função registrada por último será executada primeiro.

A mesma função pode ser registrada mais de uma vez.

A implementação tem garantia de suportar o registro de pelo menos 32 funções. O limite exato é definido pela implementação.

### Parâmetros

- **func** — ponteiro para uma função a ser chamada na terminação normal do programa

### Valor de retorno

​0​ se o registro for bem-sucedido, valor diferente de zero caso contrário.

### Exemplo

Execute este código
```c
    #include <stdlib.h>
    #include <stdio.h>
    
    void f1(void)
    {
        puts("f1");
    }
    
    void f2(void)
    {
        puts("f2");
    }
    
    int main(void)
    {
        if ( ! atexit(f1) && ! atexit(f2) && ! atexit(f2) )
            return EXIT_SUCCESS ;
    
        // o registro de atexit falhou
        return EXIT_FAILURE ;
    
    }   // <- se o registro foi bem-sucedido, chama f2, f2, f1
```

Saída:
```
    f2
    f2
    f1
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.22.4.2 A função atexit (p: 255)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.22.4.2 A função atexit (p: 350)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.20.4.2 A função atexit (p: 315)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 7.10.4.2 A função atexit (p: 156)

### Veja também

[ at_quick_exit](<#/doc/program/at_quick_exit>)(C11) | registra uma função para ser chamada na invocação de [`quick_exit`](<#/doc/program/quick_exit>)
(função)
[Documentação C++](<#/>) para atexit