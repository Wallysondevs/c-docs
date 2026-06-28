# getchar

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
int getchar( void );
```

Lê o próximo caractere de [stdin](<#/doc/io/std_streams>).

Equivalente a [getc](<#/doc/io/fgetc>)([stdin](<#/doc/io/std_streams>)).

### Parâmetros

(nenhum)

### Valor de retorno

O caractere obtido em caso de sucesso ou [EOF](<#/doc/io>) em caso de falha.

Se a falha foi causada pela condição de fim de arquivo, adicionalmente define o indicador _eof_ (veja [feof()](<#/doc/io/feof>)) em [stdin](<#/doc/io/std_streams>). Se a falha foi causada por algum outro erro, define o indicador de _erro_ (veja [ferror()](<#/doc/io/ferror>)) em [stdin](<#/doc/io/std_streams>).

### Exemplo

Demonstra `getchar` com verificação de erros

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(void)
    {
        for (int ch; (ch = getchar()) != EOF;) // lê/imprime "abcde" de stdin
            printf("%c", ch);
    
        // Testa o motivo para atingir EOF.
        if (feof(stdin)) // se a falha foi causada pela condição de fim de arquivo
            puts("End of file reached");
        else if (ferror(stdin)) // se a falha foi causada por algum outro erro
        {
            perror("getchar()");
            fprintf(stderr, "getchar() failed in file %s at line # %d\n",
                    __FILE__, __LINE__ - 9);
            exit(EXIT_FAILURE);
        }
    
        return EXIT_SUCCESS;
    }
```

Saída possível:
```
    abcde
    End of file reached
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.21.7.6 A função getchar (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.21.7.6 A função getchar (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.21.7.6 A função getchar (p: 332)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.19.7.6 A função getchar (p: 298)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.9.7.6 A função getchar

### Veja também

[ fgetcgetc](<#/doc/io/fgetc>) | obtém um caractere de um fluxo de arquivo
(função)
[Documentação C++](<#/>) para getchar