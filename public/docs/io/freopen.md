# freopen, freopen_s

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
FILE *freopen( const char *filename, const char *mode,
FILE *stream );  // até C99
FILE *freopen( const char *restrict filename, const char *restrict mode,
FILE *restrict stream );  // desde C99
errno_t freopen_s( FILE *restrict *restrict newstreamptr,
const char *restrict filename, const char *restrict mode,
FILE *restrict stream );  // desde C11
```

1) Primeiro, tenta fechar o arquivo associado a `stream`, ignorando quaisquer erros. Em seguida, se `filename` não for nulo, tenta abrir o arquivo especificado por `filename` usando `mode` como se fosse por [fopen](<#/doc/io/fopen>), e associa esse arquivo ao fluxo de arquivo apontado por `stream`. Se `filename` for um ponteiro nulo, a função tenta reabrir o arquivo que já está associado a `stream` (é definido pela implementação quais mudanças de modo são permitidas neste caso).

2) O mesmo que (1), exceto que `mode` é tratado como em fopen_s e que o ponteiro para o fluxo de arquivo é escrito em `newstreamptr` e os seguintes erros são detectados em tempo de execução e chamam a função [manipulador de restrição](<#/doc/error/set_constraint_handler_s>) atualmente instalada:

  * `newstreamptr` é um ponteiro nulo
  * `stream` é um ponteiro nulo
  * `mode` é um ponteiro nulo

Assim como todas as funções com verificação de limites, `freopen_s` é garantida para estar disponível apenas se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir [`<stdio.h>`](<#/doc/io>).

### Parâmetros

- **filename** — nome do arquivo para associar ao fluxo de arquivo
- **mode** — string de caracteres terminada em nulo que determina o novo [modo de acesso ao arquivo](<#/doc/io/freopen>)
- **stream** — o fluxo de arquivo a ser modificado
- **newstreamptr** — ponteiro para um ponteiro onde a função armazena o resultado (um parâmetro de saída)

### Sinalizadores de acesso a arquivo

String do modo de acesso ao arquivo | Significado | Explicação | Ação se o arquivo já existe | Ação se o arquivo não existe
"r" | leitura | Abre um arquivo para leitura | lê do início | falha ao abrir
"w" | escrita | Cria um arquivo para escrita | destrói o conteúdo | cria novo
"a" | anexar | Anexa a um arquivo | escreve no final | cria novo
"r+" | leitura estendida | Abre um arquivo para leitura/escrita | lê do início | erro
"w+" | escrita estendida | Cria um arquivo para leitura/escrita | destrói o conteúdo | cria novo
"a+" | anexar estendido | Abre um arquivo para leitura/escrita | escreve no final | cria novo
O sinalizador de modo de acesso a arquivo "b" pode ser opcionalmente especificado para abrir um arquivo em modo binário. Este sinalizador não tem efeito em sistemas POSIX, mas no Windows ele desabilita o tratamento especial de '\n' e '\x1A'.
Nos modos de acesso a arquivo de anexação, os dados são escritos no final do arquivo, independentemente da posição atual do indicador de posição do arquivo.
O comportamento é indefinido se o modo não for uma das strings listadas acima. Algumas implementações definem modos adicionais suportados (por exemplo, [Windows](<https://docs.microsoft.com/en-us/cpp/c-runtime-library/reference/fopen-wfopen>)).
No modo de atualização ('+'), tanto a entrada quanto a saída podem ser realizadas, mas a saída não pode ser seguida por entrada sem uma chamada intermediária para [fflush](<#/doc/io/fflush>), [fseek](<#/doc/io/fseek>), [fsetpos](<#/doc/io/fsetpos>) ou [rewind](<#/doc/io/rewind>), e a entrada não pode ser seguida por saída sem uma chamada intermediária para [fseek](<#/doc/io/fseek>), [fsetpos](<#/doc/io/fsetpos>) ou [rewind](<#/doc/io/rewind>), a menos que a operação de entrada tenha encontrado o fim do arquivo. No modo de atualização, as implementações são permitidas a usar o modo binário mesmo quando o modo de texto é especificado.
O sinalizador de modo de acesso a arquivo "x" pode ser opcionalmente anexado aos especificadores "w" ou "w+". Este sinalizador força a função a falhar se o arquivo existir, em vez de sobrescrevê-lo. (C11)
Ao usar fopen_s ou freopen_s, as permissões de acesso a arquivo para qualquer arquivo criado com "w" ou "a" impedem que outros usuários o acessem. O sinalizador de modo de acesso a arquivo "u" pode ser opcionalmente prefixado a qualquer especificador que comece com "w" ou "a", para habilitar as permissões padrão de [fopen](<#/doc/io/fopen>). (C11)

### Valor de retorno

1) Uma cópia do valor de `stream` em caso de sucesso, ponteiro nulo em caso de falha.

2) zero em caso de sucesso (e uma cópia do valor de `stream` é escrita em *newstreamptr), diferente de zero em caso de erro (e ponteiro nulo é escrito em *newstreamptr, a menos que `newstreamptr` seja ele próprio um ponteiro nulo).

### Notas

`freopen` é a única maneira de mudar a orientação estreita/ampla de um fluxo depois que ela foi estabelecida por uma operação de E/S ou por fwide.

A versão CRT da Microsoft de `freopen` não suporta nenhuma mudança de modo quando `filename` é um ponteiro nulo e trata isso como um erro (veja [documentação](<https://docs.microsoft.com/en-us/cpp/c-runtime-library/reference/freopen-wfreopen>)). Uma possível solução alternativa é a função não padrão [`_setmode()`](<https://docs.microsoft.com/en-us/cpp/c-runtime-library/reference/setmode>).

### Exemplo

O código a seguir redireciona `stdout` para um arquivo.

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
     
    int main(void)
    {
        puts("stdout is printed to console");
        if (freopen("redir.txt", "w", stdout) == NULL)
        {
           perror("freopen() failed");
           return EXIT_FAILURE;
        }
        puts("stdout is redirected to a file"); // this is written to redir.txt
        fclose(stdout);
        return EXIT_SUCCESS;
    }
```

Saída:
```
    stdout is printed to console
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    * 7.21.5.4 A função freopen (p: 224-225)

    * K.3.5.2.2 A função freopen_s (p: 429-430)

  * Padrão C11 (ISO/IEC 9899:2011):

    * 7.21.5.4 A função freopen (p: 307)

    * K.3.5.2.2 A função freopen_s (p: 590)

  * Padrão C99 (ISO/IEC 9899:1999):

    * 7.19.5.4 A função freopen (p: 272-273)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    * 4.9.5.4 A função freopen

### Veja também

[ fopenfopen_s](<#/doc/io/fopen>)(C11) | abre um arquivo
(função)
[ fclose](<#/doc/io/fclose>) | fecha um arquivo
(função)
[Documentação C++](<#/>) para freopen