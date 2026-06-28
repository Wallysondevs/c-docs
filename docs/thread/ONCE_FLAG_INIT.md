# call_once, once_flag, ONCE_FLAG_INIT

Definido no cabeçalho [`<threads.h>`](<#/doc/thread>)

```c
void call_once( once_flag* flag, void (*func)(void) );  // desde C11
typedef /* unspecified */ once_flag  // desde C11
#define ONCE_FLAG_INIT /* unspecified */  // desde C11
```

  
1) Chama a função `func` exatamente uma vez, mesmo que invocada por várias threads. A conclusão da função `func` sincroniza com todas as chamadas anteriores ou subsequentes a `call_once` com a mesma variável `flag`.

2) Tipo de objeto completo capaz de armazenar uma flag usada por `call_once`.

3) Expande para um valor que pode ser usado para inicializar um objeto do tipo `once_flag`.

### Parâmetros

flag  |  \-  |  ponteiro para um objeto do tipo `call_once` que é usado para garantir que `func` seja chamada apenas uma vez   
func  |  \-  |  a função a ser executada apenas uma vez   
  
### Valor de retorno

(nenhum) 

### Notas

O equivalente POSIX desta função é [`pthread_once`](<http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_once.html>). 

### Exemplo

Execute este código
```c 
    #include <stdio.h>
    #include <threads.h>
     
    void do_once(void) {
        puts("called once");
    }
     
    static once_flag flag = ONCE_FLAG_INIT;
    int func(void* data)
    {
        call_once(&flag, do_once);
    }
     
    int main(void)
    {
        thrd_t t1, t2, t3, t4;
        thrd_create(&t1, func, NULL);
        thrd_create(&t2, func, NULL);
        thrd_create(&t3, func, NULL);
        thrd_create(&t4, func, NULL);
     
        thrd_join(t1, NULL);
        thrd_join(t2, NULL);
        thrd_join(t3, NULL);
        thrd_join(t4, NULL);
    }
```

Saída: 
```
    called once
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.26.2.1 A função call_once (p: 275) 

    

  * 7.26.1/3 ONCE_FLAG_INIT (p: 274) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.26.2.1 A função call_once (p: 378) 

    

  * 7.26.1/3 ONCE_FLAG_INIT (p: 376) 

### Veja também

[Documentação C++](<#/>) para call_once  
---