# strerror, strerror_s, strerrorlen_s

Definido no cabeçalho [`<string.h>`](<#/doc/string/byte>)

```c
char* strerror( int errnum );
errno_t strerror_s( char *buf, rsize_t bufsz, errno_t errnum );  // desde C11
size_t strerrorlen_s( errno_t errnum );  // desde C11
```

1) Retorna um ponteiro para a descrição textual do código de erro do sistema `errnum`, idêntica à descrição que seria impressa por [perror()](<#/doc/io/perror>).

`errnum` é geralmente adquirido da variável `errno`, no entanto, a função aceita qualquer valor do tipo int. O conteúdo da string é específico da localidade.

A string retornada não deve ser modificada pelo programa, mas pode ser sobrescrita por uma chamada subsequente à função `strerror`. `strerror` não é exigida ser thread-safe. As implementações podem retornar diferentes ponteiros para literais de string estáticas somente leitura ou podem retornar o mesmo ponteiro repetidamente, apontando para um buffer estático no qual `strerror` coloca a string.

2) O mesmo que (1), exceto que a mensagem é copiada para o armazenamento fornecido pelo usuário `buf`. Não mais que `bufsz-1` bytes são escritos, o buffer é sempre terminado em nulo. Se a mensagem teve que ser truncada para caber no buffer e `bufsz` for maior que 3, então apenas `bufsz-4` bytes são escritos, e os caracteres "..." são anexados antes do terminador nulo. Além disso, os seguintes erros são detectados em tempo de execução e chamam a função [constraint handler](<#/doc/error/set_constraint_handler_s>) atualmente instalada:

  * `buf` é um ponteiro nulo
  * `bufsz` é zero ou maior que RSIZE_MAX

O comportamento é indefinido se a escrita em `buf` ocorrer além do final do array, o que pode acontecer quando o tamanho do buffer apontado por `buf` for menor que o número de caracteres na mensagem de erro, que por sua vez é menor que `bufsz`.

3) Calcula o comprimento da mensagem de erro específica da localidade não truncada que `strerror_s` escreveria se fosse chamada com `errnum`. O comprimento não inclui o terminador nulo.

Assim como todas as funções com verificação de limites, `strerror_s` e `strerrorlen_s` são garantidas de estarem disponíveis apenas se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir [`<string.h>`](<#/doc/string/byte>).

### Parâmetros

- **errnum** — valor integral referindo-se a um código de erro
- **buf** — ponteiro para um buffer fornecido pelo usuário
- **bufsz** — tamanho do buffer fornecido pelo usuário

### Valor de retorno

1) Ponteiro para uma string de bytes terminada em nulo correspondente ao código de erro [errno](<#/doc/error/errno>) `errnum`.

2) Zero se a mensagem inteira foi armazenada com sucesso em `buf`, diferente de zero caso contrário.

3) Comprimento (não incluindo o terminador nulo) da mensagem que `strerror_s` retornaria

### Notas

[POSIX](<http://pubs.opengroup.org/onlinepubs/9699919799/functions/strerror.html>) permite que chamadas subsequentes a `strerror` invalidem o valor do ponteiro retornado por uma chamada anterior. Também especifica que é a faceta de localidade [`LC_MESSAGES`](<#/doc/locale/LC_categories>) que controla o conteúdo dessas mensagens.

`strerror_s` é a única função com verificação de limites que permite truncamento, porque fornecer o máximo de informações possível sobre uma falha foi considerado mais desejável. POSIX também define [`strerror_r`](<http://pubs.opengroup.org/onlinepubs/9699919799/functions/strerror.html>) para propósitos semelhantes.

### Exemplo

Execute este código
```c
    #define __STDC_WANT_LIB_EXT1__ 1
    #include <stdio.h>
    #include <errno.h>
    #include <string.h>
    #include <locale.h>
    
    int main(void)
    {
        FILE *fp = fopen(tmpnam((char[L_tmpnam]){0}), "r");
        if(fp==NULL) {
            printf("File opening error: %s\n", strerror(errno));
            setlocale(LC_MESSAGES, "de_DE.utf8");
            printf("Now in German: %s\n", strerror(errno));
    #ifdef __STDC_LIB_EXT1__
            setlocale(LC_ALL, "ja_JP.utf8"); // printf needs CTYPE for multibyte output
            size_t errmsglen = strerrorlen_s(errno) + 1;
            char errmsg[errmsglen]; 
            strerror_s(errmsg, errmsglen, errno);
            printf("Now in Japanese: %s\n", errmsg);
    #endif
        }
    }
```

Saída possível:
```
    File opening error: No such file or directory
    Now in German: Datei oder Verzeichnis nicht gefunden
    Now in Japanese: そのようなファイル、又はディレクトリはありません
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    * 7.24.6.2 A função strerror (p: 371)

    * K.3.7.4.2 A função strerror_s (p: 622)

    * K.3.7.4.3 A função strerrorlen_s (p: 623)

  * Padrão C99 (ISO/IEC 9899:1999):

    * 7.21.6.2 A função strerror (p: 334)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    * 4.11.6.2 A função strerror

### Veja também

[ perror](<#/doc/io/perror>) | exibe uma string de caracteres correspondente ao erro atual para [stderr](<#/doc/io/std_streams>)
(função)
[ errno](<#/doc/error/errno>) | macro que se expande para uma variável de número de erro thread-local compatível com POSIX
(variável macro)
[Documentação C++](<#/>) para strerror