# at_quick_exit

Definido no cabeçalho [`<stdlib.h>`](<../program.html> "c/program")

```c
int at_quick_exit( void (*func)(void) );  // desde C11
```

Registra a função apontada por `func` para ser chamada na terminação rápida do programa (via [quick_exit](<#/doc/program/quick_exit>)).

Chamar a função de várias threads não induz uma condição de corrida (data race). A implementação tem garantia de suportar o registro de pelo menos 32 funções. O limite exato é definido pela implementação.

As funções registradas não serão chamadas na [terminação normal do programa](<#/doc/program/exit>). Se uma função precisar ser chamada nesse caso, [atexit](<#/doc/program/atexit>) deve ser usado.

### Parâmetros

- **func** — ponteiro para uma função a ser chamada na terminação rápida do programa

### Valor de retorno

​0​ se o registro for bem-sucedido, valor diferente de zero caso contrário.

### Exemplo

Execute este código
```c
    #include <stdlib.h>
    #include <stdio.h>
    
    void f1(void)
    {
        puts("pushed first");
        fflush(stdout);
    }
    
    void f2(void)
    {
        puts("pushed second");
    }
    
    int main(void)
    {
        at_quick_exit(f1);
        at_quick_exit(f2);
        quick_exit(0);
    }
```

Saída:
```
    pushed second
    pushed first
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.22.4.3 A função at_quick_exit (p: 255)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.22.4.3 A função at_quick_exit (p: 351)

### Veja também

[ abort](<#/doc/program/abort>) | causa a terminação anormal do programa (sem limpeza)
(função)
[ exit](<#/doc/program/exit>) | causa a terminação normal do programa com limpeza
(função)
[ atexit](<#/doc/program/atexit>) | registra uma função para ser chamada na invocação de [exit()](<#/doc/program/exit>)
(função)
[ quick_exit](<#/doc/program/quick_exit>)(C11) | causa a terminação normal do programa sem limpeza completa
(função)
[Documentação C++](<#/>) para at_quick_exit