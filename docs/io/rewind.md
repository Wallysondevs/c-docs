# rewind

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
void rewind( FILE *stream );
```

  
Move o indicador de posição do arquivo para o início do stream de arquivo fornecido.

A função é equivalente a [fseek](<#/doc/io/fseek>)(stream, 0, [SEEK_SET](<#/doc/io>));, exceto que os indicadores de fim de arquivo e de erro são limpos.

A função descarta quaisquer efeitos de chamadas anteriores a [ungetc](<#/doc/io/ungetc>).

### Parâmetros

stream  |  \-  |  stream de arquivo a ser modificado   
  
### Valor de retorno

(nenhum) 

### Exemplo

Este exemplo mostra como ler um arquivo duas vezes

Execute este código
```
    #include <stdio.h>
     
    char str[20];
     
    int main(void)
    {
        FILE *f;
        char ch;
     
        f = fopen("file.txt", "w");
        for (ch = '0'; ch <= '9'; ch++) {
            fputc(ch, f);
        }
        fclose(f);
     
        f = fopen("file.txt", "r");
        fread(str, 1, 10, f);
        puts(str);
     
        rewind(f);
        fread(str, 1, 10, f);
        puts(str);
        fclose(f);
     
        return 0;
    }
```

Saída: 
```
    0123456789
    0123456789
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.21.9.5 A função rewind (p: 338) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.19.9.5 A função rewind (p: 304) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.9.9.5 A função rewind 

### Veja também

[ fseek](<#/doc/io/fseek>) |  move o indicador de posição do arquivo para um local específico em um arquivo   
(função)  
[Documentação C++](<#/>) para rewind