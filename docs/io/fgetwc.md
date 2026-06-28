# fgetwc, getwc

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
wint_t fgetwc( FILE *stream );  // desde C95
wint_t getwc( FILE *stream );  // desde C95
```

  
Lê o próximo caractere largo do stream de entrada fornecido. getwc() pode ser implementado como uma macro e pode avaliar `stream` mais de uma vez. 

### Parâmetros

stream  |  \-  |  de onde ler o caractere largo   
  
### Valor de retorno

O próximo caractere largo do stream ou WEOF em caso de falha. 

Se a falha foi causada pela condição de fim de arquivo, adicionalmente define o indicador _eof_ (veja [feof()](<#/doc/io/feof>)) no `stream`. Se a falha foi causada por algum outro erro, define o indicador _error_ (veja [ferror()](<#/doc/io/ferror>)) no `stream`. 

Se ocorreu um erro de codificação, adicionalmente define [errno](<#/doc/error/errno>) para `EILSEQ`. 

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
    #include <wchar.h>
    #include <errno.h>
    #include <locale.h>
     
    int main(void)
    {
        setlocale(LC_ALL, "en_US.utf8");
        FILE *fp = fopen("fgetwc.dat", "w");
        if(!fp) {
            perror("Can't open file for writing");
            return EXIT_FAILURE;
        }
        fputs("кошка\n", fp);
        fclose(fp);
     
        fp = fopen("fgetwc.dat", "r");
        if(!fp) {
            perror("Can't open file for reading");
            return EXIT_FAILURE;
        }
        wint_t wc;
        errno = 0;
        while ((wc = fgetwc(fp)) != WEOF)
            putwchar(wc);
     
        if (ferror(fp)) {
            if (errno == EILSEQ)
                puts("Character encoding error while reading.");
            else
                puts("I/O error when reading");
        } else if (feof(fp))
            puts("End of file reached successfully");
     
        fclose(fp);
    }
```

Saída: 
```
    кошка
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.29.3.1 A função fgetwc (p: 307-308) 

    

  * 7.29.3.6 A função getwc (p: 309) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.29.3.1 A função fgetwc (p: 421-422) 

    

  * 7.29.3.6 A função getwc (p: 424) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.24.3.1 A função fgetwc (p: 367) 

    

  * 7.24.3.6 A função getwc (p: 369) 

### Veja também

[ fgetcgetc](<#/doc/io/fgetc>) |  obtém um caractere de um stream de arquivo   
(função)  
[ fgetws](<#/doc/io/fgetws>)(C95) |  obtém uma string larga de um stream de arquivo   
(função)  
[ fputwcputwc](<#/doc/io/fputwc>)(C95) |  escreve um caractere largo em um stream de arquivo   
(função)  
[ ungetwc](<#/doc/io/ungetwc>)(C95) |  coloca um caractere largo de volta em um stream de arquivo   
(função)  
[Documentação C++](<#/>) para fgetwc