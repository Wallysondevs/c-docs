# fgetc, getc

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
int fgetc( FILE* stream );
int getc( FILE* stream );
```

1) Lê o próximo caractere do fluxo de entrada fornecido.

2) O mesmo que `fgetc`, exceto que se `getc` for implementado como uma macro, ele pode avaliar `stream` mais de uma vez, então o argumento correspondente nunca deve ser uma expressão com efeitos colaterais.

### Parâmetros

- **stream** — de onde ler o caractere

### Valor de retorno

Em caso de sucesso, retorna o caractere obtido como um `unsigned char` convertido para um `int`. Em caso de falha, retorna [EOF](<#/doc/io>).

Se a falha foi causada pela condição de fim de arquivo, adicionalmente define o indicador _eof_ (veja [feof()](<#/doc/io/feof>)) no fluxo. Se a falha foi causada por algum outro erro, define o indicador _error_ (veja [ferror()](<#/doc/io/ferror>)) no fluxo.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
     
    int main(void)
    {
        const char* fname = "/tmp/unique_name.txt"; // ou tmpnam(NULL);
        int is_ok = EXIT_FAILURE;
     
        FILE* fp = fopen(fname, "w+");
        if (!fp)
        {
            perror("Falha na abertura do arquivo");
            return is_ok;
        }
        fputs("Hello, world!\n", fp);
        rewind(fp);
     
        int c; // nota: int, não char, necessário para lidar com EOF
        while ((c = fgetc(fp)) != EOF) // laço de leitura de arquivo de E/S padrão C
            putchar(c);
     
        if (ferror(fp))
            puts("Erro de E/S ao ler");
        else if (feof(fp))
        {
            puts("Fim do arquivo alcançado com sucesso");
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
    Fim do arquivo alcançado com sucesso
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.21.7.1 A função fgetc (p: TBD) 

    

  * 7.21.7.5 A função getc (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.21.7.1 A função fgetc (p: 240-241) 

    

  * 7.21.7.5 A função getc (p: 242) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.21.7.1 A função fgetc (p: 330) 

    

  * 7.21.7.5 A função getc (p: 332) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.19.7.1 A função fgetc (p: 296) 

    

  * 7.19.7.5 A função getc (p: 297-298) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.9.7.1 A função fgetc 

    

  * 4.9.7.5 A função getc 

### Veja também

[ getchar](<#/doc/io/getchar>) | lê um caractere de [stdin](<#/doc/io/std_streams>)
(função)
[ getsgets_s](<#/doc/io/gets>)(removido em C11)(C11) | lê uma string de caracteres de [stdin](<#/doc/io/std_streams>)
(função)
[ fputcputc](<#/doc/io/putc>) | escreve um caractere em um fluxo de arquivo
(função)
[ ungetc](<#/doc/io/ungetc>) | coloca um caractere de volta em um fluxo de arquivo
(função)
Documentação C++ para fgetc, getc