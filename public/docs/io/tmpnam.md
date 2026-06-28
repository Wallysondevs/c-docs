# tmpnam, tmpnam_s

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
char *tmpnam( char *filename );
errno_t tmpnam_s(char *filename_s, rsize_t maxsize);  // desde C11
#define TMP_MAX /*unspecified*/
#define TMP_MAX_S /*unspecified*/  // desde C11
#define L_tmpnam /*unspecified*/
#define L_tmpnam_s /*unspecified*/  // desde C11
```

1) Cria um nome de arquivo válido e único (não mais longo que [L_tmpnam](<#/doc/io>) caracteres) e o armazena na string de caracteres apontada por filename. A função é capaz de gerar até [TMP_MAX](<#/doc/io>) nomes de arquivo únicos, mas alguns ou todos eles podem já estar em uso no sistema de arquivos e, portanto, não serem valores de retorno adequados.

2) O mesmo que (1), exceto que até TMP_MAX_S nomes podem ser gerados, não mais longos que L_tmpnam_s caracteres, e os seguintes erros são detectados em tempo de execução e chamam a função [constraint handler](<#/doc/error/set_constraint_handler_s>) atualmente instalada:

*   filename_s é um ponteiro nulo
*   maxsize é maior que RSIZE_MAX
*   maxsize é menor que a string do nome de arquivo gerado

    Assim como todas as funções com verificação de limites, `tmpnam_s` tem sua disponibilidade garantida apenas se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir [`<stdio.h>`](<#/doc/io>).

`tmpnam` e `tmpnam_s` modificam o estado estático (que pode ser compartilhado entre essas funções) e não são obrigadas a ser thread-safe.

### Parâmetros

filename | \- | ponteiro para o array de caracteres capaz de armazenar pelo menos [L_tmpnam](<#/doc/io>) bytes, a ser usado como buffer de resultado. Se um ponteiro nulo for passado, um ponteiro para um buffer estático interno é retornado.
filename_s | \- | ponteiro para o array de caracteres capaz de armazenar pelo menos L_tmpnam_s bytes, a ser usado como buffer de resultado.
maxsize | \- | número máximo de caracteres que a função tem permissão para escrever (tipicamente o tamanho do array `filename_s`).

### Valor de retorno

1) filename se filename não for um ponteiro nulo. Caso contrário, um ponteiro para um buffer estático interno é retornado. Se nenhum nome de arquivo adequado puder ser gerado, um ponteiro nulo é retornado.

2) Retorna zero e escreve o nome do arquivo em filename_s em caso de sucesso. Em caso de erro, retorna um valor diferente de zero e escreve o caractere nulo em filename_s[0] (somente se filename_s não for nulo e maxsize não for zero e não for maior que RSIZE_MAX).

### Observações

Embora os nomes gerados por `tmpnam` sejam difíceis de adivinhar, é possível que um arquivo com esse nome seja criado por outro processo entre o momento em que `tmpnam` retorna e o momento em que este programa tenta usar o nome retornado para criar um arquivo. A função padrão [tmpfile](<#/doc/io/tmpfile>) e a função POSIX [`mkstemp`](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/mkdtemp.html>) não apresentam esse problema (criar um diretório único usando apenas a biblioteca padrão C ainda requer o uso de `tmpnam`).

Sistemas POSIX adicionalmente definem a função de nome similar [`tempnam`](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/tempnam.html>), que oferece a escolha de um diretório (que por padrão é a macro [`P_tmpdir`](<https://pubs.opengroup.org/onlinepubs/9699919799/basedefs/stdio.h.html>) definida opcionalmente).

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
    #include <string.h>
    
    int main(void)
    {
        // Nota: o compilador/linker pode emitir um aviso de segurança, ex: GCC:
        // "aviso: o uso de `tmpnam` é perigoso, é melhor usar `mkstemp`"
        char* name1 = tmpnam(NULL);
        printf("nome de arquivo temporário: %s\n", name1);
    
        char name2[L_tmpnam];
        if (tmpnam(name2))
            printf("nome de arquivo temporário: %s\n", name2);
    
        // POSIX oferece mkstemp. A seguinte declaração pode ser
        // necessária, pois mkstemp está ausente no <stdlib.h> padrão do C.
        int mkstemp(char*);
    
        char name3[] = "/tmp/fileXXXXXX"; // pelo menos seis 'X' são necessários ^_^
        int file_descriptor = mkstemp(name3);
        if (file_descriptor != -1)
            printf("nome de arquivo temporário: %s\n", name3);
        else
            perror("mkstemp");
    }
```

Saída possível:
```
    temporary file name: /tmp/file90dLlR
    temporary file name: /tmp/fileY9LWAg
    temporary file name: /tmp/filexgv8PF
```

### Referências

*   Padrão C23 (ISO/IEC 9899:2024):

    *   7.21.4.4 A função tmpnam (p: TBD)

    *   K.3.5.1.2 A função tmpnam_s (p: TBD)

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.21.4.4 A função tmpnam (p: 222)

    *   K.3.5.1.2 A função tmpnam_s (p: 427-428)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.21.4.4 A função tmpnam (p: 303-304)

    *   K.3.5.1.2 A função tmpnam_s (p: 587-588)

*   Padrão C99 (ISO/IEC 9899:1999):

    *   7.19.4.4 A função tmpnam (p: 269-270)

*   Padrão C89/C90 (ISO/IEC 9899:1990):

    *   4.9.4.4 A função tmpnam

### Veja também

[ tmpfiletmpfile_s](<#/doc/io/tmpfile>)(C11) | retorna um ponteiro para um arquivo temporário
(função)
[Documentação C++](<#/>) para tmpnam