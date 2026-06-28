# strstr

Definido no cabeçalho [`<string.h>`](<#/doc/string/byte>)

```c
char* strstr( const char* str, const char* substr );
/*QChar*/* strstr( /*QChar*/* str, const char* substr );  // desde C23
```

1) Encontra a primeira ocorrência da string de bytes terminada em nulo apontada por substr na string de bytes terminada em nulo apontada por str. Os caracteres nulos de terminação não são comparados.

2) Função genérica de tipo equivalente a (1). Seja `T` um tipo de objeto caractere não qualificado.

    * Se `str` for do tipo const T*, o tipo de retorno é const char*.
    * Caso contrário, se `str` for do tipo T*, o tipo de retorno é char*.
    * Caso contrário, o comportamento é indefinido.

Se uma definição de macro de cada uma dessas funções genéricas for suprimida para acessar uma função real (por exemplo, se (strstr) ou um ponteiro de função for usado), a declaração de função real (1) se torna visível.

O comportamento é indefinido se str ou substr não for um ponteiro para uma string de bytes terminada em nulo.

### Parâmetros

- **str** — ponteiro para a string de bytes terminada em nulo a ser examinada
- **substr** — ponteiro para a string de bytes terminada em nulo a ser procurada

### Valor de retorno

Ponteiro para o primeiro caractere da substring encontrada em str, ou um ponteiro nulo se tal substring não for encontrada. Se substr apontar para uma string vazia, str é retornado.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <string.h>
    
    void find_str(char const* str, char const* substr)
    {
        char const* pos = strstr(str, substr);
        if (pos)
            printf(
                "Found the string [%s] in [%s] at position %td\n",
                substr, str, pos - str
            );
        else
            printf(
                "The string [%s] was not found in [%s]\n",
                substr, str
            );
    }
    
    int main(void)
    {
        char const* str = "one two three";
        find_str(str, "two");
        find_str(str, "");
        find_str(str, "nine");
        find_str(str, "n");
    
        return 0;
    }
```

Saída:
```
    Found the string [two] in [one two three] at position 4
    Found the string [] in [one two three] at position 0
    The string [nine] was not found in [one two three]
    Found the string [n] in [one two three] at position 1
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    * 7.24.5.7 A função strstr (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    * 7.24.5.7 A função strstr (p: 269)

  * Padrão C11 (ISO/IEC 9899:2011):

    * 7.24.5.7 A função strstr (p: 369)

  * Padrão C99 (ISO/IEC 9899:1999):

    * 7.21.5.7 A função strstr (p: 332)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    * 4.11.5.7 A função strstr

### Veja também

[ strchr](<#/doc/string/byte/strchr>) | encontra a primeira ocorrência de um caractere
(função)
[ strrchr](<#/doc/string/byte/strrchr>) | encontra a última ocorrência de um caractere
(função)
[Documentação C++](<#/>) para strstr