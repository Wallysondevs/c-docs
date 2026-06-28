# va_copy

Definido no cabeçalho [`<stdarg.h>`](<#/doc/variadic>)

```c
void va_copy( va_list dest, va_list src );  // desde C99
```

A macro `va_copy` copia `src` para `dest`.

`va_end` deve ser chamada em `dest` antes que a função retorne ou qualquer reinicialização subsequente de `dest` (através de chamadas para `va_start` ou `va_copy`).

### Parâmetros

- **dest** — uma instância do tipo `va_list` para inicializar
- **src** — o `va_list` de origem que será usado para inicializar `dest`

### Valor expandido

(nenhum)

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <stdarg.h>
    #include <math.h>
    
    double sample_stddev(int count, ...) 
    {
        /* Compute the mean with args1. */
        double sum = 0;
        va_list args1;
        va_start(args1, count);
        va_list args2;
        va_copy(args2, args1);   /* copy va_list object */
        for (int i = 0; i < count; ++i) {
            double num = va_arg(args1, double);
            sum += num;
        }
        va_end(args1);
        double mean = sum / count;
    
        /* Compute standard deviation with args2 and mean. */
        double sum_sq_diff = 0;
        for (int i = 0; i < count; ++i) {
            double num = va_arg(args2, double);
            sum_sq_diff += (num-mean) * (num-mean);
        }
        va_end(args2);
        return sqrt(sum_sq_diff / count);
    }
    
    int main(void) 
    {
        printf("%f\n", sample_stddev(4, 25.0, 27.3, 26.9, 25.7));
    }
```

Saída possível:
```
    0.920258
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.16.1.2 A macro va_copy (p: 270) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.15.1.2 A macro va_copy (p: 250) 

### Veja também

[ va_arg](<#/doc/variadic/va_arg>) | acessa o próximo argumento de função variádica
(macro de função)
[ va_end](<#/doc/variadic/va_end>) | finaliza a travessia dos argumentos de função variádica
(macro de função)
[ va_list](<#/doc/variadic/va_list>) | mantém as informações necessárias para va_start, va_arg, va_end e va_copy
(typedef)
[ va_start](<#/doc/variadic/va_start>) | habilita o acesso a argumentos de função variádica
(macro de função)
[Documentação C++](<#/>) para va_copy