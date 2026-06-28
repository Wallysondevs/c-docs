# va_list

Definido no cabeçalho [`<stdarg.h>`](<#/doc/variadic>)

```c
/* não especificado */ va_list;
```

  
`va_list` é um tipo de objeto completo adequado para armazenar as informações necessárias pelas macros va_start, va_copy, va_arg e va_end.

Se uma instância de `va_list` for criada, passada para outra função e usada via va_arg nessa função, então qualquer uso subsequente na função chamadora deve ser precedido por uma chamada a va_end.

É legal passar um ponteiro para um objeto `va_list` para outra função e então usar esse objeto depois que a função retornar.

### Referências

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.16/3 Argumentos variáveis <stdarg.h> (p: 269) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.15/3 Argumentos variáveis <stdarg.h> (p: 249) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.8 ARGUMENTOS VARIÁVEIS <stdarg.h>

### Veja também

[ va_arg](<#/doc/variadic/va_arg>) | acessa o próximo argumento de função variádica   
(macro de função)  
[ va_copy](<#/doc/variadic/va_copy>)(C99) | faz uma cópia dos argumentos de função variádica   
(macro de função)  
[ va_end](<#/doc/variadic/va_end>) | finaliza a travessia dos argumentos de função variádica   
(macro de função)  
[ va_start](<#/doc/variadic/va_start>) | habilita o acesso aos argumentos de função variádica   
(macro de função)  
[Documentação C++](<#/>) para va_list