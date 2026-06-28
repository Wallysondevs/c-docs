# fputc, putc

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
int fputc( int ch, FILE* stream );
int putc( int ch, FILE* stream );
```

Escreve um caractere `ch` no fluxo de saída `stream` fornecido. `putc()` pode ser implementado como uma macro e avaliar `stream` mais de uma vez, portanto, o argumento correspondente nunca deve ser uma expressão com efeitos colaterais.

Internamente, o caractere é convertido para `unsigned char` pouco antes de ser escrito.

### Parâmetros

- **ch** — caractere a ser escrito
- **stream** — fluxo de saída

### Valor de retorno

Em caso de sucesso, retorna o caractere escrito.

Em caso de falha, retorna `[EOF](<#/doc/io>)` e define o indicador de _erro_ (veja `[ferror()](<#/doc/io/ferror>)`) em `stream`.

### Exemplo

Mostra `putc` com verificação de erros

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(void)
    {
        int ret_code = 0;
        for (char c = 'a'; (ret_code != EOF) && (c != 'z'); c++)
            ret_code = putc(c, stdout);
    
        // Test whether EOF was reached.
        if (ret_code == EOF && ferror(stdout))
        {
            perror("putc()");
            fprintf(stderr, "putc() failed in file %s at line # %d\n",
                    __FILE__, __LINE__ - 7);
            exit(EXIT_FAILURE);
        }
        putc('\n', stdout);
    
        return EXIT_SUCCESS;
    }
```

Saída:
```
    abcdefghijklmnopqrstuvwxy
```

### Referências

* Padrão C23 (ISO/IEC 9899:2024):

  * 7.21.7.3 A função fputc (p: TBD)

  * 7.21.7.7 A função putc (p: TBD)

* Padrão C17 (ISO/IEC 9899:2018):

  * 7.21.7.3 A função fputc (p: TBD)

  * 7.21.7.7 A função putc (p: TBD)

* Padrão C11 (ISO/IEC 9899:2011):

  * 7.21.7.3 A função fputc (p: 331)

  * 7.21.7.7 A função putc (p: 333)

* Padrão C99 (ISO/IEC 9899:1999):

  * 7.19.7.3 A função fputc (p: 297)

  * 7.19.7.8 A função putc (p: 299)

* Padrão C89/C90 (ISO/IEC 9899:1990):

  * 4.9.7.3 A função fputc

  * 4.9.7.8 A função putc

### Veja também

[ putchar](<#/doc/io/putchar>) | escreve um caractere para [stdout](<#/doc/io/std_streams>)
(função)
[Documentação C++](<#/>) para fputc, putc