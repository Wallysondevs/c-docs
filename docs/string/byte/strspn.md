# strspn

Definido no cabeçalho [`<string.h>`](<#/doc/string/byte>)

```c
size_t strspn( const char* dest, const char* src );
```

Retorna o comprimento do segmento inicial máximo (extensão) da string de bytes terminada em nulo apontada por dest, que consiste apenas nos caracteres encontrados na string de bytes terminada em nulo apontada por src.

O comportamento é indefinido se dest ou src não for um ponteiro para uma string de bytes terminada em nulo.

### Parâmetros

- **dest** — ponteiro para a string de bytes terminada em nulo a ser analisada
- **src** — ponteiro para a string de bytes terminada em nulo que contém os caracteres a serem procurados

### Valor de retorno

O comprimento do segmento inicial máximo que contém apenas caracteres da string de bytes terminada em nulo apontada por src.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <string.h>
    
    int main(void)
    {
        const char* string = "abcde312$#@";
        const char* low_alpha = "qwertyuiopasdfghjklzxcvbnm";
    
        size_t spnsz = strspn(string, low_alpha);
        printf("After skipping initial lowercase letters from '%s'\n"
               "The remainder is '%s'\n", string, string + spnsz);
    }
```

Saída:
```
    After skipping initial lowercase letters from 'abcde312$#@'
    The remainder is '312$#@'
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.24.5.6 A função strspn (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.24.5.6 A função strspn (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.24.5.6 A função strspn (p: 369)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.21.5.6 A função strspn (p: 332)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.11.5.6 A função strspn

### Veja também

[ strcspn](<#/doc/string/byte/strcspn>) | retorna o comprimento do segmento inicial máximo que consiste
apenas nos caracteres não encontrados em outra string de bytes
(função)
[ wcsspn](<#/doc/string/wide/wcsspn>)(C95) | retorna o comprimento do segmento inicial máximo que consiste
apenas nos caracteres largos encontrados em outra string larga
(função)
[ strpbrk](<#/doc/string/byte/strpbrk>) | encontra a primeira ocorrência de qualquer caractere de uma string em outra string
(função)
[Documentação C++](<#/>) para strspn