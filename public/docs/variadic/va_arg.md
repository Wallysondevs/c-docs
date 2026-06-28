# va_arg

Definido no cabeçalho [`<stdarg.h>`](<#/doc/variadic>)

```c
T va_arg( va_list ap, T );
```

A macro `va_arg` se expande para uma expressão do tipo T que corresponde ao próximo parâmetro da va_list ap.

Antes de chamar `va_arg`, ap deve ser inicializada por uma chamada a `va_start` ou `va_copy`, sem nenhuma chamada intermediária a `va_end`. Cada invocação da macro `va_arg` modifica ap para apontar para o próximo argumento variável.

Se o tipo do próximo argumento em ap (após as promoções) não for [compatível](<#/doc/language/compatible_type>) com T, o comportamento é indefinido, a menos que:

  * um tipo seja um tipo inteiro com sinal, o outro tipo seja o tipo inteiro sem sinal correspondente, e o valor seja representável em ambos os tipos; ou
  * um tipo seja um ponteiro para void e o outro seja um ponteiro para um tipo de caractere.

Se `va_arg` for chamada quando não houver mais argumentos em ap, o comportamento é indefinido.

### Parâmetros

- **ap** — uma instância do tipo va_list
- **T** — o tipo do próximo parâmetro em ap

### Valor expandido

o próximo parâmetro variável em ap

### Exemplo

Execute este código
```c
    #include <math.h>
    #include <stdarg.h>
    #include <stdio.h>
    
    double stddev(int count, ...)
    {
        double sum = 0;
        double sum_sq = 0;
        va_list args;
        va_start(args, count);
        for (int i = 0; i < count; ++i)
        {
            double num = va_arg(args, double);
            sum += num;
            sum_sq += num*num;
        }
        va_end(args);
        return sqrt(sum_sq / count - (sum / count) * (sum / count));
    }
    
    int main(void)
    {
        printf("%f\n", stddev(4, 25.0, 27.3, 26.9, 25.7));
    }
```

Saída:
```
    0.920258
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.16.2.2 A macro va_arg (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.16.1.1 A macro va_arg (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.16.1.1 A macro va_arg (p: 269-270)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.15.1.1 A macro va_arg (p: 249-250)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.8.1.2 A macro va_arg

### Veja também

[ va_copy](<#/doc/variadic/va_copy>)(desde C99) | faz uma cópia dos argumentos de função variádicos
(macro de função) |
[ va_end](<#/doc/variadic/va_end>) | finaliza a travessia dos argumentos de função variádicos
(macro de função) |
[ va_list](<#/doc/variadic/va_list>) | armazena as informações necessárias por va_start, va_arg, va_end e va_copy
(typedef) |
[ va_start](<#/doc/variadic/va_start>) | habilita o acesso aos argumentos de função variádicos
(macro de função) |
[Documentação C++](<#/>) para va_arg