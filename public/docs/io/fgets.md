# fgets

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
char* fgets( char* str, int count, FILE* stream );  // até C99
char* fgets( char* restrict str, int count, FILE* restrict stream );  // desde C99
```

Lê no máximo count - 1 caracteres do fluxo de arquivo fornecido e os armazena no array de caracteres apontado por str. A análise para se um caractere de nova linha é encontrado (nesse caso, str conterá esse caractere de nova linha) ou se o fim do arquivo ocorrer. Se bytes forem lidos e nenhum erro ocorrer, escreve um caractere nulo na posição imediatamente após o último caractere escrito em str.

### Parâmetros

- **str** — ponteiro para um elemento de um array de char
- **count** — número máximo de caracteres a serem escritos (tipicamente o comprimento de str)
- **stream** — fluxo de arquivo para ler os dados

### Valor de retorno

str em caso de sucesso, ponteiro nulo em caso de falha.

Se a condição de fim de arquivo for encontrada, define o indicador _eof_ no fluxo (veja [feof()](<#/doc/io/feof>)). Isso é uma falha apenas se não causar a leitura de bytes, caso em que um ponteiro nulo é retornado e o conteúdo do array apontado por str não é alterado (ou seja, o primeiro byte não é sobrescrito com um caractere nulo).

Se a falha foi causada por algum outro erro, define o indicador _error_ (veja [ferror()](<#/doc/io/ferror>)) no fluxo. O conteúdo do array apontado por str é indeterminado (pode nem mesmo ser terminado em nulo).

### Notas

[POSIX adicionalmente exige](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/fgets.html>) que fgets defina [errno](<#/doc/error/errno>) se ocorrer um erro de leitura.

Embora a especificação padrão seja [pouco clara](<https://stackoverflow.com/questions/23388620>) nos casos em que count <= 1, implementações comuns fazem

* se count < 1, não faz nada, reporta erro,
* se count == 1,

  * algumas implementações não fazem nada, reportam erro,
  * outras não leem nada, armazenam zero em str[0], reportam sucesso.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(void)
    {
        FILE* tmpf = tmpfile();
        fputs("Alan Turing\n", tmpf);
        fputs("John von Neumann\n", tmpf);
        fputs("Alonzo Church\n", tmpf);
    
        rewind(tmpf);
    
        char buf[8];
        while (fgets(buf, sizeof buf, tmpf) != NULL)
              printf("\"%s\"\n", buf);
    
        if (feof(tmpf))
           puts("End of file reached");
    }
```

Saída:
```
    "Alan Tu"
    "ring
    "
    "John vo"
    "n Neuma"
    "nn
    "
    "Alonzo "
    "Church
    "
    End of file reached
```

### Referências

* Padrão C23 (ISO/IEC 9899:2024):

  * 7.21.7.2 A função fgets (p: TBD)
* Padrão C17 (ISO/IEC 9899:2018):

  * 7.21.7.2 A função fgets (p: 241)
* Padrão C11 (ISO/IEC 9899:2011):

  * 7.21.7.2 A função fgets (p: 331)
* Padrão C99 (ISO/IEC 9899:1999):

  * 7.19.7.2 A função fgets (p: 296)
* Padrão C89/C90 (ISO/IEC 9899:1990):

  * 4.9.7.2 A função fgets

### Veja também

[ scanffscanfsscanfscanf_sfscanf_ssscanf_s](<#/doc/io/fscanf>)(C11)(C11)(C11) | lê entrada formatada de [stdin](<#/doc/io/std_streams>), um fluxo de arquivo ou um buffer
(função)
[ getsgets_s](<#/doc/io/gets>)(removido em C11)(C11) | lê uma string de caracteres de [stdin](<#/doc/io/std_streams>)
(função)
[ fputs](<#/doc/io/fputs>) | escreve uma string de caracteres em um fluxo de arquivo
(função)
[ getlinegetwlinegetdelimgetwdelim](<#/doc/experimental/dynamic/getline>)(TR de memória dinâmica) | lê de um fluxo para um buffer redimensionado automaticamente até o delimitador/fim da linha
(função)
[Documentação C++](<#/>) para fgets