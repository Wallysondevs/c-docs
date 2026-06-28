# quick_exit

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
_Noreturn void quick_exit( int exit_code );  // desde C11
(até C23)  // até C23
[[noreturn]] void quick_exit( int exit_code );  // desde C23
```

  
Causa o encerramento normal do programa sem limpar completamente os recursos.

Funções passadas para [at_quick_exit](<#/doc/program/at_quick_exit>) são chamadas na ordem inversa de seu registro. Após chamar as funções registradas, invoca [_Exit](<#/doc/program/_Exit>)(exit_code).

Funções passadas para [atexit](<#/doc/program/atexit>) ou manipuladores de sinal passados para [signal](<#/doc/program/signal>) não são chamados.

### Parâmetros

exit_code  |  \-  |  status de saída do programa   
  
### Valor de retorno

(nenhum)

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
     
    void f3(void)
    {
        puts("won't be called");
    }
     
    int main(void)
    {
        at_quick_exit(f1);
        at_quick_exit(f2);
        atexit(f3);
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

    

  * 7.22.4.7 A função quick_exit (p: 257) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.22.4.7 A função quick_exit (p: 353) 

### Veja também

[ abort](<#/doc/program/abort>) |  causa o encerramento anormal do programa (sem limpeza)   
(função)  
[ atexit](<#/doc/program/atexit>) |  registra uma função a ser chamada na invocação de [exit()](<#/doc/program/exit>)   
(função)  
[ at_quick_exit](<#/doc/program/at_quick_exit>)(C11) |  registra uma função a ser chamada na invocação de `quick_exit`   
(função)  
[Documentação C++](<#/>) para quick_exit