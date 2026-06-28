# va_end

Definido no cabeçalho [`<stdarg.h>`](<#/doc/variadic>)

```c
void va_end( va_list ap );
```

A macro `va_end` realiza a limpeza de um objeto `ap` inicializado por uma chamada a va_start ou va_copy. `va_end` pode modificar `ap` de forma que ele não seja mais utilizável.

Se não houver uma chamada correspondente a va_start ou va_copy, ou se `va_end` não for chamada antes que uma função que chama va_start ou va_copy retorne, o comportamento é indefinido.

### Parâmetros

- **ap** — uma instância do tipo va_list para limpar

### Valor expandido

(nenhum)

### Referências

* Padrão C11 (ISO/IEC 9899:2011):

* 7.16.1.3 A macro va_end (p: 270-271)

* Padrão C99 (ISO/IEC 9899:1999):

* 7.15.1.3 A macro va_end (p: 250-251)

* Padrão C89/C90 (ISO/IEC 9899:1990):

* 4.8.1.3 A macro va_end

### Veja também

[ va_arg](<#/doc/variadic/va_arg>) | acessa o próximo argumento de função variádica
(macro de função)
[ va_copy](<#/doc/variadic/va_copy>)(C99) | faz uma cópia dos argumentos de função variádica
(macro de função)
[ va_list](<#/doc/variadic/va_list>) | mantém as informações necessárias para va_start, va_arg, va_end e va_copy
(typedef)
[ va_start](<#/doc/variadic/va_start>) | habilita o acesso aos argumentos de função variádica
(macro de função)
[Documentação C++](<#/>) para va_end