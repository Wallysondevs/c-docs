# stdin, stdout, stderr

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
#define stdin /* implementation-defined */
#define stdout /* implementation-defined */
#define stderr /* implementation-defined */
```

Três fluxos de texto são predefinidos. Esses fluxos são implicitamente abertos e não orientados na inicialização do programa.

1) Associado ao fluxo de _entrada padrão_, usado para ler entrada convencional. Na inicialização do programa, o fluxo é totalmente armazenado em buffer se e somente se for determinado que o fluxo não se refere a um dispositivo interativo.

2) Associado ao fluxo de _saída padrão_, usado para escrever saída convencional. Na inicialização do programa, o fluxo é totalmente armazenado em buffer se e somente se for determinado que o fluxo não se refere a um dispositivo interativo.

3) Associado ao fluxo de _erro padrão_, usado para escrever saída de diagnóstico. Na inicialização do programa, o fluxo não é totalmente armazenado em buffer.

O que constitui um dispositivo interativo é definido pela implementação.

Essas macros são expandidas para expressões do tipo [FILE](<#/doc/io/FILE>)*.

### Notas

Embora não seja exigido pelo POSIX, a convenção UNIX é que `stdin` e `stdout` são armazenados em buffer de linha se associados a um terminal e `stderr` não é armazenado em buffer.

Essas macros podem ser expandidas para lvalues modificáveis. Se qualquer um desses lvalues [FILE](<#/doc/io/FILE>)* for modificado, operações subsequentes no fluxo correspondente resultam em comportamento não especificado ou comportamento indefinido.

### Exemplo

Este exemplo mostra uma função equivalente a [printf](<#/doc/io/fprintf>).

Execute este código
```c
    #include <stdarg.h>
    #include <stdio.h>
     
    int my_printf(const char* restrict fmt, ...)
    {
        va_list vl;
        va_start(vl, fmt);
        int ret = vfprintf(stdout, fmt, vl);
        va_end(vl);
        return ret;
    }
     
    int main(void)
    {
        my_printf("Rounding:\t%f %.0f %.32f\n", 1.5, 1.5, 1.3);
        my_printf("Padding:\t%05.2f %.2f %5.2f\n", 1.5, 1.5, 1.5);
        my_printf("Scientific:\t%E %e\n", 1.5, 1.5);
        my_printf("Hexadecimal:\t%a %A\n", 1.5, 1.5);
    }
```

Saída possível:
```
    Rounding:       1.500000 2 1.30000000000000004440892098500626
    Padding:        01.50 1.50  1.50
    Scientific:     1.500000E+00 1.500000e+00
    Hexadecimal:    0x1.8p+0 0X1.8P+0
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.21.1 Introdução (p: TBD)

    

  * 7.21.2 Fluxos (p: TBD)

    

  * 7.21.2 Arquivos (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.21.1 Introdução (p: 217-218)

    

  * 7.21.2 Fluxos (p: 217-219)

    

  * 7.21.2 Arquivos (p: 219-221)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.21.1 Introdução (p: 296-298)

    

  * 7.21.2 Fluxos (p: 298-299)

    

  * 7.21.2 Arquivos (p: 300-302)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.19.1 Introdução (p: 262-264)

    

  * 7.19.2 Fluxos (p: 264-265)

    

  * 7.19.2 Arquivos (p: 266-268)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 7.9.1 Introdução

    

  * 7.9.2 Fluxos

    

  * 7.9.3 Arquivos

### Veja também

[ FILE](<#/doc/io/FILE>) | tipo de objeto, capaz de armazenar todas as informações necessárias para controlar um fluxo de E/S C
(typedef)
[Documentação C++](<#/>) para stdin, stdout, stderr