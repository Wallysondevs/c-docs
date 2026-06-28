# strcspn

Definido no cabeçalho [`<string.h>`](<#/doc/string/byte>)

```c
size_t strcspn( const char *dest, const char *src );
```

Retorna o comprimento do segmento inicial máximo da string de bytes terminada em nulo apontada por `dest`, que consiste apenas nos caracteres _não_ encontrados na string de bytes terminada em nulo apontada por `src`.

O comportamento é indefinido se `dest` ou `src` não for um ponteiro para uma string de bytes terminada em nulo.

### Parâmetros

- **dest** — ponteiro para a string de bytes terminada em nulo a ser analisada
- **src** — ponteiro para a string de bytes terminada em nulo que contém os caracteres a serem procurados

### Valor de retorno

O comprimento do segmento inicial máximo que contém apenas caracteres não encontrados na string de bytes terminada em nulo apontada por `src`

### Observações

O nome da função significa "complementary span" (extensão complementar) porque a função procura por caracteres não encontrados em `src`, ou seja, o complemento de `src`.

### Exemplo

Execute este código
```
    #include <string.h>
    #include <stdio.h>
    
    int main(void)
    {
        const char *string = "abcde312$#@";
        const char *invalid = "*$#";
    
        size_t valid_len = strcspn(string, invalid);
        if(valid_len != strlen(string))
           printf("'%s' contains invalid chars starting at position %zu\n",
                   string, valid_len);
    }
```

Saída:
```
    'abcde312$#@' contains invalid chars starting at position 8
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.24.5.3 A função strcspn (p: 368)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.21.5.3 A função strcspn (p: 331)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.11.5.3 A função strcspn

### Veja também

[ strspn](<#/doc/string/byte/strspn>) | retorna o comprimento do segmento inicial máximo que consiste
apenas nos caracteres encontrados em outra string de bytes
(função)
[ wcscspn](<#/doc/string/wide/wcscspn>)(C95) | retorna o comprimento do segmento inicial máximo que consiste
apenas nos caracteres largos _não_ encontrados em outra string larga
(função)
[ strpbrk](<#/doc/string/byte/strpbrk>) | encontra a primeira ocorrência de qualquer caractere de uma string, em outra string
(função)
[Documentação C++](<#/>) para strcspn