# perror

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
void perror( const char *s );
```

  
Imprime uma descrição textual do código de erro atualmente armazenado na variável de sistema [errno](<#/doc/error/errno>) para [stderr](<#/doc/io/std_streams>).

A descrição é formada pela concatenação dos seguintes componentes:

  * o conteúdo da string de bytes terminada em nulo apontada por `s`, seguido por ": " (a menos que `s` seja um ponteiro nulo ou o caractere apontado por `s` seja o caractere nulo)
  * string de mensagem de erro definida pela implementação descrevendo o código de erro armazenado em `errno`, seguido por '\n'. A string da mensagem de erro é idêntica ao resultado de [strerror](<#/doc/string/byte/strerror>)(errno).

### Parâmetros

s  |  \-  |  ponteiro para uma string terminada em nulo com mensagem explicativa   
  
### Valor de retorno

(nenhum)

### Exemplo

Execute este código
```c
    #include <stdio.h>
    
    int main(void)
    {
        FILE *f = fopen("non_existent", "r");
        if (f == NULL) {
            perror("fopen() failed");
        } else {
            fclose(f);
        }
    }
```

Saída possível:
```
    fopen() failed: No such file or directory
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.21.10.4 A função perror (p: 339) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.19.10.4 A função perror (p: 305) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.9.10.4 A função perror 

### Veja também

[ strerrorstrerror_sstrerrorlen_s](<#/doc/string/byte/strerror>)(C11)(C11) |  retorna uma versão textual de um dado código de erro   
(função)  
[Documentação C++](<#/>) para perror