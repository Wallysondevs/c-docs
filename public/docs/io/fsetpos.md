# fsetpos

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
int fsetpos( FILE* stream, const fpos_t* pos );
```

Define o indicador de posição do arquivo e o estado de análise multibyte (se houver) para o fluxo de arquivo stream de acordo com o valor apontado por pos.

Além de estabelecer um novo estado de análise e posição, uma chamada a esta função desfaz os efeitos de [ungetc](<#/doc/io/ungetc>) e limpa o estado de fim de arquivo, se estiver definido.

Se ocorrer um erro de leitura ou escrita, o indicador de erro ([ferror](<#/doc/io/ferror>)) para o fluxo é definido.

### Parâmetros

- **stream** — fluxo de arquivo a ser modificado
- **pos** — ponteiro para um objeto [fpos_t](<#/doc/io/fpos_t>) a ser usado como novo valor do indicador de posição do arquivo

### Valor de retorno

​0​ em caso de sucesso, valor diferente de zero caso contrário.

### Observações

Após buscar uma posição que não seja o fim em um fluxo largo (wide stream), a próxima chamada a qualquer função de saída pode tornar o restante do arquivo indefinido, por exemplo, ao gerar uma sequência multibyte de um comprimento diferente.

### Exemplo

`fsetpos` com verificação de erro

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(void)
    {
        // Prepare an array of FP (floating-point) values.
        #define SIZE 5
        double A[SIZE] = {1.0, 2.0, 3.0, 4.0, 5.0};
        // Write array to a file.
        FILE * fp = fopen("test.bin", "wb");
        fwrite(A,sizeof(double),SIZE,fp);
        fclose (fp);
    
        // Read the FP values into array B.
        double B[SIZE];
        fp = fopen("test.bin","rb");
        fpos_t pos;
        if (fgetpos(fp, &pos)) // current position: start of file
        {
            perror("fgetpos()");
            fprintf(stderr, "fgetpos() failed in file %s at line # %d\n",
                    __FILE__, __LINE__ - 3);
            exit(EXIT_FAILURE);
        }
    
        int ret_code = fread(B,sizeof(double),1,fp); // read one FP value
        // current position: after reading one f-p value
        printf("%.1f; read count = %d\n", B[0], ret_code); // print one FP value and ret_code
    
        if (fsetpos(fp, &pos)) // reset current position to start of file
        {
            if (ferror(fp))
            {
                perror("fsetpos()");
                fprintf(stderr, "fsetpos() failed in file %s at line # %d\n", __FILE__,
                        __LINE__ - 5);
                exit(EXIT_FAILURE);
            }
        }
    
        ret_code = fread(B, sizeof(double), 1, fp); // reread first FP value
        printf("%.1f; read count = %d\n", B[0], ret_code); // print one FP value and ret_code
        fclose(fp);
    
        return EXIT_SUCCESS;
    }
```

Saída possível:
```
    1.0; read count = 1
    1.0; read count = 1
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.21.9.3 A função fsetpos (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.21.9.3 A função fsetpos (p: TBD) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.21.9.3 A função fsetpos (p: 337) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.19.9.3 A função fsetpos (p: 303) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.9.9.3 A função fsetpos 

### Veja também

[ fgetpos](<#/doc/io/fgetpos>) | obtém o indicador de posição do arquivo
(função)
[ ftell](<#/doc/io/ftell>) | retorna o indicador de posição atual do arquivo
(função)
[ fseek](<#/doc/io/fseek>) | move o indicador de posição do arquivo para um local específico em um arquivo
(função)
[Documentação C++](<#/>) para fsetpos