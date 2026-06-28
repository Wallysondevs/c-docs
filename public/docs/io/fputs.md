# fputs

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
int fputs( const char* str, FILE* stream );  // até C99
int fputs( const char* restrict str, FILE* restrict stream );  // desde C99
```

Escreve cada caractere da string terminada em nulo `str` para o fluxo de saída `stream`, como se executasse repetidamente [fputc](<#/doc/io/putc>).

O caractere nulo terminador de `str` não é escrito.

### Parâmetros

- **str** — string de caracteres terminada em nulo a ser escrita
- **stream** — fluxo de saída

### Valor de retorno

Em caso de sucesso, retorna um valor não negativo.

Em caso de falha, retorna [EOF](<#/doc/io>) e define o indicador de _erro_ (veja [ferror()](<#/doc/io/ferror>)) no fluxo.

### Observações

A função relacionada [puts](<#/doc/io/puts>) anexa um caractere de nova linha à saída, enquanto `fputs` escreve a string sem modificações.

Diferentes implementações retornam diferentes números não negativos: algumas retornam o último caractere escrito, algumas retornam o número de caracteres escritos (ou [INT_MAX](<#/doc/types/limits>) se a string for mais longa que isso), algumas simplesmente retornam uma constante não negativa, como zero.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    
    int main(void)
    {
        int rc = fputs("Hello World", stdout);
    
        if (rc == EOF)
           perror("fputs()"); // POSIX requires that errno is set
    }
```

Saída:
```
    Hello World
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.21.7.4 A função fputs (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.21.7.4 A função fputs (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.21.7.4 A função fputs (p: 331-332)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.19.7.4 A função fputs (p: 297)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.9.7.4 A função fputs

### Veja também

[ printffprintfsprintfsnprintfprintf_sfprintf_ssprintf_ssnprintf_s](<#/doc/io/fprintf>)(C99)(C11)(C11)(C11)(C11) | imprime saída formatada para [stdout](<#/doc/io/std_streams>), um fluxo de arquivo ou um buffer
(função)
[ puts](<#/doc/io/puts>) | escreve uma string de caracteres para [stdout](<#/doc/io/std_streams>)
(função)
[ fgets](<#/doc/io/fgets>) | obtém uma string de caracteres de um fluxo de arquivo
(função)
[Documentação C++](<#/>) para fputs