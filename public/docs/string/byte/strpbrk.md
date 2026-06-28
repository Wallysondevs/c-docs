# strpbrk

Definido no cabeçalho [`<string.h>`](<#/doc/string/byte>)

```c
char *strpbrk( const char *dest, const char *breakset );
/*QChar*/ *strpbrk( /*QChar*/ *dest, const char *breakset );  // desde C23
```

1 ) Examina a string de bytes terminada em nulo apontada por dest em busca de qualquer caractere da string de bytes terminada em nulo apontada por breakset, e retorna um ponteiro para esse caractere.

2) Função genérica de tipo equivalente a (1). Seja `T` um tipo de objeto caractere não qualificado.

* Se `dest` for do tipo const T*, o tipo de retorno é const char*.
* Caso contrário, se `dest` for do tipo T*, o tipo de retorno é char*.
* Caso contrário, o comportamento é indefinido.

Se uma definição de macro de cada uma dessas funções genéricas for suprimida para acessar uma função real (por exemplo, se (strpbrk) ou um ponteiro de função for usado), a declaração de função real (1) torna-se visível.

O comportamento é indefinido se dest ou breakset não for um ponteiro para uma string de bytes terminada em nulo.

### Parâmetros

- **dest** — ponteiro para a string de bytes terminada em nulo a ser analisada
- **breakset** — ponteiro para a string de bytes terminada em nulo que contém os caracteres a serem procurados

### Valor de retorno

Ponteiro para o primeiro caractere em dest, que também está em breakset, ou ponteiro nulo se nenhum caractere desse tipo existir.

### Notas

O nome significa "string pointer break" (ponteiro de quebra de string), porque ele retorna um ponteiro para o primeiro dos caracteres separadores ("break").

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <string.h>
    
    int main(void)
    {
        const char* str = "hello world, friend of mine!";
        const char* sep = " ,!";
    
        unsigned int cnt = 0;
        do
        {
           str = strpbrk(str, sep); // encontra separador
           if(str) str += strspn(str, sep); // pula separador
           ++cnt; // incrementa contagem de palavras
        }
        while(str && *str);
    
        printf("There are %u words\n", cnt);
    }
```

Saída:
```
    There are 5 words
```

### Referências

* Padrão C23 (ISO/IEC 9899:2024):

* 7.24.5.4 A função strpbrk (p: TBD)

* Padrão C17 (ISO/IEC 9899:2018):

* 7.24.5.4 A função strpbrk (p: TBD)

* Padrão C11 (ISO/IEC 9899:2011):

* 7.24.5.4 A função strpbrk (p: 368)

* Padrão C99 (ISO/IEC 9899:1999):

* 7.21.5.4 A função strpbrk (p: 331)

* Padrão C89/C90 (ISO/IEC 9899:1990):

* 4.11.5.4 A função strpbrk

### Veja também

[ strcspn](<#/doc/string/byte/strcspn>) | retorna o comprimento do segmento inicial máximo que consiste apenas nos caracteres não encontrados em outra string de bytes (função)
[ strchr](<#/doc/string/byte/strchr>) | encontra a primeira ocorrência de um caractere (função)
[ strtokstrtok_s](<#/doc/string/byte/strtok>)(C11) | encontra o próximo token em uma string de bytes (função)
[Documentação C++](<#/>) para strpbrk