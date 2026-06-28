# ungetc

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
int ungetc( int ch, FILE* stream );
```

  
Se ch não for igual a [EOF](<#/doc/io>), empurra o caractere ch (reinterpretado como unsigned char) para o buffer de entrada associado ao fluxo stream de tal maneira que uma operação de leitura subsequente do fluxo recuperará esse caractere. O dispositivo externo associado ao fluxo não é modificado.

As operações de reposicionamento de fluxo [fseek](<#/doc/io/fseek>), [fsetpos](<#/doc/io/fsetpos>) e [rewind](<#/doc/io/rewind>) descartam os efeitos de `ungetc`.

Se `ungetc` for chamado mais de uma vez sem uma leitura ou reposicionamento intermediário, ele pode falhar (em outras palavras, um buffer de retorno de tamanho 1 é garantido, mas qualquer buffer maior é definido pela implementação). Se múltiplas chamadas bem-sucedidas de `ungetc` forem realizadas, as operações de leitura recuperam os caracteres retornados na ordem inversa de `ungetc`.

Se ch for igual a [EOF](<#/doc/io>), a operação falha e o fluxo não é afetado.

Uma chamada bem-sucedida a `ungetc` limpa a flag de status de fim de arquivo [feof](<#/doc/io/feof>).

Uma chamada bem-sucedida a `ungetc` em um fluxo binário decrementa o indicador de posição do fluxo em um (o comportamento é indeterminado se o indicador de posição do fluxo era zero).

Uma chamada bem-sucedida a `ungetc` em um fluxo de texto modifica o indicador de posição do fluxo de maneira não especificada, mas garante que, após todos os caracteres retornados serem recuperados com uma operação de leitura, o indicador de posição do fluxo seja igual ao seu valor antes de `ungetc`.

### Parâmetros

ch  |  \-  |  caractere a ser empurrado para o buffer de entrada do fluxo   
stream  |  \-  |  fluxo de arquivo para o qual o caractere será retornado   
  
### Valor de retorno

Em caso de sucesso, ch é retornado.

Em caso de falha, [EOF](<#/doc/io>) é retornado e o fluxo fornecido permanece inalterado.

### Notas

O tamanho do buffer de retorno varia na prática de 4k (Linux, MacOS) para tão pouco quanto 4 (Solaris) ou o mínimo garantido de 1 (HPUX, AIX).

O tamanho aparente do buffer de retorno pode ser maior se o caractere que é retornado for igual ao caractere existente naquela localização na sequência de caracteres externa (a implementação pode simplesmente decrementar o indicador de posição de leitura do arquivo e evitar manter um buffer de retorno).

### Exemplo

Demonstra o propósito original de `ungetc`: implementação de [scanf](<#/doc/io/fscanf>)

Execute este código
```
    #include <ctype.h>
    #include <stdio.h>
     
    void demo_scanf(const char* fmt, FILE* s)
    {
        while (*fmt != '\0')
        {
            if (*fmt == '%')
            {
                int c;
                switch (*++fmt)
                {
                    case 'u':
                        while (isspace(c=getc(s))) {}
                        unsigned int num = 0;
                        while (isdigit(c))
                        {
                            num = num*10 + c-'0';
                            c = getc(s);
                        }
                        printf("%%u scanned %u\n", num);
                        ungetc(c, s);
                        break;
                    case 'c':
                        c = getc(s);
                        printf("%%c scanned '%c'\n", c);
                        break;
                }
            }
            else
                ++fmt;
        }
    }
     
    int main(void)
    {
        FILE* f = fopen("input.txt", "w+");
        if (f != NULL)
        {
            fputs("123x", f);
            rewind(f);
            demo_scanf("%u%c", f);
            fclose(f);
        }
        return 0;
    }
```

Saída: 
```
    %u scanned 123
    %c scanned 'x'
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.21.7.10 A função ungetc (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.21.7.10 A função ungetc (p: 243) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.21.7.10 A função ungetc (p: 334) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.19.7.11 A função ungetc (p: 300) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.9.7.11 A função ungetc 

### Veja também

[ fgetcgetc](<#/doc/io/fgetc>) |  obtém um caractere de um fluxo de arquivo   
(função)  
[documentação C++](<#/>) para ungetc