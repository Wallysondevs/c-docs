# ftell

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
long ftell( FILE* stream );
```

Retorna o indicador de posição do arquivo para o fluxo de arquivo stream.

Se o fluxo estiver aberto em modo binário, o valor obtido por esta função é o número de bytes desde o início do arquivo.

Se o fluxo estiver aberto em modo texto, o valor retornado por esta função é não especificado e só é significativo como entrada para [fseek()](<#/doc/io/fseek>).

### Parâmetros

- **stream** — fluxo de arquivo a ser examinado

### Valor de retorno

Indicador de posição do arquivo em caso de sucesso ou -1L se ocorrer falha.

Em caso de erro, a variável errno é definida para um valor positivo definido pela implementação.

### Notas

No Windows, [`_ftelli64`](<https://learn.microsoft.com/en-us/cpp/c-runtime-library/reference/ftell-ftelli64>) pode ser usado para trabalhar com arquivos maiores que 2 GiB.

### Exemplo

Demonstra `ftell()` com verificação de erros. Escreve e depois lê alguns valores de ponto flutuante (FP) de/para um arquivo.

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
    
    /* Se a condição não for atendida, encerra o programa com mensagem de erro. */
    void check(_Bool condition, const char* func, int line)
    {
        if (condition)
            return;
        perror(func);
        fprintf(stderr, "%s failed in file %s at line # %d\n", func, __FILE__, line - 1);
        exit(EXIT_FAILURE);
    }
    
    int main(void)
    {
        /* Prepara um array de valores FP. */
        #define SIZE 5
        double A[SIZE] = {1.1, 2.0, 3.0, 4.0, 5.0};
    
        /* Escreve o array em um arquivo. */
        const char* fname = "/tmp/test.bin";
        FILE* file = fopen(fname, "wb");
        check(file != NULL, "fopen()", __LINE__);
    
        const int write_count = fwrite(A, sizeof(double), SIZE, file);
        check(write_count == SIZE, "fwrite()", __LINE__);
    
        fclose(file);
    
        /* Lê os valores FP para o array B. */
        double B[SIZE];
        file = fopen(fname, "rb");
        check(file != NULL, "fopen()", __LINE__);
    
        long int pos = ftell(file); /* indicador de posição no início do arquivo */
        check(pos != -1L, "ftell()", __LINE__);
        printf("pos: %ld\n", pos);
    
        const int read_count = fread(B, sizeof(double), 1, file); /* lê um valor FP */
        check(read_count == 1, "fread()", __LINE__);
    
        pos = ftell(file); /* indicador de posição após ler um valor FP */
        check(pos != -1L, "ftell()", __LINE__);
        printf("pos: %ld\n", pos);
        printf("B[0]: %.1f\n", B[0]); /* imprime um valor FP */
    
        return EXIT_SUCCESS;
    }
```

Saída possível:
```
    pos: 0
    pos: 8
    B[0]: 1.1
```

### Referências

* Padrão C23 (ISO/IEC 9899:2024):

  * 7.21.9.4 A função ftell (p: TBD)

* Padrão C17 (ISO/IEC 9899:2018):

  * 7.21.9.4 A função ftell (p: TBD)

* Padrão C11 (ISO/IEC 9899:2011):

  * 7.21.9.4 A função ftell (p: 337-338)

* Padrão C99 (ISO/IEC 9899:1999):

  * 7.19.9.4 A função ftell (p: 303-304)

* Padrão C89/C90 (ISO/IEC 9899:1990):

  * 4.9.9.4 A função ftell

### Veja também

[ fgetpos](<#/doc/io/fgetpos>) | obtém o indicador de posição do arquivo
(função)
[ fseek](<#/doc/io/fseek>) | move o indicador de posição do arquivo para um local específico em um arquivo
(função)
[ fsetpos](<#/doc/io/fsetpos>) | move o indicador de posição do arquivo para um local específico em um arquivo
(função)
[Documentação C++](<#/>) para ftell