# wcstok, wcstok_s

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
wchar_t* wcstok( wchar_t* str, const wchar_t* delim, wchar_t** ptr );  // desde C95
(até C99)  // até C99
wchar_t* wcstok( wchar_t* restrict str, const wchar_t* restrict delim,
wchar_t** restrict ptr );  // desde C99
wchar_t* wcstok_s( wchar_t* restrict str, rsize_t* restrict strmax,
const wchar_t* restrict delim, wchar_t** restrict ptr);  // desde C11
```

1) Encontra o próximo token em uma string larga terminada em nulo apontada por str. Os caracteres separadores são identificados pela string larga terminada em nulo apontada por delim.

Esta função é projetada para ser chamada múltiplas vezes para obter tokens sucessivos da mesma string.

*   Se str != [NULL](<#/doc/types/NULL>), a chamada é tratada como a primeira chamada para `wcstok` para esta string larga em particular. A função procura pelo primeiro caractere largo que _não_ está contido em delim.
*   Se nenhum caractere largo desse tipo for encontrado, não há tokens em str, e a função retorna um ponteiro nulo.
*   Se tal caractere largo for encontrado, ele é o _início do token_. A função então procura a partir desse ponto pelo primeiro caractere largo que _está_ contido em delim.
*   Se nenhum caractere largo desse tipo for encontrado, str tem apenas um token, e chamadas futuras para `wcstok` retornarão um ponteiro nulo.
*   Se tal caractere largo for encontrado, ele é _substituído_ pelo caractere largo nulo L'\0' e o estado do analisador (tipicamente um ponteiro para o caractere largo seguinte) é armazenado no local fornecido pelo usuário *ptr.
*   A função então retorna o ponteiro para o início do token.
*   Se str == [NULL](<#/doc/types/NULL>), a chamada é tratada como uma chamada subsequente para `wcstok`: a função continua de onde parou na invocação anterior com o mesmo *ptr. O comportamento é o mesmo como se o ponteiro para o caractere largo que segue o último token detectado fosse passado como str.

2) O mesmo que (1), exceto que a cada passo, escreve o número de caracteres restantes a serem vistos em str em *strmax. Chamadas repetidas (com str nulo) devem passar strmax e ptr com os valores armazenados pela chamada anterior. Além disso, os seguintes erros são detectados em tempo de execução e chamam a função [manipulador de restrição](<#/doc/error/set_constraint_handler_s>) atualmente instalada, sem armazenar nada no objeto apontado por ptr:

*   strmax, delim, ou ptr é um ponteiro nulo.
*   em uma chamada não inicial (com str nulo), *ptr é um ponteiro nulo.
*   na primeira chamada, *strmax é zero ou maior que RSIZE_MAX / sizeof(wchar_t).
*   a busca pelo fim de um token atinge o fim da string de origem (medido pelo valor inicial de *strmax) sem encontrar o terminador nulo.

Como todas as funções com verificação de limites, `wcstok_s` é garantida para estar disponível apenas se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir [`<wchar.h>`](<#/doc/string/wide>).

### Parâmetros

- **str** — ponteiro para a string larga terminada em nulo a ser tokenizada
- **delim** — ponteiro para a string larga terminada em nulo que identifica os delimitadores
- **ptr** — ponteiro para um objeto do tipo wchar_t*, que é usado por `wcstok` e `wcstok_s` para armazenar o estado interno do analisador
- **strmax** — ponteiro para um objeto que inicialmente contém o tamanho de str: wcstok_s armazena o número de caracteres que restam a serem examinados

### Valor de retorno

Retorna um ponteiro para o início do próximo token ou um ponteiro nulo se não houver mais tokens.

### Nota

Esta função é destrutiva: ela escreve os caracteres L'\0' nos elementos da string str. Em particular, um literal de string larga não pode ser usado como o primeiro argumento de `wcstok`.

Ao contrário de [strtok](<#/doc/string/byte/strtok>), `wcstok` não atualiza o armazenamento estático: ela armazena o estado do analisador no local fornecido pelo usuário.

Ao contrário da maioria dos outros tokenizadores, os delimitadores em `wcstok` podem ser diferentes para cada token subsequente e podem até depender do conteúdo dos tokens anteriores.

A implementação de wcstok_s no [Windows CRT](<https://learn.microsoft.com/en-us/cpp/c-runtime-library/reference/strtok-s-strtok-s-l-wcstok-s-wcstok-s-l-mbstok-s-mbstok-s-l>) é incompatível com o padrão C, sendo meramente um alias para wcstok.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <wchar.h>
     
    int main(void)
    {
        wchar_t input[] = L"A bird came down the walk";
        printf("Parsing the input string '%ls'\n", input);
        wchar_t* buffer;
        wchar_t* token = wcstok(input, L" ", &buffer);
        while (token)
        {
            printf("%ls\n", token);
            token = wcstok(NULL, L" ", &buffer);
        }
     
        printf("Contents of the input string now: '");
        for (size_t n = 0; n < sizeof input / sizeof *input; ++n)
            input[n] ? printf("%lc", input[n]) : printf("\\0");
        puts("'");
    }
```

Saída:
```
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

*   Padrão C11 (ISO/IEC 9899:2011):
    *   7.29.4.5.7 A função wcstok (p: 437-438)
    *   K.3.9.2.3.1 A função wcstok_s (p: 645-646)
*   Padrão C99 (ISO/IEC 9899:1999):
    *   7.24.4.5.7 A função wcstok (p: 383-384)

### Ver também

[ strtokstrtok_s](<#/doc/string/byte/strtok>)(C11) | encontra o próximo token em uma string de bytes
(função)
[Documentação C++](<#/>) para wcstok