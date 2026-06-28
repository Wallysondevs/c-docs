# strncmp

Definido no cabeçalho [`<string.h>`](<#/doc/string/byte>)

```c
int strncmp( const char* lhs, const char* rhs, size_t count );
```

  
Compara no máximo `count` caracteres de dois arrays possivelmente terminados em nulo. A comparação é feita lexicograficamente. Caracteres após o caractere nulo não são comparados. 

O sinal do resultado é o sinal da diferença entre os valores do primeiro par de caracteres (ambos interpretados como `unsigned char`) que diferem nos arrays sendo comparados. 

O comportamento é indefinido quando o acesso ocorre além do final de qualquer um dos arrays `lhs` ou `rhs`. O comportamento é indefinido quando `lhs` ou `rhs` é o ponteiro nulo. 

### Parâmetros

lhs, rhs  |  \-  |  ponteiros para os arrays possivelmente terminados em nulo a serem comparados   
count  |  \-  |  número máximo de caracteres a serem comparados   
  
### Valor de retorno

Valor negativo se `lhs` aparecer antes de `rhs` na ordem lexicográfica. 

Zero se `lhs` e `rhs` forem iguais na comparação, ou se `count` for zero. 

Valor positivo se `lhs` aparecer depois de `rhs` na ordem lexicográfica. 

### Observações

Esta função não é sensível à localidade, ao contrário de [strcoll](<#/doc/string/byte/strcoll>) e [strxfrm](<#/doc/string/byte/strxfrm>). 

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <string.h>
     
    void demo(const char* lhs, const char* rhs, int sz)
    {
        const int rc = strncmp(lhs, rhs, sz);
        if (rc < 0)
            printf("First %d chars of [%s] precede [%s]\n", sz, lhs, rhs);
        else if (rc > 0)
            printf("First %d chars of [%s] follow [%s]\n", sz, lhs, rhs);
        else
            printf("First %d chars of [%s] equal [%s]\n", sz, lhs, rhs);
    }
    int main(void)
    {
        const char* string = "Hello World!";
        demo(string, "Hello!", 5);
        demo(string, "Hello", 10);
        demo(string, "Hello there", 10);
        demo("Hello, everybody!" + 12, "Hello, somebody!" + 11, 5);
    }
```

Saída: 
```
    First 5 chars of [Hello World!] equal [Hello!]
    First 10 chars of [Hello World!] follow [Hello]
    First 10 chars of [Hello World!] precede [Hello there]
    First 5 chars of [body!] equal [body!]
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.24.4.4 A função strncmp (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.24.4.4 A função strncmp (p: TBD) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.24.4.4 A função strncmp (p: 366) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.21.4.4 A função strncmp (p: 329) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.11.4.4 A função strncmp 

### Veja também

[ strcmp](<#/doc/string/byte/strcmp>) |  compara duas strings   
(função)  
[ wcsncmp](<#/doc/string/wide/wcsncmp>)(C95) |  compara uma certa quantidade de caracteres de duas strings largas   
(função)  
[ memcmp](<#/doc/string/byte/memcmp>) |  compara dois buffers   
(função)  
[ strcoll](<#/doc/string/byte/strcoll>) |  compara duas strings de acordo com a localidade atual   
(função)  
[Documentação C++](<#/>) para strncmp