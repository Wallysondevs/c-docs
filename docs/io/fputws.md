# fputws

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
int fputws( const wchar_t *str, FILE *stream );  // desde C95
(até C99)  // até C99
int fputws( const wchar_t * restrict str, FILE * restrict stream );  // desde C99
```

Escreve cada caractere da string larga terminada em nulo `str` para o stream de saída `stream`, como se executasse repetidamente [fputwc](<#/doc/io/fputwc>).

O caractere largo nulo terminador de `str` não é escrito.

### Parâmetros

- **str** — string larga terminada em nulo a ser escrita
- **stream** — stream de saída

### Valor de retorno

Em caso de sucesso, retorna um valor não negativo

Em caso de falha, retorna [EOF](<#/doc/io>) e define o indicador de erro (veja [ferror](<#/doc/io/ferror>)) em `stream`.

### Exemplo

Execute este código
```c
    #include <locale.h>
    #include <stdio.h>
    #include <wchar.h>
    
    int main(void)
    {
        setlocale(LC_ALL, "en_US.utf8");
        int rc = fputws(L"御休みなさい", stdout);
    
        if (rc == EOF)
           perror("fputws()"); // POSIX requires that errno is set
    }
```

Saída:
```
    御休みなさい
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.29.3.4 A função fputws (p: 423)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.24.3.4 A função fputws (p: 368)

### Veja também

[ fputs](<#/doc/io/fputs>) | escreve uma string de caracteres para um stream de arquivo
(função)
[ wprintffwprintfswprintfwprintf_sfwprintf_sswprintf_ssnwprintf_s](<#/doc/io/fwprintf>)(C95)(C95)(C95)(C11)(C11)(C11)(C11) | imprime saída formatada de caracteres largos para [stdout](<#/doc/io/std_streams>), um stream de arquivo ou um buffer
(função)
** fputws**(C95) | escreve uma string larga para um stream de arquivo
(função)
[ fgetws](<#/doc/io/fgetws>)(C95) | obtém uma string larga de um stream de arquivo
(função)
[Documentação C++](<#/>) para fputws