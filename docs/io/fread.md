# fread

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
size_t fread( void *buffer, size_t size, size_t count,
FILE *stream );  // ate C99
size_t fread( void *restrict buffer, size_t size, size_t count,
FILE *restrict stream );  // desde C99
```

Lê até count objetos para o array buffer do fluxo de entrada stream fornecido, como se chamasse [fgetc](<#/doc/io/fgetc>) size vezes para cada objeto, e armazenasse os resultados, na ordem obtida, nas posições sucessivas de buffer, que é reinterpretado como um array de unsigned char. O indicador de posição do arquivo para o fluxo é avançado pelo número de caracteres lidos.

Se ocorrer um erro, o valor resultante do indicador de posição do arquivo para o fluxo é indeterminado. Se um elemento parcial for lido, seu valor é indeterminado.

### Parâmetros

- **buffer** — ponteiro para o array onde os objetos lidos são armazenados
- **size** — tamanho de cada objeto em bytes
- **count** — o número de objetos a serem lidos
- **stream** — o fluxo a ser lido

### Valor de retorno

Número de objetos lidos com sucesso, que pode ser menor que count se ocorrer um erro ou condição de fim de arquivo.

Se size ou count for zero, `fread` retorna zero e não executa nenhuma outra ação.

`fread` não distingue entre fim de arquivo e erro, e os chamadores devem usar [feof](<#/doc/io/feof>) e [ferror](<#/doc/io/ferror>) para determinar qual ocorreu.

### Exemplo

Execute este código
```c
    #include <stdio.h>
     
    enum { SIZE = 5 };
     
    int main(void)
    {
        const double a[SIZE] = {1.0, 2.0, 3.0, 4.0, 5.0};
        printf("Array has size %ld bytes, element size: %ld\n", sizeof a, sizeof *a);
        FILE *fp = fopen("test.bin", "wb"); // must use binary mode
        fwrite(a, sizeof *a, SIZE, fp); // writes an array of doubles
        fclose(fp);
     
        double b[SIZE];
        fp = fopen("test.bin","rb");
        const size_t ret_code = fread(b, sizeof b[0], SIZE, fp); // reads an array of doubles
        if (ret_code == SIZE)
        {
            printf("Array at %p read successfully, contents:\n", (void*)&a);
            for (int n = 0; n != SIZE; ++n)
                printf("%f ", b[n]);
            putchar('\n');
        }
        else // error handling
        {
            if (feof(fp))
                printf("Error reading test.bin: unexpected end of file\n");
            else if (ferror(fp))
                perror("Error reading test.bin");
        }
     
        fclose(fp);
    }
```

Saída possível:
```
    Array has size 40 bytes, element size: 8
    Array at 0x1337f00d6960 read successfully, contents:
    1.000000 2.000000 3.000000 4.000000 5.000000
```

### Referências

* Padrão C23 (ISO/IEC 9899:2024):

  * 7.21.8.1 A função fread (p: TBD)

* Padrão C17 (ISO/IEC 9899:2018):

  * 7.21.8.1 A função fread (p: 243-244)

* Padrão C11 (ISO/IEC 9899:2011):

  * 7.21.8.1 A função fread (p: 335)

* Padrão C99 (ISO/IEC 9899:1999):

  * 7.19.8.1 A função fread (p: 301)

* Padrão C89/C90 (ISO/IEC 9899:1990):

  * 4.9.8.1 A função fread

### Veja também

[ scanffscanfsscanfscanf_sfscanf_ssscanf_s](<#/doc/io/fscanf>)(C11)(C11)(C11) | lê entrada formatada de [stdin](<#/doc/io/std_streams>), um fluxo de arquivo ou um buffer
(função)
[ fgets](<#/doc/io/fgets>) | obtém uma string de caracteres de um fluxo de arquivo
(função)
[ fwrite](<#/doc/io/fwrite>) | escreve em um arquivo
(função)
[Documentação C++](<#/>) para fread