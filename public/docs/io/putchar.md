# putchar

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
int putchar( int ch );
```

  
Escreve um caractere ch para [stdout](<#/doc/io/std_streams>). Internamente, o caractere é convertido para unsigned char pouco antes de ser escrito. 

Equivalente a [putc](<#/doc/io/putc>)(ch, [stdout](<#/doc/io/std_streams>)). 

### Parâmetros

ch  |  \-  |  caractere a ser escrito   
  
### Valor de retorno

Em caso de sucesso, retorna o caractere escrito. 

Em caso de falha, retorna [EOF](<#/doc/io>) e define o indicador de _erro_ (veja [ferror()](<#/doc/io/ferror>)) em [stdout](<#/doc/io/std_streams>). 

### Exemplo

Mostra `putchar` com verificação de erro

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(void)
    {
        int ret_code = 0;
        for (char c = 'a'; (ret_code != EOF) && (c != 'z'); c++)
            ret_code = putchar(c);
    
        // Test whether EOF was reached.
        if (ret_code == EOF && ferror(stdout))
        {
            fprintf(stderr, "putchar() failed in file %s at line # %d\n",
                    __FILE__, __LINE__ - 6);
            perror("putchar()");
            exit(EXIT_FAILURE);
        }
        putchar('\n');
    
        // putchar return value is not equal to the argument
        int r = 0x1070;
        printf("\n0x%x\n", r);
        r = putchar(r);
        printf("\n0x%x\n", r);
    }
```

Saída: 
```
    abcdefghijklmnopqrstuvwxy
    
    0x1070
    p
    0x70
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.21.7.8 A função putchar (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.21.7.8 A função putchar (p: TBD) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.21.7.8 A função putchar (p: 333) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.19.7.9 A função putchar (p: 299) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.9.7.9 A função putchar 

### Veja também

[ fputcputc](<#/doc/io/putc>) |  escreve um caractere em um fluxo de arquivo   
(função)  
[Documentação C++](<#/>) para putchar