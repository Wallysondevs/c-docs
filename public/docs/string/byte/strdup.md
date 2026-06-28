# strdup

Definido no cabeçalho [`<string.h>`](<#/doc/string/byte>)

```c
char *strdup( const char *src );  // desde C23
```

  
Retorna um ponteiro para uma string de bytes terminada em nulo, que é uma duplicata da string apontada por `src`. O espaço para a nova string é obtido como se [malloc](<#/doc/memory/malloc>) tivesse sido invocado. O ponteiro retornado deve ser passado para [free](<#/doc/memory/free>) para evitar um vazamento de memória. 

Se ocorrer um erro, um ponteiro nulo é retornado e [errno](<#/doc/error/errno>) pode ser definido. 

### Parâmetros

src  |  \-  |  ponteiro para a string de bytes terminada em nulo a ser duplicada   
  
### Valor de retorno

Um ponteiro para a string recém-alocada, ou um ponteiro nulo se um erro ocorreu. 

### Notas

A função é idêntica à [strdup POSIX](<http://pubs.opengroup.org/onlinepubs/9699919799/functions/strdup.html>). 

### Exemplo

Execute este código
```c
    #include <string.h>
    #include <stdio.h>
    #include <stdlib.h>
     
    int main(void)
    {
        const char *s1 = "Duplicate me!";
        char *s2 = strdup(s1);
        printf("s2 = \"%s\"\n", s2);
        free(s2);
    }
```

Saída: 
```
    s2 = "Duplicate me!"
```

### Veja também

[ strndup](<#/doc/string/byte/strndup>)(C23) |  aloca uma cópia de uma string de tamanho especificado   
(função)  
[ strcpystrcpy_s](<#/doc/string/byte/strcpy>)(C11) |  copia uma string para outra   
(função)  
[ malloc](<#/doc/memory/malloc>) |  aloca memória   
(função)  
[ free](<#/doc/memory/free>) |  desaloca memória previamente alocada   
(função)