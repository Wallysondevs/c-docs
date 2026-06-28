# strndup

Definido no cabeçalho [`<string.h>`](<#/doc/string/byte>)

```c
char *strndup( const char *str, size_t size );
```

Retorna um ponteiro para uma string de bytes terminada em nulo, que contém cópias de no máximo `size` bytes da string apontada por `str`. Se o terminador nulo não for encontrado nos primeiros `size` bytes, ele é adicionado à string duplicada.

O ponteiro retornado deve ser passado para [free](<#/doc/memory/free>) para evitar um vazamento de memória.

Se ocorrer um erro, um ponteiro nulo é retornado e [errno](<#/doc/error/errno>) pode ser definido.

Assim como todas as funções do TR de Memória Dinâmica, `strndup` tem sua disponibilidade garantida apenas se __STDC_ALLOC_LIB__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT2__ para a constante inteira 1 antes de incluir `string.h`.

### Parâmetros

- **str** — ponteiro para a string de bytes terminada em nulo a ser duplicada
- **size** — número máximo de bytes a serem copiados de `str`

### Valor de retorno

Um ponteiro para a string recém-alocada, ou um ponteiro nulo se um erro ocorreu.

### Observações

A função é idêntica à [POSIX strndup](<http://pubs.opengroup.org/onlinepubs/9699919799/functions/strdup.html>), exceto que é permitido, mas não obrigatório, definir [errno](<#/doc/error/errno>) em caso de erro.

### Exemplo

Execute este código
```
    #ifdef __STDC_ALLOC_LIB__
    #define __STDC_WANT_LIB_EXT2__ 1
    #else
    #define _POSIX_C_SOURCE 200809L
    #endif
    
    #include <string.h>
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(void)
    {
        const char *s1 = "String";
        char *s2 = strndup(s1, 2);
        printf("strndup(\"String\", 2) == %s\n", s2);
        free(s2);
    }
```

Saída:
```
    strndup("String", 2) == St
```

### Veja também

[ strdup](<#/doc/experimental/dynamic/strdup>)(TR de memória dinâmica) | aloca uma cópia de uma string
(função)
[ strncpystrncpy_s](<#/doc/string/byte/strncpy>)(C11) | copia uma certa quantidade de caracteres de uma string para outra
(função)
[ malloc](<#/doc/memory/malloc>) | aloca memória
(função)