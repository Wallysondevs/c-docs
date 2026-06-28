# getline, getwline, getdelim, getwdelim

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
ssize_t getline(char **lineptr, size_t *n, FILE *stream);
ssize_t getwline(wchar_t **lineptr, size_t *n, FILE *stream);
ssize_t getdelim(char ** restrict lineptr, size_t * restrict n,
int delimiter, FILE *stream);
ssize_t getwdelim(wchar_t ** restrict lineptr, size_t * restrict n,
wint_t delimiter, FILE * stream);
```

1) Comporta-se como getdelim(lineptr, n, '\n', stream)

2) Comporta-se como getwdelim(lineptr, n, L'\n', stream)

3) Lê do fluxo `stream` como se por [fgetc](<#/doc/io/fgetc>), até que `delimiter` seja encontrado, armazenando os caracteres no buffer de tamanho `*n` apontado por `*lineptr`, aumentando automaticamente seu tamanho como se por [realloc](<#/doc/memory/realloc>) para acomodar toda a entrada, incluindo o delimitador, e adicionando um terminador nulo. `*lineptr` pode ser nulo, caso em que `*n` é ignorado e `getline` aloca um novo buffer como se por [malloc](<#/doc/memory/malloc>). O comportamento é indefinido se `delimiter` tiver um valor fora do intervalo de `unsigned char` ou [EOF](<#/doc/io>).

4) O mesmo que (3), exceto que os caracteres são lidos como se por [fgetwc](<#/doc/io/fgetwc>) e que `delimiter` deve ser um `wchar_t` válido ou WEOF.

Se `*lineptr` não for nulo, o comportamento é indefinido se `*lineptr` não for um ponteiro que pode ser passado para [free](<#/doc/memory/free>) ou se `*n` for menor que o tamanho da memória alocada apontada por `*lineptr`.

Assim como todas as funções do TR de Memória Dinâmica, `getline` só é garantido como disponível se __STDC_ALLOC_LIB__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT2__ para a constante inteira 1 antes de incluir `stdio.h`.

### Parâmetros

- **lineptr** — ponteiro para um ponteiro para o buffer inicial ou para um ponteiro nulo
- **n** — ponteiro para o tamanho do buffer inicial
- **delimiter** — o caractere delimitador
- **stream** — fluxo de entrada válido, aberto por [fopen](<#/doc/io/fopen>)

### Valor de retorno

O número de caracteres armazenados no buffer, incluindo o delimitador, mas excluindo o terminador nulo.

Em caso de erro, retorna -1 e define [feof](<#/doc/io/feof>) ou [ferror](<#/doc/io/ferror>) no `stream`.

### Observações

Estas funções são idênticas às suas [versões POSIX](<http://pubs.opengroup.org/onlinepubs/9699919799/functions/getdelim.html>), exceto que é permitido, mas não obrigatório, definir [errno](<#/doc/error/errno>) em caso de erro.

### Exemplo

Execute este código
```c
    #ifdef __STDC_ALLOC_LIB__
    #define __STDC_WANT_LIB_EXT2__ 1
    #else
    #define _POSIX_C_SOURCE 200809L
    #endif
    
    #include <stdio.h>
    #include <stdlib.h>
    void get_y_or_n(void)
    {
        char *response = NULL;
        size_t len;
        printf("Continue? [y] n: ");
        if((getline(&response, &len, stdin) < 0) || (len && response[0] == 'n')) {
            free(response);
            exit(0);
        }
        free(response);
        return;
    }
    int main(void) 
    {
        get_y_or_n();
    }
```

Saída:
```
    Continue? [y] n:
```

### Veja também

[ fgets](<#/doc/io/fgets>) | obtém uma string de caracteres de um fluxo de arquivo
(função)
[ getsgets_s](<#/doc/io/gets>)(removido em C11)(C11) | lê uma string de caracteres de [stdin](<#/doc/io/std_streams>)
(função)
[ fgetws](<#/doc/io/fgetws>)(C95) | obtém uma string larga de um fluxo de arquivo
(função)
[ malloc](<#/doc/memory/malloc>) | aloca memória
(função)