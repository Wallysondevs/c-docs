# fgetpos

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
int fgetpos( FILE* stream, fpos_t* pos );  // até C99
int fgetpos( FILE* restrict stream, fpos_t* restrict pos );  // desde C99
```

Obtém o indicador de posição do arquivo e o estado de análise atual (se houver) para o fluxo de arquivo stream e os armazena no objeto apontado por pos. O valor armazenado é significativo apenas como entrada para [fsetpos](<#/doc/io/fsetpos>).

### Parâmetros

- **stream** — fluxo de arquivo a ser examinado
- **pos** — ponteiro para um objeto [fpos_t](<#/doc/io/fpos_t>) para armazenar o indicador de posição do arquivo

### Valor de retorno

`0` em caso de sucesso, valor diferente de zero caso contrário.

### Exemplo

Execute este código
```c
    #include <assert.h>
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(void)
    {
        // prepare a file holding 4 values of type double
        enum {SIZE = 4};
        FILE* fp = fopen("test.bin", "wb");
        assert(fp);
        int rc = fwrite((double[SIZE]){1.1, 2.2, 3.3, 4.4}, sizeof(double), SIZE, fp);
        assert(rc == SIZE);
        fclose(fp);
    
        // demo using fsetpos to return to the beginning of a file
        fp = fopen("test.bin", "rb");
        fpos_t pos;
        fgetpos(fp, &pos);               // store start of file in pos
        double d;
        rc = fread(&d, sizeof d, 1, fp); // read the first double
        assert(rc == 1);
        printf("First value in the file: %.1f\n", d);
        fsetpos(fp,&pos);                // move file position back to the start of the file
        rc = fread(&d, sizeof d, 1, fp); // read the first double again
        assert(rc == 1);
        printf("First value in the file again: %.1f\n", d);
        fclose(fp);
    
        // demo error handling
        rc = fsetpos(stdin, &pos);
        if (rc)
            perror("could not fsetpos stdin");
    }
```

Saída:
```
    First value in the file: 1.1
    First value in the file again: 1.1
    could not fsetpos stdin: Illegal seek
```

### Referências

* Padrão C23 (ISO/IEC 9899:2024):

  * 7.21.9.1 A função fgetpos (p: TBD)

* Padrão C17 (ISO/IEC 9899:2018):

  * 7.21.9.1 A função fgetpos (p: TBD)

* Padrão C11 (ISO/IEC 9899:2011):

  * 7.21.9.1 A função fgetpos (p: 336)

* Padrão C99 (ISO/IEC 9899:1999):

  * 7.19.9.1 A função fgetpos (p: 302)

* Padrão C89/C90 (ISO/IEC 9899:1990):

  * 4.9.9.1 A função fgetpos

### Veja também

[ ftell](<#/doc/io/ftell>) | retorna o indicador de posição atual do arquivo
(função)
[ fseek](<#/doc/io/fseek>) | move o indicador de posição do arquivo para um local específico em um arquivo
(função)
[ fsetpos](<#/doc/io/fsetpos>) | move o indicador de posição do arquivo para um local específico em um arquivo
(função)
[Documentação C++](<#/>) para fgetpos