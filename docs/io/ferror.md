# ferror

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
int ferror( FILE *stream );
```

  
Verifica o fluxo (stream) fornecido em busca de erros.

### Parâmetros

stream  |  \-  |  o fluxo de arquivo a ser verificado   
  
### Valor de retorno

Valor diferente de zero se o fluxo de arquivo tiver ocorrido erros, ​0​ caso contrário.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
    #include <locale.h>
    #include <wchar.h>
    
    int main(void)
    {
        char* fname = tmpnam(NULL);
        FILE* f = fopen(fname, "wb");
        fputs("\xff\xff\n", f); // not a valid UTF-8 character sequence
        fclose(f);
    
        setlocale(LC_ALL, "en_US.utf8");
        f = fopen(fname, "rb");
        wint_t ch;
        while ((ch=fgetwc(f)) != WEOF) // attempt to read as UTF-8 fails
              printf("%#x ", ch);
    
        if (feof(f))
            puts("EOF indicator set");
        if (ferror(f))
            puts("Error indicator set");
    }
```

Saída: 
```
    Error indicator set
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.21.10.3 A função ferror (p: 339) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.19.10.3 A função ferror (p: 305) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.9.10.3 A função ferror 

### Veja também

[ clearerr](<#/doc/io/clearerr>) |  limpa erros   
(função)  
[ feof](<#/doc/io/feof>) |  verifica o fim do arquivo   
(função)  
[Documentação C++](<#/>) para ferror