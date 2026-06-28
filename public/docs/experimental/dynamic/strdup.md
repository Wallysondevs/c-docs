# strdup

Definido no cabeçalho [`<string.h>`](<#/doc/string/byte>)

```c
char * strdup( const char *str1 );
```

Retorna um ponteiro para uma string de bytes terminada em nulo, que é uma duplicata da string apontada por `str1`. O ponteiro retornado deve ser passado para [free](<#/doc/memory/free>) para evitar um vazamento de memória.

Se ocorrer um erro, um ponteiro nulo é retornado e [errno](<#/doc/error/errno>) pode ser definido.

Assim como todas as funções do TR de Memória Dinâmica, `strdup` tem sua disponibilidade garantida apenas se __STDC_ALLOC_LIB__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT2__ para a constante inteira 1 antes de incluir `string.h`.

### Parâmetros

- **str1** — ponteiro para a string de bytes terminada em nulo a ser duplicada

### Valor de retorno

Um ponteiro para a string recém-alocada, ou um ponteiro nulo se um erro ocorreu.

### Notas

A função é idêntica à [POSIX strdup](<http://pubs.opengroup.org/onlinepubs/9699919799/functions/strdup.html>).

### Exemplo

Execute este código
```
    #ifdef __STDC_ALLOC_LIB__
    #define __STDC_WANT_LIB_EXT2__ 1
    #else
    #define _POSIX_C_SOURCE 200809L
    #endif
    
    #include <string.h>
    #include <assert.h>
    #include <stdlib.h>
    
    int main(void)
    {
        const char *s1 = "String";
        char *s2 = strdup(s1);
        assert(strcmp(s1, s2) == 0);
        free(s2);
    }
```

### Veja também

[ strndup](<#/doc/experimental/dynamic/strndup>)(TR de memória dinâmica) | aloca uma cópia de uma string até um tamanho especificado
(função)
[ strcpystrcpy_s](<#/doc/string/byte/strcpy>)(C11) | copia uma string para outra
(função)
[ malloc](<#/doc/memory/malloc>) | aloca memória
(função)