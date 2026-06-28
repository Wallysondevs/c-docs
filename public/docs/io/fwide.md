# fwide

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
int fwide( FILE* stream, int mode );  // desde C95
```

Se mode > 0, tenta tornar o fluxo orientado a caracteres largos (wide-oriented). Se mode < 0, tenta tornar o fluxo orientado a bytes (byte-oriented). Se mode == 0, apenas consulta a orientação atual do fluxo.

Se a orientação do fluxo já foi decidida (pela execução de saída ou por uma chamada anterior a `fwide`), esta função não faz nada.

### Parâmetros

- **stream** — ponteiro para o fluxo de E/S C a ser modificado ou consultado
- **mode** — valor inteiro maior que zero para definir o fluxo como largo (wide), menor que zero para definir o fluxo como estreito (narrow), ou zero para apenas consultar

### Valor de retorno

Um inteiro maior que zero se o fluxo estiver orientado a caracteres largos (wide-oriented) após esta chamada, menor que zero se o fluxo estiver orientado a bytes (byte-oriented) após esta chamada, e zero se o fluxo não tiver orientação.

### Exemplo

O código a seguir define e redefine a orientação do fluxo.

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
    #include <wchar.h>
     
    void show_orientation(int n)
    {
        n < 0 ? puts("\tnarrow orientation"):
        n > 0 ? puts("\twide orientation"):
                puts("\tno orientation");
    }
     
    void try_read(FILE* fp)
    {
        int c = fgetc(fp);
        c == EOF
            ? printf("\tnarrow character read failed\n")
            : printf("\tnarrow character read '%c'\n", c);
     
        wint_t wc = fgetwc(fp);
        wc == WEOF
            ? printf("\twide character read failed\n")
            : printf("\twide character read '%lc'\n", wc);
    }
     
    int main(void)
    {
        enum fwide_orientation { narrow = -1, query, wide };
     
        FILE* fp = fopen("main.cpp", "r");
        if (!fp)
        {
            perror("fopen() failed");
            return EXIT_FAILURE;
        }
     
        puts("1) A newly opened stream has no orientation.");
        show_orientation(fwide(fp, query));
     
        puts("2) Establish byte orientation.");
        show_orientation(fwide(fp, narrow));
        try_read(fp);
     
        puts("3) Only freopen() can reset stream orientation.");
        if (freopen("main.cpp", "r", fp) == NULL)
        {
           perror("freopen() failed");
           return EXIT_FAILURE;
        }
     
        puts("4) A reopened stream has no orientation.");
        show_orientation(fwide(fp, query));
     
        puts("5) Establish wide orientation.");
        show_orientation(fwide(fp, wide));
        try_read(fp);
     
        fclose(fp);
    }
```

Saída possível:
```
    1) A newly opened stream has no orientation.
            no orientation
    2) Establish byte orientation.
            narrow orientation
            narrow character read '#'
            wide character read failed
    3) Only freopen() can reset stream orientation.
    4) A reopened stream has no orientation.
            no orientation
    5) Establish wide orientation.
            wide orientation
            narrow character read failed
            wide character read '#'
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.29.3.5 A função fwide (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.29.3.5 A função fwide (p: 309)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.29.3.5 A função fwide (p: 423)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.24.3.5 A função fwide (p: 369)

### Veja também

[ fopenfopen_s](<#/doc/io/fopen>)(C11) | abre um arquivo
(função)
[Documentação C++](<#/>) para fwide