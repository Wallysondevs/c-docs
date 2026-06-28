# va_start

Definido no cabeçalho [`<stdarg.h>`](<#/doc/variadic>)

```c
void va_start( va_list ap, parmN );  // ate C23
void va_start( va_list ap, ... );  // desde C23
```

A macro `va_start` permite o acesso aos argumentos variáveis que seguem o argumento nomeado `parmN` (ate C23).

`va_start` deve ser invocada com uma instância de um objeto `va_list` válido `ap` antes de quaisquer chamadas para `va_arg`.

Se `parmN` for declarado com o especificador de classe de armazenamento `register`, com um tipo array, com um tipo função, ou com um tipo não compatível com o tipo que resulta das promoções de argumento padrão, o comportamento é indefinido. | (ate C23)
Apenas o primeiro argumento passado para `va_start` é avaliado. Quaisquer argumentos adicionais não são expandidos nem usados de forma alguma. | (desde C23)

### Parâmetros

- **ap** — uma instância do tipo `va_list`
- **parmN** — o parâmetro nomeado que precede o primeiro parâmetro variável

### Valor expandido

(nenhum)

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <stdarg.h>
    
    int add_nums_C99(int count, ...)
    {
        int result = 0;
        va_list args;
        va_start(args, count); // count pode ser omitido desde C23
    
        for (int i = 0; i < count; ++i) {
            result += va_arg(args, int);
        }
    
        va_end(args);
        return result;
    }
    
    #if __STDC_VERSION__ > 201710L
    // O mesmo que acima, válido desde C23
    int add_nums_C23(...)
    {
        int result = 0;
        va_list args;
        va_start(args);
    
        int count = va_arg(args, int);
        for (int i = 0; i < count; ++i) {
            result += va_arg(args, int);
        }
    
        va_end(args);
        return result;
    }
    #endif
    
    int main(void)
    {
        printf("%d\n", add_nums_C99(4, 25, 25, 50, 50));
    #if __STDC_VERSION__ > 201710L
        printf("%d\n", add_nums_C23(4, 25, 25, 50, 50));
    #endif
    }
```

Saída possível:
```
    150
    150
```

### Referências

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.16.1.4 A macro va_start (p: 198-199)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.16.1.4 A macro va_start (p: 271-272)

*   Padrão C99 (ISO/IEC 9899:1999):

    *   7.15.1.4 A macro va_start (p: 251-252)

*   Padrão C89/C90 (ISO/IEC 9899:1990):

    *   4.8.1.1 A macro va_start

### Veja também

[ va_arg](<#/doc/variadic/va_arg>) | acessa o próximo argumento de função variádica
(macro de função)
[ va_copy](<#/doc/variadic/va_copy>)(C99) | faz uma cópia dos argumentos de função variádica
(macro de função)
[ va_end](<#/doc/variadic/va_end>) | finaliza a travessia dos argumentos de função variádica
(macro de função)
[ va_list](<#/doc/variadic/va_list>) | armazena as informações necessárias por va_start, va_arg, va_end e va_copy
(typedef)
[Documentação C++](<#/>) para va_start