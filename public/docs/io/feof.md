# feof

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
int feof( FILE *stream );
```

Verifica se o fim do fluxo de arquivo fornecido foi atingido.

### Parâmetros

- **stream** — o fluxo de arquivo a ser verificado

### Valor de retorno

valor diferente de zero se o fim do fluxo foi atingido, caso contrário ​0​

### Observações

Esta função apenas relata o estado do fluxo conforme relatado pela operação de E/S mais recente, ela não examina a fonte de dados associada. Por exemplo, se a operação de E/S mais recente foi um [fgetc](<#/doc/io/fgetc>), que retornou o último byte de um arquivo, `feof` retorna zero. O próximo [fgetc](<#/doc/io/fgetc>) falha e altera o estado do fluxo para _fim de arquivo_. Somente então `feof` retorna um valor diferente de zero.

No uso típico, o processamento do fluxo de entrada para em qualquer erro; `feof` e [ferror](<#/doc/io/ferror>) são então usados para distinguir entre diferentes condições de erro.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
     
    int main(void)
    {
        const char* fname = "/tmp/unique_name.txt"; // or tmpnam(NULL);
        int is_ok = EXIT_FAILURE;
     
        FILE* fp = fopen(fname, "w+");
        if (!fp)
        {
            perror("File opening failed");
            return is_ok;
        }
        fputs("Hello, world!\n", fp);
        rewind(fp);
     
        int c; // note: int, not char, required to handle EOF
        while ((c = fgetc(fp)) != EOF) // standard C I/O file reading loop
            putchar(c);
     
        if (ferror(fp))
            puts("I/O error when reading");
        else if (feof(fp))
        {
            puts("End of file is reached successfully");
            is_ok = EXIT_SUCCESS;
        }
     
        fclose(fp);
        remove(fname);
        return is_ok;
    }
```

Saída possível:
```
    Hello, world!
    End of file is reached successfully
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.21.10.2 A função feof (p: 339)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.19.10.2 A função feof (p: 305)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.9.10.2 A função feof

### Veja também

[ clearerr](<#/doc/io/clearerr>) | limpa erros
(função)
[ perror](<#/doc/io/perror>) | exibe uma string de caracteres correspondente ao erro atual para [stderr](<#/doc/io/std_streams>)
(função)
[ ferror](<#/doc/io/ferror>) | verifica por um erro de arquivo
(função)
[Documentação C++](<#/>) para feof