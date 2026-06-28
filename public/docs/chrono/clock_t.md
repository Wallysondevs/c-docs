# clock_t

Definido no cabeçalho [`<time.h>`](<#/doc/chrono>)

```c
typedef /* unspecified */ clock_t;
```

  
Aritmético(até C11)Real(desde C11) tipo capaz de representar o tempo de processador usado por um processo. Possui um intervalo e precisão definidos pela implementação. 

### Exemplo

Execute este código
```
    #include <stdio.h>
    #include <time.h>
    #include <math.h>
     
    volatile double sink;
    int main (void)
    {
      clock_t start = clock();
     
      for(size_t i=0; i<3141592; ++i)
          sink+=sin(i);
     
      clock_t end = clock();
      double cpu_time_used = ((double) (end - start)) / CLOCKS_PER_SEC;
     
      printf("for loop took %f seconds to execute \n", cpu_time_used);
    }
```

Saída possível: 
```
    for loop took 0.271828 seconds to execute
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.27.1/3 Componentes de tempo (p: 284) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.27.1/3 Componentes de tempo (p: 388) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.23.1/3 Componentes de tempo (p: 338) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.12.1 Componentes de tempo 

### Veja também

[ clock](<#/doc/chrono/clock>) |  retorna o tempo bruto do clock do processador desde que o programa foi iniciado   
(função)  
[ CLOCKS_PER_SEC](<#/doc/chrono/CLOCKS_PER_SEC>) |  número de tiques do clock do processador por segundo   
(constante de macro)  
[Documentação C++](<#/>) para clock_t