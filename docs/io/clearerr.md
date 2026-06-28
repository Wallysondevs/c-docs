# clearerr

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
void clearerr( FILE *stream );
```

Reinicia os sinalizadores de erro e o indicador [`EOF`](<#/doc/io>) para o fluxo de arquivo fornecido.

### Parâmetros

- **stream** — o arquivo para o qual os sinalizadores de erro devem ser reiniciados

### Valor de retorno

(nenhum)

### Exemplo

Execute este código
```
    #include <stdio.h>
    #include <assert.h>
    
    int main(void)
    {
        FILE* tmpf = tmpfile();
        fputs("cppreference.com\n", tmpf);
        rewind(tmpf);
    
        for (int ch; (ch = fgetc(tmpf)) != EOF; putchar(ch)) { }
    
        assert(feof(tmpf)); // espera-se que o loop termine por EOF
        puts("Fim do arquivo alcançado");
    
        clearerr(tmpf); // limpa EOF
    
        puts(feof(tmpf) ? "Indicador EOF definido" 
                        : "Indicador EOF limpo");
    }
```

Saída:
```
    cppreference.com
    End of file reached
    EOF indicator cleared
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.21.10.1 A função clearerr (p: 246)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.21.10.1 A função clearerr (p: 338)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.19.10.1 A função clearerr (p: 304)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.9.10.1 A função clearerr

### Veja também

[ feof](<#/doc/io/feof>) | verifica o fim do arquivo
(função)
[ perror](<#/doc/io/perror>) | exibe uma string de caracteres correspondente ao erro atual em [stderr](<#/doc/io/std_streams>)
(função)
[ ferror](<#/doc/io/ferror>) | verifica um erro de arquivo
(função)
[Documentação C++](<#/>) para clearerr