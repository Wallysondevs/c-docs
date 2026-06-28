# fputwc, putwc

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
wint_t fputwc( wchar_t ch, FILE* stream );  // desde C95
wint_t putwc( wchar_t ch, FILE* stream );  // desde C95
```

  
Escreve um caractere largo ch no fluxo de saída stream fornecido.

2) Pode ser implementado como uma macro e pode avaliar stream mais de uma vez.

### Parâmetros

ch  |  \-  |  caractere largo a ser escrito   
stream  |  \-  |  o fluxo de saída   
  
### Valor de retorno

Retorna uma cópia de ch em caso de sucesso.

Em caso de falha, retorna WEOF e define o indicador de _erro_ (veja [ferror()](<#/doc/io/ferror>)) em stream.

Se ocorreu um erro de codificação, adicionalmente define [errno](<#/doc/error/errno>) para [EILSEQ](<#/doc/error/errno_macros>).

### Exemplo

Execute este código
```c
    #include <errno.h>
    #include <locale.h>
    #include <stdio.h>
    #include <stdlib.h>
    #include <wchar.h>
     
    int main(void)
    {
        setlocale(LC_ALL, "en_US.utf8");
     
        errno = 0;
        if (fputwc(L'🍌', stdout) == WEOF)
        {
            if (errno == EILSEQ)
                puts("Encoding error in fputwc.");
            else
                puts("I/O error in fputwc.");
            return EXIT_FAILURE;
        }
    }
```

Saída possível: 
```
    🍌
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.31.3.3 A função fputwc (p: 430) 

    

  * 7.31.3.8 A função putwc (p: 431-432) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.29.3.3 A função fputwc (p: 308) 

    

  * 7.29.3.8 A função putwc (p: 310) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.29.3.3 A função fputwc (p: 422-423) 

    

  * 7.29.3.8 A função putwc (p: 424) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.24.3.3 A função fputwc (p: 368) 

    

  * 7.24.3.8 A função putwc (p: 370) 

### Veja também

[ fputcputc](<#/doc/io/putc>) |  escreve um caractere em um fluxo de arquivo   
(função)  
[ fputws](<#/doc/io/fputws>)(C95) |  escreve uma string larga em um fluxo de arquivo   
(função)  
[ fgetwcgetwc](<#/doc/io/fgetwc>)(C95) |  obtém um caractere largo de um fluxo de arquivo   
(função)  
[Documentação C++](<#/>) para fputwc