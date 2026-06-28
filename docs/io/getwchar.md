# getwchar

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
wint_t getwchar(void);  // desde C95
```

Lê o próximo caractere largo de [stdin](<#/doc/io/std_streams>).

### Parâmetros

(nenhum)

### Valor de retorno

o caractere largo obtido ou WEOF se um erro ocorreu ou o fim do arquivo foi atingido

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.29.3.7 A função getwchar (p: 424)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.24.3.7 A função getwchar (p: 369-370)

### Veja também

[ getchar](<#/doc/io/getchar>) | lê um caractere de [stdin](<#/doc/io/std_streams>)
(função)
[ fgetwcgetwc](<#/doc/io/fgetwc>)(C95) | obtém um caractere largo de um fluxo de arquivo
(função)
[Documentação C++](<#/>) para getwchar