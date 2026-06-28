# fclose

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
int fclose( FILE* stream );
```

Fecha o fluxo de arquivo fornecido. Quaisquer dados armazenados em buffer não gravados são descarregados para o sistema operacional. Quaisquer dados armazenados em buffer não lidos são descartados.

Independentemente do sucesso da operação, o fluxo não está mais associado a um arquivo, e o buffer alocado por [setbuf](<#/doc/io/setbuf>) ou [setvbuf](<#/doc/io/setvbuf>), se houver, também é desassociado e desalocado se a alocação automática foi usada.

O comportamento é indefinido se o valor do ponteiro stream for usado após `fclose` retornar.

### Parâmetros

- **stream** — o fluxo de arquivo a ser fechado

### Valor de retorno

`0` em caso de sucesso, [EOF](<#/doc/io>) caso contrário

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(void)
    {
        const char* fname = "/tmp/unique_name.txt"; // or tmpnam(NULL);
        int is_ok = EXIT_FAILURE;
    
        FILE* fp = fopen(fname, "w+");
        if (!fp)
        {
            perror("File opening failed");
            return is_ok;
        }
        fputs("Hello, world!\n", fp);
        rewind(fp);
    
        int c; // note: int, not char, required to handle EOF
        while ((c = fgetc(fp)) != EOF) // standard C I/O file reading loop
            putchar(c);
    
        if (ferror(fp))
            puts("I/O error when reading");
        else if (feof(fp))
        {
            puts("End of file is reached successfully");
            is_ok = EXIT_SUCCESS;
        }
    
        fclose(fp);
        remove(fname);
        return is_ok;
    }
```

Saída possível:
```
    Hello, world!
    End of file is reached successfully
```

### Referências

* Padrão C23 (ISO/IEC 9899:2024):

  * 7.21.5.1 A função fclose (p: TBD)

* Padrão C17 (ISO/IEC 9899:2018):

  * 7.21.5.1 A função fclose (p: TBD)

* Padrão C11 (ISO/IEC 9899:2011):

  * 7.21.5.1 A função fclose (p: 304)

* Padrão C99 (ISO/IEC 9899:1999):

  * 7.19.5.1 A função fclose (p: 270)

* Padrão C89/C90 (ISO/IEC 9899:1990):

  * 4.9.5.1 A função fclose

### Veja também

[ fopenfopen_s](<#/doc/io/fopen>)(C11) | abre um arquivo
(função)
[ freopenfreopen_s](<#/doc/io/freopen>)(C11) | abre um fluxo existente com um nome diferente
(função)
[Documentação C++](<#/>) para fclose