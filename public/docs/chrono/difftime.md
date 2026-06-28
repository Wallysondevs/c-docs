# difftime

Definido no cabeçalho [`<time.h>`](<#/doc/chrono>)

```c
double difftime( time_t time_end, time_t time_beg );
```

  
Calcula a diferença entre dois tempos de calendário como objetos [time_t](<#/doc/chrono/time_t>) (time_end - time_beg) em segundos. Se `time_end` se refere a um ponto no tempo anterior a `time_beg`, então o resultado é negativo. 

### Parâmetros

time_beg, time_end  |  \-  |  tempos a comparar   
  
### Valor de retorno

Diferença entre dois tempos em segundos. 

### Observações

Em sistemas POSIX, [time_t](<#/doc/chrono/time_t>) é medido em segundos, e `difftime` é equivalente à subtração aritmética, mas C e C++ permitem unidades fracionárias para [time_t](<#/doc/chrono/time_t>). 

### Exemplo

O programa a seguir calcula o número de segundos que se passaram desde o início do mês.

Execute este código
```c
    #include <stdio.h>
    #include <time.h>
    
    int main(void)
    {
        time_t now = time(0);
    
        struct tm beg = *localtime(&now);
    
        // define beg para o início do mês
        beg.tm_hour = 0,
        beg.tm_min = 0,
        beg.tm_sec = 0,
        beg.tm_mday = 1;
    
        double seconds = difftime(now, mktime(&beg));
    
        printf("%.f seconds have passed since the beginning of the month.\n", seconds);
    
        return 0;
    }
```

Saída: 
```
    1937968 segundos se passaram desde o início do mês.
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.27.2.2 A função difftime (p: 285) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.27.2.2 A função difftime (p: 390) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.23.2.2 A função difftime (p: 338) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 7.12.2.2 A função difftime (p: 171) 

### Veja também

[documentação C++](<#/>) para difftime  
---