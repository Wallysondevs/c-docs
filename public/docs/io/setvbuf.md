# setvbuf

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
int setvbuf( FILE * stream, char * buffer,
int mode, size_t size );  // ate C99
int setvbuf( FILE *restrict stream, char *restrict buffer,
int mode, size_t size );  // desde C99
#define _IOFBF /*unspecified*/
#define _IOLBF /*unspecified*/
#define _IONBF /*unspecified*/
```

Altera o modo de buffer do fluxo de arquivo `stream` fornecido, conforme indicado pelo argumento `mode`. Além disso,

*   Se `buffer` for um ponteiro nulo, redimensiona o buffer interno para `size`.
*   Se `buffer` não for um ponteiro nulo, instrui o fluxo a usar o buffer fornecido pelo usuário de tamanho `size` começando em `buffer`. O fluxo deve ser fechado (com [fclose](<#/doc/io/fclose>)) antes que o [tempo de vida](<#/doc/language/lifetime>) do array apontado por `buffer` termine. O conteúdo do array após uma chamada bem-sucedida a `setvbuf` é indeterminado e qualquer tentativa de usá-lo é comportamento indefinido.

### Parâmetros

- **stream** — o fluxo de arquivo para o qual definir o buffer
- **buffer** — ponteiro para um buffer para o fluxo usar ou ponteiro nulo para alterar apenas o tamanho e o modo
- **mode** — modo de buffer a ser usado. Pode ser um dos seguintes valores: | [_IOFBF](<#/doc/io>) | bufferização completa
[_IOLBF](<#/doc/io>) | bufferização por linha
[_IONBF](<#/doc/io>) | sem bufferização
- **size** — tamanho do buffer

### Valor de retorno

`0` em caso de sucesso ou diferente de zero em caso de falha.

### Observações

Esta função só pode ser usada depois que `stream` tiver sido associado a um arquivo aberto, mas antes de qualquer outra operação (além de uma chamada falha a [setbuf](<#/doc/io/setbuf>)/`setvbuf`).

Nem todos os `size` bytes serão necessariamente usados para bufferização: o tamanho real do buffer é geralmente arredondado para baixo para um múltiplo de 2, um múltiplo do tamanho da página, etc.

Em muitas implementações, a bufferização por linha está disponível apenas para fluxos de entrada de terminal.

Um erro comum é definir o buffer de stdin ou stdout para um array cujo tempo de vida termina antes que o programa seja encerrado:
```c
    int main(void) {
        char buf[BUFSIZ];
        setbuf(stdin, buf);
    } // tempo de vida de buf termina, comportamento indefinido
```

O tamanho de buffer padrão [BUFSIZ](<#/doc/io>) é esperado para ser o tamanho de buffer mais eficiente para E/S de arquivo na implementação, mas [fstat](<http://pubs.opengroup.org/onlinepubs/9699919799/functions/fstat.html>) POSIX frequentemente fornece uma estimativa melhor.

### Exemplo

Um caso de uso para alterar o tamanho do buffer é quando um tamanho melhor é conhecido. (Este exemplo usa algumas funções POSIX, por exemplo, [`fileno`](<https://pubs.opengroup.org/onlinepubs/7908799/xsh/fileno.html>). Veja também SO: [#1](<https://stackoverflow.com/questions/15749184/fileno-not-available>) e [#2](<https://stackoverflow.com/questions/44622827/why-am-i-getting-error-implicit-declaration-of-function-fileno-when-i-try-t>)).

Execute este código
```c
    // Torna algumas funções POSIX, como `int fileno(FILE*)`, visíveis:
    #define _POSIX_SOURCE
     
    #include <stdio.h>
    #include <stdlib.h>
    #include <sys/stat.h>
     
    int main(void)
    {
        FILE* fp = fopen("/tmp/test.txt", "w+");
        if (fp == NULL)
        {
            perror("fopen");
            return EXIT_FAILURE;
        }
     
        struct stat stats;
        if (fstat(fileno(fp), &stats) == -1) // Apenas POSIX
        {
            perror("fstat");
            return EXIT_FAILURE;
        }
     
        printf("BUFSIZ is %d, but optimal block size is %ld\n", BUFSIZ, stats.st_blksize);
        if (setvbuf(fp, NULL, _IOFBF, stats.st_blksize) != 0)
        {
            perror("setvbuf failed"); // A versão POSIX define errno
            return EXIT_FAILURE;
        }
     
        int ch;
        while((ch=fgetc(fp)) != EOF); // lê o arquivo inteiro: use truss/strace para
                                      // observar as chamadas de sistema read(2) usadas
     
        fclose(fp);
        return EXIT_SUCCESS;
    }
```

Saída possível:
```
    BUFSIZ is 8192, but optimal block size is 65536
```

### Referências

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.21.5.6 A função setvbuf (p: 225)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.21.5.6 A função setvbuf (p: 308)

*   Padrão C99 (ISO/IEC 9899:1999):

    *   7.19.5.6 A função setvbuf (p: 273-274)

*   Padrão C89/C90 (ISO/IEC 9899:1990):

    *   4.9.5.6 A função setvbuf

### Veja também

[ setbuf](<#/doc/io/setbuf>) | define o buffer para um fluxo de arquivo
(função)
[documentação C++](<#/>) para setvbuf