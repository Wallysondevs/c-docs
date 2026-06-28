# Funções variádicas

Funções variádicas são funções (por exemplo, [printf](<#/doc/io/fprintf>)) que aceitam um número variável de argumentos.

A declaração de uma função variádica usa reticências como o último parâmetro, por exemplo, int [printf](<#/doc/io/fprintf>)(const char* format, ...);. Veja [argumentos variádicos](<#/doc/language/variadic>) para detalhes adicionais sobre a sintaxe e conversões automáticas de argumentos.

O acesso aos argumentos variádicos a partir do corpo da função utiliza as seguintes facilidades da biblioteca:

##### Tipos

---
[ va_list](<#/doc/variadic/va_list>) | armazena as informações necessárias por va_start, va_arg, va_end e va_copy
(typedef)

##### Macros

Definido no cabeçalho `<stdarg.h>`
[ va_start](<#/doc/variadic/va_start>) | permite o acesso aos argumentos de função variádicos
(macro de função)
[ va_arg](<#/doc/variadic/va_arg>) | acessa o próximo argumento de função variádico
(macro de função)
[ va_copy](<#/doc/variadic/va_copy>)(C99) | faz uma cópia dos argumentos de função variádicos
(macro de função)
[ va_end](<#/doc/variadic/va_end>) | finaliza a travessia dos argumentos de função variádicos
(macro de função)

### Exemplo

Imprime valores de diferentes tipos.

Execute este código
```
    #include <stdarg.h>
    #include <stdio.h>
    
    void simple_printf(const char* fmt, ...)
    {
        va_list args;
    
        for (va_start(args, fmt); *fmt != '\0'; ++fmt)
        {
            switch(*fmt)
            {
                case 'd':
                {
                    int i = va_arg(args, int);
                    printf("%d\n", i);
                    break;
                }
                case 'c':
                {
                    // Uma variável 'char' será promovida para 'int'
                    // Um literal de caractere em C já é 'int' por si só
                    int c = va_arg(args, int);
                    printf("%c\n", c);
                    break;
                }
                case 'f':
                {
                    double d = va_arg(args, double);
                    printf("%f\n", d);
                    break;
                }
                default:
                    puts("Formatador desconhecido!");
                    goto END;
            }
        }
    END:
        va_end(args);
    }
    
    int main(void)
    {
        simple_printf("dcff", 3, 'a', 1.969, 42.5);
    }
```

Saída:
```
    3
    a
    1.969000
    42.50000
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.16 Argumentos variáveis <stdarg.h> (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.16 Argumentos variáveis <stdarg.h> (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.16 Argumentos variáveis <stdarg.h> (p: 269-272)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.15 Argumentos variáveis <stdarg.h> (p: 249-252)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.8 ARGUMENTOS VARIÁVEIS <stdarg.h>

### Veja também

[Documentação C++](<#/>) para Funções variádicas
---