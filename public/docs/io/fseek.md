# fseek

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
int fseek( FILE* stream, long offset, int origin );
#define SEEK_SET /* unspecified */
#define SEEK_CUR /* unspecified */
#define SEEK_END /* unspecified */
```

  
Define o indicador de posição do arquivo para o fluxo de arquivo `stream` para o valor apontado por `offset`.

Se o fluxo estiver aberto em modo binário, a nova posição é exatamente `offset` bytes medidos a partir do início do arquivo se `origin` for [SEEK_SET](<#/doc/io>), a partir da posição atual do arquivo se `origin` for [SEEK_CUR](<#/doc/io>), e a partir do final do arquivo se `origin` for [SEEK_END](<#/doc/io>). Fluxos binários não são obrigados a suportar [SEEK_END](<#/doc/io>), em particular se bytes nulos adicionais forem gerados.

Se o fluxo estiver aberto em modo texto, os únicos valores suportados para `offset` são zero (que funciona com qualquer `origin`) e um valor retornado por uma chamada anterior a [ftell](<#/doc/io/ftell>) em um fluxo associado ao mesmo arquivo (que funciona apenas com `origin` de [SEEK_SET](<#/doc/io>)).

Se o fluxo for orientado a caracteres largos (wide-oriented), as restrições de ambos os fluxos de texto e binários se aplicam (o resultado de [ftell](<#/doc/io/ftell>) é permitido com [SEEK_SET](<#/doc/io>) e `offset` zero é permitido a partir de [SEEK_SET](<#/doc/io>) e [SEEK_CUR](<#/doc/io>), mas não [SEEK_END](<#/doc/io>)).

Além de alterar o indicador de posição do arquivo, `fseek` desfaz os efeitos de [ungetc](<#/doc/io/ungetc>) e limpa o status de fim de arquivo, se aplicável.

Se ocorrer um erro de leitura ou escrita, o indicador de erro para o fluxo ([ferror](<#/doc/io/ferror>)) é definido e a posição do arquivo permanece inalterada.

### Parâmetros

stream  |  \-  |  fluxo de arquivo a ser modificado   
offset  |  \-  |  número de caracteres para deslocar a posição em relação a `origin`   
origin  |  \-  |  posição à qual `offset` é adicionado. Pode ter um dos seguintes valores: [SEEK_SET](<#/doc/io>), [SEEK_CUR](<#/doc/io>), [SEEK_END](<#/doc/io>)  
  
### Valor de retorno

​0​ em caso de sucesso, valor diferente de zero caso contrário.

### Observações

Após buscar para uma posição que não seja o fim em um fluxo de caracteres largos (wide stream), a próxima chamada a qualquer função de saída pode tornar o restante do arquivo indefinido, por exemplo, ao gerar uma sequência multibyte de um comprimento diferente.

Para fluxos de texto, os únicos valores válidos de `offset` são ​0​ (aplicável a qualquer `origin`) e um valor retornado por uma chamada anterior a [ftell](<#/doc/io/ftell>) (aplicável apenas a [SEEK_SET](<#/doc/io>)).

POSIX permite buscar além do fim do arquivo existente. Se uma saída for realizada após esta busca, qualquer leitura da lacuna retornará zero bytes. Onde suportado pelo sistema de arquivos, isso cria um _arquivo esparso_.

POSIX também exige que `fseek` primeiro execute [fflush](<#/doc/io/fflush>) se houver quaisquer dados não escritos (mas se o estado de deslocamento é restaurado é definido pela implementação).

POSIX especifica que [`fseek`](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/fseek.html>) deve retornar -1 em caso de erro e definir [errno](<#/doc/error/errno>) para indicar o erro.

No Windows, [`_fseeki64`](<https://learn.microsoft.com/en-us/cpp/c-runtime-library/reference/fseek-fseeki64>) pode ser usado para trabalhar com arquivos maiores que 2 GiB.

### Exemplo

`fseek` com verificação de erro:

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(void)
    {
        // Prepare an array of double values.
        #define SIZE 5
        double A[SIZE] = {1.0, 2.0, 3.0, 4.0, 5.0};
    
        // Write array to a file.
        FILE * fp = fopen("test.bin", "wb");
        fwrite(A, sizeof(double), SIZE, fp);
        fclose (fp);
    
        // Read the double values into array B.
        double B[SIZE];
        fp = fopen("test.bin", "rb");
    
        // Set the file position indicator in front of third double value.
        if (fseek(fp, sizeof(double) * 2L, SEEK_SET) != 0)
        {
            fprintf(stderr, "fseek() failed in file %s at line # %d\n",
                    __FILE__, __LINE__ - 2);
            fclose(fp);
            return EXIT_FAILURE;
        }
    
        int ret_code = fread(B, sizeof(double), 1, fp); // reads one double value
        printf("ret_code == %d\n", ret_code);           // prints the number of values read
        printf("B[0] == %.1f\n", B[0]);                 // prints one value
    
        fclose(fp);
        return EXIT_SUCCESS;
    }
```

Saída possível: 
```
    ret_code == 1
    B[0] == 3.0
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.23.9.2 A função fseek (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.21.9.2 A função fseek (p: 245) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.21.9.2 A função fseek (p: 336-337) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.19.9.2 A função fseek (p: 302-303) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.9.9.2 A função fseek 

### Veja também

[ fsetpos](<#/doc/io/fsetpos>) |  move o indicador de posição do arquivo para um local específico em um arquivo   
(função)  
[ fgetpos](<#/doc/io/fgetpos>) |  obtém o indicador de posição do arquivo   
(função)  
[ ftell](<#/doc/io/ftell>) |  retorna o indicador de posição atual do arquivo   
(função)  
[ rewind](<#/doc/io/rewind>) |  move o indicador de posição do arquivo para o início em um arquivo   
(função)  
[Documentação C++](<#/>) para fseek