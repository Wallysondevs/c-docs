# Argumentos Variádicos

Funções variádicas são funções que podem ser chamadas com um número diferente de argumentos.

Apenas [declarações de função](<#/doc/language/function_declaration>) prototipadas podem ser variádicas. Isso é indicado pelo parâmetro na forma ... que deve aparecer por último na lista de parâmetros e deve seguir pelo menos um parâmetro nomeado (até C23). O parâmetro de reticências e o parâmetro precedente devem ser delimitados por vírgula (,).
```c
    // Declaração prototipada
    int printx(const char* fmt, ...); // função declarada desta forma
    printx("hello world");     // pode ser chamada com um
    printx("a=%d b=%d", a, b); // ou mais argumentos
    
    int printz(...); // OK desde C23 e em C++
    // Erro até C23: ... deve seguir pelo menos um parâmetro nomeado
    
    // int printy(..., const char* fmt); // Erro: ... deve ser o último
    // int printa(const char* fmt...);   // Erro em C: ',' é obrigatória; OK em C++
```

Na [chamada de função](<#/doc/language/operator_other>), cada argumento que faz parte da lista de argumentos variáveis passa por conversões implícitas especiais conhecidas como [promoções de argumento padrão](<#/doc/language/conversion>).

Dentro do corpo de uma função que usa argumentos variádicos, os valores desses argumentos podem ser acessados usando as [facilidades da biblioteca `<stdarg.h>`](<#/doc/variadic>):

Definido no cabeçalho `[`<stdarg.h>`](<#/doc/variadic>)`
---
[ va_start](<#/doc/variadic/va_start>) | habilita o acesso aos argumentos de função variádicos
(macro de função)
[ va_arg](<#/doc/variadic/va_arg>) | acessa o próximo argumento de função variádico
(macro de função)
[ va_copy](<#/doc/variadic/va_copy>)(C99) | cria uma cópia dos argumentos de função variádicos
(macro de função)
[ va_end](<#/doc/variadic/va_end>) | finaliza a travessia dos argumentos de função variádicos
(macro de função)
[ va_list](<#/doc/variadic/va_list>) | contém as informações necessárias por va_start, va_arg, va_end e va_copy
(typedef)

### Notas

Embora [declarações de função](<#/doc/language/function_declaration>) no estilo antigo (sem protótipo) permitam que as chamadas de função subsequentes usem qualquer número de argumentos, elas não são permitidas serem variádicas (a partir de C89). A definição de tal função deve especificar um número fixo de parâmetros e não pode usar as macros de `stdarg.h`.
```c
    // declaração no estilo antigo, removida em C23
    int printx(); // função declarada desta forma
    printx("hello world");     // pode ser chamada com um
    printx("a=%d b=%d", a, b); // ou mais argumentos
    // o comportamento de pelo menos uma dessas chamadas é indefinido, dependendo do
    // número de parâmetros que a função é definida para receber
```

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <time.h>
    #include <stdarg.h>
    
    void tlog(const char* fmt,...)
    {
        char msg[50];
        strftime(msg, sizeof msg, "%T", localtime(&(time_t){time(NULL)}));
        printf("[%s] ", msg);
        va_list args;
        va_start(args, fmt);
        vprintf(fmt, args);
        va_end(args);
    }
    
    int main(void)
    {
       tlog("logging %d %d %d...\n", 1, 2, 3);
    }
```

Saída:
```
    [10:21:38] logging 1 2 3...
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 6.7.6.3/9 Declaradores de função (incluindo protótipos) (pág: 96)

    

  * 7.16 Argumentos variáveis <stdarg.h> (pág: 197-199)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 6.7.6.3/9 Declaradores de função (incluindo protótipos) (pág: 133)

    

  * 7.16 Argumentos variáveis <stdarg.h> (pág: 269-272)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 6.7.5.3/9 Declaradores de função (incluindo protótipos) (pág: 119)

    

  * 7.15 Argumentos variáveis <stdarg.h> (pág: 249-252)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 3.5.4.3/5 Declaradores de função (incluindo protótipos)

    

  * 4.8 ARGUMENTOS VARIÁVEIS <stdarg.h>

### Veja também

[documentação C++](<#/>) para Argumentos variádicos
---