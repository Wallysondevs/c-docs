# fwrite

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
size_t fwrite( const void* buffer, size_t size, size_t count,
FILE* stream );  // até C99
size_t fwrite( const void* restrict buffer, size_t size, size_t count,
FILE* restrict stream );  // desde C99
```

Escreve `count` objetos do `buffer` de array fornecido para o fluxo de saída `stream`. Os objetos são escritos como se cada objeto fosse reinterpretado como um array de `unsigned char` e chamando [fputc](<#/doc/io/putc>) `size` vezes para cada objeto para escrever esses `unsigned char` no fluxo, em ordem. O indicador de posição do arquivo para o fluxo é avançado pelo número de caracteres escritos.

Se ocorrer um erro, o valor resultante do indicador de posição do arquivo para o fluxo é indeterminado.

### Parâmetros

- **buffer** — ponteiro para o primeiro objeto no array a ser escrito
- **size** — tamanho de cada objeto
- **count** — o número de objetos a serem escritos
- **stream** — ponteiro para o fluxo de saída

### Valor de retorno

O número de objetos escritos com sucesso, que pode ser menor que `count` se ocorrer um erro.

Se `size` ou `count` for zero, `fwrite` retorna zero e não executa nenhuma outra ação.

### Exemplo

Execute este código
```c
    #include <assert.h>
    #include <stdio.h>
    #include <stdlib.h>
    
    enum { SIZE = 5 };
    
    int main(void)
    {
        double a[SIZE] = {1, 2, 3, 4, 5};
        FILE* f1 = fopen("file.bin", "wb");
        assert(f1);
        size_t r1 = fwrite(a, sizeof a[0], SIZE, f1);
        printf("wrote %zu elements out of %d requested\n", r1, SIZE);
        fclose(f1);
    
        double b[SIZE];
        FILE* f2 = fopen("file.bin", "rb");
        size_t r2 = fread(b, sizeof b[0], SIZE, f2);
        fclose(f2);
        printf("read back: ");
        for (size_t i = 0; i < r2; ++i)
            printf("%0.2f ", b[i]);
    }
```

Saída:
```
    wrote 5 elements out of 5 requested
    read back: 1.00 2.00 3.00 4.00 5.00
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.21.8.2 A função fwrite (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.21.8.2 A função fwrite (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.21.8.2 A função fwrite (p: 335-336)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.19.8.2 A função fwrite (p: 301-302)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.9.8.2 A função fwrite

### Veja também

[ printffprintfsprintfsnprintfprintf_sfprintf_ssprintf_ssnprintf_s](<#/doc/io/fprintf>)(C99)(C11)(C11)(C11)(C11) | imprime saída formatada para [stdout](<#/doc/io/std_streams>), um fluxo de arquivo ou um buffer
(função)
[ fputs](<#/doc/io/fputs>) | escreve uma string de caracteres em um fluxo de arquivo
(função)
[ fread](<#/doc/io/fread>) | lê de um arquivo
(função)
[Documentação C++](<#/>) para fwrite