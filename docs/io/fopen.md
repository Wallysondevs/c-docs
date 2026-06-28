# fopen, fopen_s

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
FILE *fopen( const char *filename, const char *mode );  // até C99
FILE *fopen( const char *restrict filename, const char *restrict mode );  // desde C99
errno_t fopen_s( FILE *restrict *restrict streamptr,
const char *restrict filename,
const char *restrict mode );  // desde C11
```

1) Abre um arquivo indicado por `filename` e retorna um ponteiro para o fluxo de arquivo associado a esse arquivo. `mode` é usado para determinar o modo de acesso ao arquivo.

2) O mesmo que (1), exceto que o ponteiro para o fluxo de arquivo é escrito em `streamptr` e os seguintes erros são detectados em tempo de execução e chamam a função [manipulador de restrição](<#/doc/error/set_constraint_handler_s>) atualmente instalada:

  * `streamptr` é um ponteiro nulo
  * `filename` é um ponteiro nulo
  * `mode` é um ponteiro nulo

Assim como todas as funções com verificação de limites, `fopen_s` tem sua disponibilidade garantida apenas se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir `[`<stdio.h>`](<#/doc/io>)`.

### Parâmetros

- **filename** — nome do arquivo para associar ao fluxo de arquivo
- **mode** — string de caracteres terminada em nulo que determina o [modo de acesso ao arquivo](<#/doc/io/fopen>)
- **streamptr** — ponteiro para um ponteiro onde a função armazena o resultado (um parâmetro de saída)

### Flags de acesso ao arquivo

String do modo de acesso ao arquivo | Significado | Explicação | Ação se o arquivo já existe | Ação se o arquivo não existe
"r" | leitura | Abre um arquivo para leitura | lê do início | falha ao abrir
"w" | escrita | Cria um arquivo para escrita | destrói o conteúdo | cria novo
"a" | anexar | Anexa a um arquivo | escreve no final | cria novo
"r+" | leitura estendida | Abre um arquivo para leitura/escrita | lê do início | erro
"w+" | escrita estendida | Cria um arquivo para leitura/escrita | destrói o conteúdo | cria novo
"a+" | anexar estendido | Abre um arquivo para leitura/escrita | escreve no final | cria novo
A flag de modo de acesso ao arquivo "b" pode ser especificada opcionalmente para abrir um arquivo em modo binário. Esta flag não tem efeito em sistemas POSIX, mas no Windows ela desabilita o tratamento especial de '\n' e '\x1A'.
Nos modos de acesso ao arquivo de anexação, os dados são escritos no final do arquivo, independentemente da posição atual do indicador de posição do arquivo.
O comportamento é indefinido se o modo não for uma das strings listadas acima. Algumas implementações definem modos adicionais suportados (por exemplo, [Windows](<https://docs.microsoft.com/en-us/cpp/c-runtime-library/reference/fopen-wfopen>)).
No modo de atualização ('+'), tanto a entrada quanto a saída podem ser realizadas, mas a saída não pode ser seguida por entrada sem uma chamada intermediária para [fflush](<#/doc/io/fflush>), [fseek](<#/doc/io/fseek>), [fsetpos](<#/doc/io/fsetpos>) ou [rewind](<#/doc/io/rewind>), e a entrada não pode ser seguida por saída sem uma chamada intermediária para [fseek](<#/doc/io/fseek>), [fsetpos](<#/doc/io/fsetpos>) ou [rewind](<#/doc/io/rewind>), a menos que a operação de entrada tenha encontrado o fim do arquivo. No modo de atualização, as implementações têm permissão para usar o modo binário mesmo quando o modo de texto é especificado.
A flag de modo de acesso ao arquivo "x" pode ser anexada opcionalmente aos especificadores "w" ou "w+". Esta flag força a função a falhar se o arquivo existir, em vez de sobrescrevê-lo. (C11)
Ao usar fopen_s ou freopen_s, as permissões de acesso a arquivos para qualquer arquivo criado com "w" ou "a" impedem que outros usuários o acessem. A flag de modo de acesso ao arquivo "u" pode ser opcionalmente prefixada a qualquer especificador que comece com "w" ou "a", para habilitar as permissões padrão do **fopen**. (C11)

### Valor de retorno

1) Em caso de sucesso, retorna um ponteiro para o novo fluxo de arquivo. O fluxo é totalmente armazenado em buffer, a menos que `filename` se refira a um dispositivo interativo. Em caso de erro, retorna um ponteiro nulo. [POSIX exige](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/fopen.html>) que [errno](<#/doc/error/errno>) seja definido neste caso.

2) Em caso de sucesso, retorna zero e um ponteiro para o novo fluxo de arquivo é escrito em *streamptr. Em caso de erro, retorna um código de erro diferente de zero e escreve o ponteiro nulo em *streamptr (a menos que `streamptr` seja um ponteiro nulo em si).

### Observações

O formato de `filename` é definido pela implementação e não se refere necessariamente a um arquivo (por exemplo, pode ser o console ou outro dispositivo acessível através da API do sistema de arquivos). Em plataformas que os suportam, `filename` pode incluir um caminho absoluto ou relativo do sistema de arquivos.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(void)
    {
        const char* fname = "/tmp/unique_name.txt"; // or tmpnam(NULL);
        int is_ok = EXIT_FAILURE;
    
        FILE* fp = fopen(fname, "w+");
        if (!fp)
        {
            perror("File opening failed");
            return is_ok;
        }
        fputs("Hello, world!\n", fp);
        rewind(fp);
    
        int c; // note: int, not char, required to handle EOF
        while ((c = fgetc(fp)) != EOF) // standard C I/O file reading loop
            putchar(c);
    
        if (ferror(fp))
            puts("I/O error when reading");
        else if (feof(fp))
        {
            puts("End of file is reached successfully");
            is_ok = EXIT_SUCCESS;
        }
    
        fclose(fp);
        remove(fname);
        return is_ok;
    }
```

Saída possível:
```
    Hello, world!
    End of file is reached successfully
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    * 7.21.5.3 A função fopen (p: 223-224)

    * K.3.5.2.1 A função fopen_s (p: 428-429)

  * Padrão C11 (ISO/IEC 9899:2011):

    * 7.21.5.3 A função fopen (p: 305-306)

    * K.3.5.2.1 A função fopen_s (p: 588-590)

  * Padrão C99 (ISO/IEC 9899:1999):

    * 7.19.5.3 A função fopen (p: 271-272)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    * 4.9.5.3 A função fopen

### Veja também

[ fclose](<#/doc/io/fclose>) | fecha um arquivo
(função)
[ fflush](<#/doc/io/fflush>) | sincroniza um fluxo de saída com o arquivo real
(função)
[ freopenfreopen_s](<#/doc/io/freopen>)(C11) | abre um fluxo existente com um nome diferente
(função)
[documentação C++](<#/>) para fopen