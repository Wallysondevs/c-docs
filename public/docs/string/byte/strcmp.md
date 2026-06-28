# strcmp

Definido no cabeçalho [`<string.h>`](<#/doc/string/byte>)

```c
int strcmp( const char* lhs, const char* rhs );
```

  
Compara duas strings de bytes terminadas em nulo lexicograficamente. 

O sinal do resultado é o sinal da diferença entre os valores do primeiro par de caracteres (ambos interpretados como unsigned char) que diferem nas strings sendo comparadas. 

O comportamento é indefinido se lhs ou rhs não forem ponteiros para strings de bytes terminadas em nulo. 

### Parâmetros

lhs, rhs  |  \-  |  ponteiros para as strings de bytes terminadas em nulo a serem comparadas   
  
### Valor de retorno

Valor negativo se lhs aparecer antes de rhs na ordem lexicográfica. 

Zero se lhs e rhs forem iguais. 

Valor positivo se lhs aparecer depois de rhs na ordem lexicográfica. 

### Notas

Esta função não é sensível à localidade, ao contrário de [strcoll](<#/doc/string/byte/strcoll>) e [strxfrm](<#/doc/string/byte/strxfrm>). 

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <string.h>
    
    void demo(const char* lhs, const char* rhs)
    {
        const int rc = strcmp(lhs, rhs);
        const char* rel = rc < 0 ? "precedes" : rc > 0 ? "follows" : "equals";
        printf("[%s] %s [%s]\n", lhs, rel, rhs);
    }
    
    int main(void)
    {
        const char* string = "Hello World!";
        demo(string, "Hello!");
        demo(string, "Hello");
        demo(string, "Hello there");
        demo("Hello, everybody!" + 12, "Hello, somebody!" + 11);
    }
```

Saída: 
```
    [Hello World!] precedes [Hello!]
    [Hello World!] follows [Hello]
    [Hello World!] precedes [Hello there]
    [body!] equals [body!]
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.24.4.2 A função strcmp (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.24.4.2 A função strcmp (p: TBD) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.24.4.2 A função strcmp (p: 365-366) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.21.4.2 A função strcmp (p: 328-329) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.11.4.2 A função strcmp 

### Veja também

[ strncmp](<#/doc/string/byte/strncmp>) |  compara uma certa quantidade de caracteres de duas strings   
(função)  
[ wcscmp](<#/doc/string/wide/wcscmp>)(C95) |  compara duas strings largas   
(função)  
[ memcmp](<#/doc/string/byte/memcmp>) |  compara dois buffers   
(função)  
[ strcoll](<#/doc/string/byte/strcoll>) |  compara duas strings de acordo com a localidade atual   
(função)  
[Documentação C++](<#/>) para strcmp