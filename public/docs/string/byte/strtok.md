# strtok, strtok_s

Definido no cabeçalho [`<string.h>`](<#/doc/string/byte>)

```c
char* strtok( char* str, const char* delim );  // ate C99
char* strtok( char* restrict str, const char* restrict delim );  // desde C99
char* strtok_s( char* restrict str, rsize_t* restrict strmax,
const char* restrict delim, char** restrict ptr );  // desde C11
```

  
1) Encontra o próximo token em uma string de bytes terminada em nulo apontada por str. Os caracteres separadores são identificados pela string de bytes terminada em nulo apontada por delim.

Esta função é projetada para ser chamada múltiplas vezes para obter tokens sucessivos da mesma string.

    

  * Se str não for um ponteiro nulo, a chamada é tratada como a primeira chamada para `strtok` para esta string em particular. A função procura pelo primeiro caractere que _não_ está contido em delim. 

    

  * Se nenhum caractere desse tipo for encontrado, não há tokens em str, e a função retorna um ponteiro nulo. 
  * Se tal caractere for encontrado, ele é o _início do token_. A função então procura a partir desse ponto pelo primeiro caractere que _está_ contido em delim. 

    

  * Se nenhum caractere desse tipo for encontrado, str tem apenas um token, e chamadas futuras para `strtok` retornarão um ponteiro nulo. 
  * Se tal caractere for encontrado, ele é _substituído_ pelo caractere nulo '\0' e o ponteiro para o caractere seguinte é armazenado em um local estático para invocações subsequentes. 

  * A função então retorna o ponteiro para o início do token. 

  * Se str for um ponteiro nulo, a chamada é tratada como uma chamada subsequente para `strtok`: a função continua de onde parou na invocação anterior. O comportamento é o mesmo como se o ponteiro armazenado anteriormente fosse passado como str. 

O comportamento é indefinido se str ou delim não for um ponteiro para uma string de bytes terminada em nulo.

2) O mesmo que (1), exceto que a cada passo, escreve o número de caracteres restantes a serem vistos em str em `*strmax` e escreve o estado interno do tokenizador em `*ptr`. Chamadas repetidas (com str nulo) devem passar strmax e ptr com os valores armazenados pela chamada anterior. Além disso, os seguintes erros são detectados em tempo de execução e chamam a função [manipulador de restrição](<#/doc/error/set_constraint_handler_s>) atualmente instalada, sem armazenar nada no objeto apontado por ptr:

    

  * strmax, delim, ou ptr é um ponteiro nulo. 
  * em uma chamada não inicial (com str nulo), `*ptr` é um ponteiro nulo. 
  * na primeira chamada, `*strmax` é zero ou maior que RSIZE_MAX.
  * a busca pelo fim de um token atinge o fim da string de origem (conforme medido pelo valor inicial de `*strmax`) sem encontrar o terminador nulo.

O comportamento é indefinido se str aponta para um array de caracteres que não possui o caractere nulo e strmax aponta para um valor que é maior que o tamanho desse array de caracteres. 

    Assim como todas as funções com verificação de limites, `strtok_s` é garantida para estar disponível apenas se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir [`<string.h>`](<#/doc/string/byte>).

### Parâmetros

str  |  \-  |  ponteiro para a string de bytes terminada em nulo a ser tokenizada   
delim  |  \-  |  ponteiro para a string de bytes terminada em nulo que identifica os delimitadores   
strmax  |  \-  |  ponteiro para um objeto que inicialmente contém o tamanho de str: strtok_s armazena o número de caracteres que restam a serem examinados   
ptr  |  \-  |  ponteiro para um objeto do tipo char*, que é usado por strtok_s para armazenar seu estado interno   
  
### Valor de retorno

Retorna um ponteiro para o início do próximo token ou um ponteiro nulo se não houver mais tokens. 

### Nota

Esta função é destrutiva: ela escreve os caracteres '\0' nos elementos da string str. Em particular, um literal de string não pode ser usado como o primeiro argumento de `strtok`. 

Cada chamada para `strtok` modifica uma variável estática: não é thread-safe. 

Ao contrário da maioria dos outros tokenizadores, os delimitadores em `strtok` podem ser diferentes para cada token subsequente, e podem até depender do conteúdo dos tokens anteriores. 

A função `strtok_s` difere da função POSIX [`strtok_r`](<https://pubs.opengroup.org/onlinepubs/9799919799/functions/strtok.html>) por proteger contra o armazenamento fora da string que está sendo tokenizada e por verificar restrições em tempo de execução. A assinatura de `strtok_s` do Microsoft CRT corresponde a esta definição POSIX `strtok_r`, não à `strtok_s` do C11. 

### Exemplo

Execute este código
```c
    #define __STDC_WANT_LIB_EXT1__ 1
    #include <stdio.h>
    #include <string.h>
    
    int main(void)
    {
        char input[] = "A bird came down the walk";
        printf("Parsing the input string '%s'\n", input);
        char* token = strtok(input, " ");
        while (token)
        {
            puts(token);
            token = strtok(NULL, " ");
        }
    
        printf("Contents of the input string now: '");
        for (size_t n = 0; n < sizeof input; ++n)
            input[n] ? putchar(input[n]) : fputs("\\0", stdout);
        puts("'");
    
    #ifdef __STDC_LIB_EXT1__
        char str[] = "A bird came down the walk";
        rsize_t strmax = sizeof str;
        const char* delim = " ";
        char* next_token;
        printf("Parsing the input string '%s'\n", str);
        token = strtok_s(str, &strmax, delim, &next_token);
        while (token)
        {
            puts(token);
            token = strtok_s(NULL, &strmax, delim, &next_token);
        }
    
        printf("Contents of the input string now: '");
        for (size_t n = 0; n < sizeof str; ++n)
            str[n] ? putchar(str[n]) : fputs("\\0", stdout);
        puts("'");
    #endif
    }
```

Saída possível: 
```
    Parsing the input string 'A bird came down the walk'
    A
    bird
    came
    down
    the
    walk
    Contents of the input string now: 'A\0bird\0came\0down\0the\0walk\0'
    Parsing the input string 'A bird came down the walk'
    A
    bird
    came
    down
    the
    walk
    Contents of the input string now: 'A\0bird\0came\0down\0the\0walk\0'
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.24.5.8 A função strtok (p: TBD) 

    

  * K.3.7.3.1 A função strtok_s (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.24.5.8 A função strtok (p: TBD) 

    

  * K.3.7.3.1 A função strtok_s (p: TBD) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.24.5.8 A função strtok (p: 369-370) 

    

  * K.3.7.3.1 A função strtok_s (p: 620-621) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.21.5.8 A função strtok (p: 332-333) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.11.5.8 A função strtok 

### Veja também

[ strpbrk](<#/doc/string/byte/strpbrk>) |  encontra a primeira ocorrência de qualquer caractere de uma string, em outra string   
(função)  
[ strcspn](<#/doc/string/byte/strcspn>) |  retorna o comprimento do segmento inicial máximo que consiste   
apenas nos caracteres não encontrados em outra string de bytes   
(função)  
[ strspn](<#/doc/string/byte/strspn>) |  retorna o comprimento do segmento inicial máximo que consiste   
apenas nos caracteres encontrados em outra string de bytes   
(função)  
[ wcstokwcstok_s](<#/doc/string/wide/wcstok>)(C95)(C11) |  encontra o próximo token em uma wide string   
(função)  
[Documentação C++](<#/>) para strtok