# exit

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
void exit( int exit_code );  // até C11
_Noreturn void exit( int exit_code );  // desde C11
(até C23)  // até C23
[[noreturn]] void exit( int exit_code );  // desde C23
```

Causa a terminação normal do programa.

Várias etapas de limpeza são realizadas:

*   funções passadas para [atexit](<#/doc/program/atexit>) são chamadas, na ordem inversa de registro
*   todos os fluxos C são descarregados e fechados
*   arquivos criados por [tmpfile](<#/doc/io/tmpfile>) são removidos
*   o controle é retornado ao ambiente hospedeiro. Se `exit_code` for zero ou [EXIT_SUCCESS](<#/doc/program/EXIT_status>), um status definido pela implementação indicando terminação bem-sucedida é retornado. Se `exit_code` for [EXIT_FAILURE](<#/doc/program/EXIT_status>), um status definido pela implementação indicando terminação mal-sucedida é retornado. Em outros casos, um valor de status definido pela implementação é retornado.

### Notas

As funções registradas com [at_quick_exit](<#/doc/program/at_quick_exit>) não são chamadas.

O comportamento é indefinido se um programa chamar `exit` mais de uma vez, ou se chamar `exit` e [quick_exit](<#/doc/program/quick_exit>)

O comportamento é indefinido se, durante uma chamada a uma função registrada com [atexit](<#/doc/program/atexit>), a função sair com [longjmp](<#/doc/program/longjmp>).

Retornar da [função main](<#/doc/language/main_function>), seja por uma instrução `return` ou por atingir o final da função, executa `exit()`, passando o argumento da instrução `return` (ou ​0​ se um retorno implícito foi usado) como `exit_code`.

### Parâmetros

- **exit_code** — status de saída do programa

### Valor de retorno

(nenhum)

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(void)
    {
        FILE *fp = fopen("data.txt","r");
        if (fp == NULL)
        {
           fprintf(stderr, "error opening file data.txt in function main()\n");
           exit( EXIT_FAILURE );
        }
        fclose(fp);
        printf("Normal Return\n");
        return EXIT_SUCCESS ;
    }
```

Saída possível:
```
    error opening file data.txt in function main()
```

### Referências

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.22.4.4 A função exit (p: 256)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.22.4.4 A função exit (p: 351-352)

*   Padrão C99 (ISO/IEC 9899:1999):

    *   7.20.4.3 A função exit (p: 315-316)

*   Padrão C89/C90 (ISO/IEC 9899:1990):

    *   4.10.4.3 A função exit

### Veja também

[ abort](<#/doc/program/abort>) | causa a terminação anormal do programa (sem limpeza)
(função)
[ atexit](<#/doc/program/atexit>) | registra uma função a ser chamada na invocação de **exit()**
(função)
[ quick_exit](<#/doc/program/quick_exit>)(C11) | causa a terminação normal do programa sem limpeza completa
(função)
[documentação C++](<#/>) para exit