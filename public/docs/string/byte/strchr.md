# strchr

Definido no cabeçalho [`<string.h>`](<#/doc/string/byte>)

```c
char* strchr( const char* str, int ch );
/*QChar*/ *strchr( /*QChar*/ *str, int ch );  // desde C23
```

1) Encontra a primeira ocorrência de ch (após conversão para char como se por (char)ch) na string de bytes terminada em nulo apontada por str (cada caractere interpretado como unsigned char). O caractere nulo terminador é considerado parte da string e pode ser encontrado ao procurar por '\0'.

2) Função genérica de tipo equivalente a (1). Seja `T` um tipo de objeto caractere não qualificado.

    * Se `str` for do tipo const T*, o tipo de retorno é const char*.
    * Caso contrário, se `str` for do tipo T*, o tipo de retorno é char*.
    * Caso contrário, o comportamento é indefinido.

Se uma definição de macro de cada uma dessas funções genéricas for suprimida para acessar uma função real (por exemplo, se (strchr) ou um ponteiro de função for usado), a declaração de função real (1) se torna visível.

O comportamento é indefinido se str não for um ponteiro para uma string de bytes terminada em nulo.

### Parâmetros

- **str** — ponteiro para a string de bytes terminada em nulo a ser analisada
- **ch** — caractere a ser procurado

### Valor de retorno

Ponteiro para o caractere encontrado em str, ou ponteiro nulo se nenhum caractere for encontrado.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <string.h>
     
    int main(void)
    {
        const char *str = "Try not. Do, or do not. There is no try.";
        char target = 'T';
        const char* result = str;
     
        while((result = strchr(result, target)) != NULL)
        {
            printf("Found '%c' starting at '%s'\n", target, result);
            ++result; // Increment result, otherwise we'll find target at the same location
        }
    }
```

Saída:
```
    Found 'T' starting at 'Try not. Do, or do not. There is no try.'
    Found 'T' starting at 'There is no try.'
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    * 7.24.5.2 A função strchr (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    * 7.24.5.2 A função strchr (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    * 7.24.5.2 A função strchr (p: 367-368)

  * Padrão C99 (ISO/IEC 9899:1999):

    * 7.21.5.2 A função strchr (p: 330)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    * 4.11.5.2 A função strchr

### Veja também

[ memchr](<#/doc/string/byte/memchr>) | procura em um array pela primeira ocorrência de um caractere
(função)
[ strrchr](<#/doc/string/byte/strrchr>) | encontra a última ocorrência de um caractere
(função)
[ strpbrk](<#/doc/string/byte/strpbrk>) | encontra a primeira localização de qualquer caractere de uma string, em outra string
(função)
[Documentação C++](<#/>) para strchr