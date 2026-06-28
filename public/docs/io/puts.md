# puts

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
int puts( const char* str );
```

Escreve cada caractere da string terminada em nulo str e um caractere de nova linha adicional '\n' para o fluxo de saída [stdout](<#/doc/io/std_streams>), como se executasse repetidamente [fputc](<#/doc/io/putc>).

O caractere nulo de terminação de str não é escrito.

### Parâmetros

- **str** — string de caracteres a ser escrita

### Valor de retorno

Em caso de sucesso, retorna um valor não negativo.

Em caso de falha, retorna [EOF](<#/doc/io>) e define o indicador de _erro_ (veja [ferror()](<#/doc/io/ferror>)) no `stream`.

### Observações

A função `puts` anexa o caractere de nova linha à saída, enquanto a função [fputs](<#/doc/io/fputs>) não o faz.

Diferentes implementações retornam diferentes números não negativos: algumas retornam o último caractere escrito, algumas retornam o número de caracteres escritos (ou [INT_MAX](<#/doc/types/limits>) se a string for mais longa que isso), algumas simplesmente retornam uma constante não negativa.

Uma causa típica de falha para `puts` é a falta de espaço no sistema de arquivos, quando [stdout](<#/doc/io/std_streams>) é redirecionado para um arquivo.

### Exemplo

Execute este código
```c
    #include <stdio.h>
     
    int main(void)
    {
        int rc = puts("Hello World");
     
        if (rc == EOF)
            perror("puts()"); // POSIX requires that errno is set
    }
```

Saída:
```
    Hello World
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.21.7.9 A função puts (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.21.7.9 A função puts (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.21.7.9 A função puts (p: 333)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.19.7.10 A função puts (p: 299)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 7.9.7.10 A função puts

### Veja também

[ fputs](<#/doc/io/fputs>) | escreve uma string de caracteres em um fluxo de arquivo
(função)
[ printffprintfsprintfsnprintfprintf_sfprintf_ssprintf_ssnprintf_s](<#/doc/io/fprintf>)(C99)(C11)(C11)(C11)(C11) | imprime saída formatada para [stdout](<#/doc/io/std_streams>), um fluxo de arquivo ou um buffer
(função)
[Documentação C++](<#/>) para puts