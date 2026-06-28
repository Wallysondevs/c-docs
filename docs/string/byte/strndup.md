# strndup

Definido no cabeçalho [`<string.h>`](<#/doc/string/byte>)

```c
char *strndup( const char *src, size_t size );  // desde C23
```

  
Retorna um ponteiro para uma string de bytes terminada em nulo, que contém cópias de no máximo `size` bytes da string apontada por `src`. O espaço para a nova string é obtido como se [malloc](<#/doc/memory/malloc>) tivesse sido chamado. Se o terminador nulo não for encontrado nos primeiros `size` bytes, ele é anexado à string duplicada.

O ponteiro retornado deve ser passado para [free](<#/doc/memory/free>) para evitar um vazamento de memória.

Se ocorrer um erro, um ponteiro nulo é retornado e [errno](<#/doc/error/errno>) pode ser definido.

### Parâmetros

src  |  \-  |  ponteiro para a string de bytes terminada em nulo a ser duplicada   
size  |  \-  |  número máximo de bytes a copiar de `src`  
  
### Valor de retorno

Um ponteiro para a string recém-alocada, ou um ponteiro nulo se ocorreu um erro.

### Observações

A função é idêntica à [POSIX strndup](<http://pubs.opengroup.org/onlinepubs/9699919799/functions/strdup.html>), exceto que é permitido, mas não obrigatório, definir [errno](<#/doc/error/errno>) em caso de erro.

### Exemplo

Execute este código
```c
    #include <string.h>
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(void)
    {
        const size_t n = 3;
    
        const char *src = "Replica";
        char *dup = strndup(src, n);
        printf("strndup(\"%s\", %lu) == \"%s\"\n", src, n, dup);
        free(dup);
    
        src = "Hi";
        dup = strndup(src, n);
        printf("strndup(\"%s\", %lu) == \"%s\"\n", src, n, dup);
        free(dup);
    
        const char arr[] = {'A','B','C','D'}; // NB: no trailing '\0'
        dup = strndup(arr, n);
        printf("strndup({'A','B','C','D'}, %lu) == \"%s\"\n", n, dup);
        free(dup);
    }
```

Saída:
```
    strndup("Replica", 3) == "Rep"
    strndup("Hi", 3) == "Hi"
    strndup({'A','B','C','D'}, 3) == "ABC"
```

### Veja também

[ strdup](<#/doc/string/byte/strdup>)(C23) |  aloca uma cópia de uma string   
(função)  
[ strcpystrcpy_s](<#/doc/string/byte/strcpy>)(C11) |  copia uma string para outra   
(função)  
[ malloc](<#/doc/memory/malloc>) |  aloca memória   
(função)  
[ free](<#/doc/memory/free>) |  desaloca memória previamente alocada   
(função)