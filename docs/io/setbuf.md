# setbuf

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
void setbuf( FILE *stream, char *buffer );  // ate C99
void setbuf( FILE *restrict stream, char *restrict buffer );  // desde C99
#define BUFSIZ /*unspecified*/
```

Define o buffer interno a ser usado para operações de stream. Ele deve ter pelo menos `BUFSIZ` caracteres de comprimento.

Se `buffer` não for nulo, é equivalente a [setvbuf](<#/doc/io/setvbuf>)(stream, buffer, [_IOFBF](<#/doc/io>), [BUFSIZ](<#/doc/io>)).

Se `buffer` for nulo, é equivalente a [setvbuf](<#/doc/io/setvbuf>)(stream, [NULL](<#/doc/types/NULL>), [_IONBF](<#/doc/io>), 0), o que desativa o buffering.

### Parâmetros

- **stream** — o stream de arquivo para o qual definir o buffer
- **buffer** — ponteiro para um buffer para o stream usar. Se um ponteiro nulo for fornecido, o buffering é desativado

### Valor de retorno

Nenhum.

### Observações

Se [BUFSIZ](<#/doc/io>) não for o tamanho de buffer apropriado, [setvbuf](<#/doc/io/setvbuf>) pode ser usado para alterá-lo.

[setvbuf](<#/doc/io/setvbuf>) também deve ser usado para detectar erros, já que `setbuf` não indica sucesso ou falha.

Esta função só pode ser usada depois que `stream` tiver sido associado a um arquivo aberto, mas antes de qualquer outra operação (além de uma chamada falha para **setbuf** /`setvbuf`).

Um erro comum é definir o buffer de stdin ou stdout para um array cuja vida útil termina antes que o programa seja encerrado:
```
    int main(void) {
        char buf[BUFSIZ];
        setbuf(stdin, buf);
    } // vida útil de buf termina, comportamento indefinido
```

### Exemplo

`setbuf` pode ser usado para desativar o buffering em streams que exigem saída imediata.

Execute este código
```
    #include <stdio.h>
    #include <threads.h>
    
    int main(void)
    {
        setbuf(stdout, NULL); // stdout sem buffer
        putchar('a'); // 'a' aparece imediatamente se stdout estiver sem buffer
        thrd_sleep(&(struct timespec){.tv_sec=1}, NULL); // dorme 1 seg
        putchar('b');
    }
```

Saída:
```
    ab
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.21.5.5 A função setbuf (p: 225)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.21.5.5 A função setbuf (p: 307-308)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.19.5.5 A função setbuf (p: 273)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.9.5.5 A função setbuf

### Veja também

[ setvbuf](<#/doc/io/setvbuf>) | define o buffer e seu tamanho para um stream de arquivo
(função)
[Documentação C++](<#/>) para setbuf