# EXIT_SUCCESS, EXIT_FAILURE

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
#define EXIT_SUCCESS /*definido pela implementação*/
#define EXIT_FAILURE /*definido pela implementação*/
```

As macros `EXIT_SUCCESS` e `EXIT_FAILURE` expandem-se para expressões constantes integrais que podem ser usadas como argumentos para a função [exit](<#/doc/program/exit>) (e, portanto, como os valores a serem retornados da [função main](<#/doc/language/main_function>)), e indicam o status de execução do programa.

Constante | Descrição
`EXIT_SUCCESS` | execução bem-sucedida de um programa
`EXIT_FAILURE` | execução mal-sucedida de um programa

### Notas

Tanto `EXIT_SUCCESS` quanto o valor zero indicam status de execução bem-sucedida do programa (veja [exit](<#/doc/program/exit>)), embora não seja exigido que `EXIT_SUCCESS` seja igual a zero.

### Exemplo

Execute este código
```
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(void)
    {
        FILE* fp = fopen("data.txt", "r");
        if (fp == NULL)
        {
           fprintf(stderr, "fopen() failed in file %s at line #%d", __FILE__, __LINE__);
           exit(EXIT_FAILURE);
        }
    
        /* Normal processing continues here. */
        fclose(fp);
        printf("Normal Return\n");
    
        return EXIT_SUCCESS;
    }
```

Saída:
```
    fopen() failed in file main.cpp at line #9
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.22/3 Utilitários gerais <stdlib.h> (p: A definir)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.22/3 Utilitários gerais <stdlib.h> (p: 248)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.22/3 Utilitários gerais <stdlib.h> (p: 340)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.20/3 Utilitários gerais <stdlib.h> (p: 306)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.10 Utilitários gerais <stdlib.h>

### Veja também

[Documentação C++](<#/>) para EXIT_SUCCESS, EXIT_FAILURE
---