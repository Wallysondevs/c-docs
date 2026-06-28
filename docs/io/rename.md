# rename

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
int rename( const char* old_filename, const char* new_filename );
```

  
Altera o nome de um arquivo. O arquivo é identificado pela string de caracteres apontada por old_filename. O novo nome do arquivo é identificado pela string de caracteres apontada por new_filename.

Se new_filename existir, o comportamento é definido pela implementação.

### Parâmetros

old_filename  |  \-  |  ponteiro para uma string terminada em nulo contendo o caminho que identifica o arquivo a ser renomeado   
new_filename  |  \-  |  ponteiro para uma string terminada em nulo contendo o novo caminho do arquivo   
  
### Valor de retorno

​0​ em caso de sucesso ou um valor diferente de zero em caso de erro.

### Notas

[POSIX](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/rename.html>) especifica muitos detalhes adicionais sobre a semântica desta função.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(void)
    {
        FILE* fp = fopen("from.txt", "w"); // cria o arquivo "from.txt"
        if (!fp)
        {
            perror("from.txt");
            return EXIT_FAILURE;
        }
        fputc('a', fp); // escreve em "from.txt"
        fclose(fp);
    
        int rc = rename("from.txt", "to.txt");
        if (rc)
        {
            perror("rename");
            return EXIT_FAILURE;
        }
    
        fp = fopen("to.txt", "r");
        if(!fp)
        {
            perror("to.txt");
            return EXIT_FAILURE;
        }
        printf("%c\n", fgetc(fp)); // lê de "to.txt"
        fclose(fp);
    
        return EXIT_SUCCESS;
    }
```

Saída possível: 
```
    a
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.21.4.2 A função rename (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.21.4.2 A função rename (p: TBD) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.21.4.2 A função rename (p: 302-303) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.19.4.2 A função rename (p: 268-269) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.9.4.2 A função rename 

### Veja também

[ remove](<#/doc/io/remove>) |  apaga um arquivo   
(função)  
[Documentação C++](<#/>) para rename