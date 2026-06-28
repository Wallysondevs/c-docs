# remove

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
int remove( const char* pathname );
```

Exclui o arquivo identificado pela string de caracteres apontada por pathname.

Se o arquivo estiver atualmente aberto por qualquer processo, o comportamento desta função é definido pela implementação. Sistemas POSIX desvinculam o nome do arquivo (entrada de diretório), mas o espaço do sistema de arquivos usado pelo arquivo não é recuperado enquanto ele estiver aberto em qualquer processo e enquanto outros links físicos para o arquivo existirem. O Windows não permite que o arquivo seja excluído em tais casos.

### Parâmetros

- **pathname** — ponteiro para uma string terminada em nulo contendo o caminho que identifica o arquivo a ser excluído

### Valor de retorno

`0` em caso de sucesso ou um valor diferente de zero em caso de erro.

### Observações

[POSIX especifica](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/remove.html>) muitos detalhes adicionais para o comportamento desta função.

### Exemplo

Execute este código
```
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(void)
    {
        FILE* fp = fopen("file1.txt", "w"); // create file
        if (!fp)
        {
            perror("file1.txt");
            return EXIT_FAILURE;
        }
        puts("Created file1.txt");
        fclose(fp);
    
        int rc = remove("file1.txt");
        if (rc)
        {
            perror("remove");
            return EXIT_FAILURE;
        }
        puts("Removed file1.txt");
    
        fp = fopen("file1.txt", "r"); // Failure: file does not exist
        if (!fp)
            perror("Opening removed file failed");
    
        rc = remove("file1.txt"); // Failure: file does not exist
        if (rc)
            perror("Double-remove failed");
    
        return EXIT_SUCCESS;
    }
```

Saída possível:
```
    Created file1.txt
    Removed file1.txt
    Opening removed file failed: No such file or directory
    Double-remove failed: No such file or directory
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.21.4.1 A função remove (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.21.4.1 A função remove (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.21.4.1 A função remove (p: 302)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.19.4.1 A função remove (p: 268)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.9.4.1 A função remove

### Veja também

[ rename](<#/doc/io/rename>) | renomeia um arquivo
(função)
[Documentação C++](<#/>) para remove