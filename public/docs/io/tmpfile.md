# tmpfile, tmpfile_s

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
FILE* tmpfile( void );
errno_t tmpfile_s( FILE* restrict* restrict streamptr );  // desde C11
```

  
1) Cria e abre um arquivo temporário. O arquivo é aberto como arquivo binário para atualização (como se fosse por [fopen](<#/doc/io/fopen>) com o modo "wb+"). O nome do arquivo é garantido como único dentro do sistema de arquivos. Pelo menos [TMP_MAX](<#/doc/io>) arquivos podem ser abertos durante a vida útil de um programa (este limite pode ser compartilhado com [tmpnam](<#/doc/io/tmpnam>) e pode ser ainda mais limitado por [FOPEN_MAX](<#/doc/io>)).

2) O mesmo que (1), exceto que pelo menos TMP_MAX_S arquivos podem ser abertos (o limite pode ser compartilhado com tmpnam_s), e se streamptr for um ponteiro nulo, a função [constraint handler](<#/doc/error/set_constraint_handler_s>) atualmente instalada é chamada. 

    Assim como todas as funções com verificação de limites (bounds-checked functions), `tmpfile_s` é garantida como disponível apenas se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir [`<stdio.h>`](<#/doc/io>).

O arquivo temporário criado por esta função é fechado e excluído quando o programa termina normalmente. Se ele é excluído em caso de término anormal é um comportamento definido pela implementação (implementation-defined). 

### Parâmetros

1) (nenhum)

2) ponteiro para um ponteiro que será atualizado por esta chamada de função

### Valor de retorno

1) Ponteiro para o fluxo de arquivo (file stream) associado ao arquivo ou ponteiro nulo se um erro ocorreu.

2) Zero se o arquivo foi criado e aberto com sucesso, diferente de zero se o arquivo não foi criado ou aberto ou se streamptr era um ponteiro nulo. Além disso, o ponteiro para o fluxo de arquivo associado é armazenado em *streamptr em caso de sucesso, e um valor de ponteiro nulo é armazenado em *streamptr em caso de erro.

### Notas

Em algumas implementações (por exemplo, Linux mais antigos), esta função realmente cria, abre e imediatamente exclui o arquivo do sistema de arquivos: enquanto um descritor de arquivo (file descriptor) aberto para um arquivo excluído for mantido por um programa, o arquivo existe, mas como foi excluído, seu nome não aparece em nenhum diretório, de modo que nenhum outro processo pode abri-lo. Uma vez que o descritor de arquivo é fechado, ou uma vez que o programa termina (normalmente ou anormalmente), o espaço ocupado pelo arquivo é recuperado pelo sistema de arquivos. Linux mais recentes (desde 3.11 ou posterior, dependendo do sistema de arquivos) criam tais arquivos temporários invisíveis em uma única etapa, através de um flag especial na chamada de sistema [`open()`](<https://man7.org/linux/man-pages/man2/open.2.html>). 

Em algumas implementações (por exemplo, Windows), privilégios elevados (elevated privileges) são necessários, pois a função pode criar o arquivo temporário em um diretório do sistema. 

### Exemplo

Execute este código
```
    #define _POSIX_C_SOURCE 200112L
    #include <stdio.h>
    #include <unistd.h>
     
    int main(void)
    {
        printf("TMP_MAX = %d, FOPEN_MAX = %d\n", TMP_MAX, FOPEN_MAX);
        FILE* tmpf = tmpfile();
        fputs("Hello, world", tmpf);
        rewind(tmpf);
        char buf[6];
        fgets(buf, sizeof buf, tmpf);
        printf("got back from the file: '%s'\n", buf);
     
        // Linux-specific method to display the tmpfile name
        char fname[FILENAME_MAX], link[FILENAME_MAX] = {0};
        sprintf(fname, "/proc/self/fd/%d", fileno(tmpf));
        if (readlink(fname, link, sizeof link - 1) > 0)
            printf("File name: %s\n", link);
    }
```

Saída possível: 
```
    TMP_MAX = 238328, FOPEN_MAX = 16
    got back from the file: 'Hello'
    File name: /tmp/tmpfjptPe5 (deleted)
```

### Referências

  * C23 standard (ISO/IEC 9899:2024): 

    

  * 7.21.4.3 The tmpfile function (p: TBD) 

    

  * K.3.5.1.1 The tmpfile_s function (p: TBD) 

  * C17 standard (ISO/IEC 9899:2018): 

    

  * 7.21.4.3 The tmpfile function (p: 222) 

    

  * K.3.5.1.1 The tmpfile_s function (p: 427) 

  * C11 standard (ISO/IEC 9899:2011): 

    

  * 7.21.4.3 The tmpfile function (p: 303) 

    

  * K.3.5.1.1 The tmpfile_s function (p: 586-587) 

  * C99 standard (ISO/IEC 9899:1999): 

    

  * 7.19.4.3 The tmpfile function (p: 269) 

  * C89/C90 standard (ISO/IEC 9899:1990): 

    

  * 4.9.4.3 The tmpfile function 

### Veja também

[ tmpnamtmpnam_s](<#/doc/io/tmpnam>)(C11) |  retorna um nome de arquivo único   
(função)  
[Documentação C++](<#/>) para tmpfile