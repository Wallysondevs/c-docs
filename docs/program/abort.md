# abort

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
void abort(void);  // até C11
_Noreturn void abort(void);  // desde C11
(até C23)  // até C23
[[noreturn]] void abort(void);  // desde C23
```

  
Causa a terminação anormal do programa, a menos que [SIGABRT](<#/doc/program/SIG_types>) esteja sendo capturado por um manipulador de sinal (signal handler) passado para signal e o manipulador não retorne.

Funções passadas para [atexit()](<#/doc/program/atexit>) não são chamadas. Se recursos abertos, como arquivos, são fechados é definido pela implementação. Um status definido pela implementação é retornado ao ambiente hospedeiro (host environment) que indica execução mal-sucedida.

### Parâmetros

(nenhum)

### Valor de retorno

(nenhum)

### Notas

POSIX [especifica](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/abort.html>) que a função `abort()` anula o bloqueio ou a ignorância do sinal `SIGABRT`.

Alguns intrínsecos do compilador (compiler intrinsics), por exemplo, [`__builtin_trap`](<https://gcc.gnu.org/onlinedocs/gcc/Other-Builtins.html>) (gcc, clang e icc) ou [`__fastfail`](<https://learn.microsoft.com/en-us/cpp/intrinsics/fastfail>)/[`__debugbreak`](<https://learn.microsoft.com/en-us/cpp/intrinsics/debugbreak>) (msvc), podem ser usados para terminar o programa o mais rápido possível.

### Exemplo

Execute este código
```
    #include <stdio.h>
    #include <stdlib.h>
     
    int main(void)
    {
        FILE *fp = fopen("data.txt","r");
        if (fp == NULL)
        {
            fprintf(stderr, "error opening file data.txt in function main()\n");
            abort();
        }
     
        /* Normal processing continues here. */
        fclose(fp);
        printf("Normal Return\n");
        return 0;
    }
```

Saída: 
```
    error opening file data.txt in function main()
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.22.4.1 A função abort (p: 255) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.22.4.1 A função abort (p: 350) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.20.4.1 A função abort (p: 315) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.10.4.1 A função abort 

### Veja também

[ exit](<#/doc/program/exit>) |  causa a terminação normal do programa com limpeza   
(função)  
[ atexit](<#/doc/program/atexit>) |  registra uma função a ser chamada na invocação de [exit()](<#/doc/program/exit>)   
(função)  
[ quick_exit](<#/doc/program/quick_exit>)(C11) |  causa a terminação normal do programa sem limpeza completa   
(função)  
[Documentação C++](<#/>) para abort