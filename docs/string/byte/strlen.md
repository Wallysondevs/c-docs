# strlen, strnlen_s

Definido no cabeçalho [`<string.h>`](<#/doc/string/byte>)

```c
size_t strlen( const char* str );
size_t strnlen_s( const char* str, size_t strsz );  // desde C11
```

  
1) Retorna o comprimento da string de bytes terminada em nulo fornecida, ou seja, o número de caracteres em um array de caracteres cujo primeiro elemento é apontado por str até, mas não incluindo, o primeiro caractere nulo.

O comportamento é indefinido se str não for um ponteiro para uma string de bytes terminada em nulo.

2) O mesmo que (1), exceto que a função retorna zero se str for um ponteiro nulo e retorna strsz se o caractere nulo não for encontrado nos primeiros strsz bytes de str.

O comportamento é indefinido se str não for um ponteiro para uma string de bytes terminada em nulo e strsz for maior que o tamanho desse array de caracteres. 

    Assim como todas as funções com verificação de limites, `strnlen_s` tem sua disponibilidade garantida apenas se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir [`<string.h>`](<#/doc/string/byte>).

### Parâmetros

str  |  \-  |  ponteiro para a string de bytes terminada em nulo a ser examinada   
strsz  |  \-  |  número máximo de caracteres a serem examinados   
  
### Valor de retorno

1) O comprimento da string de bytes terminada em nulo str.

2) O comprimento da string de bytes terminada em nulo str em caso de sucesso, zero se str for um ponteiro nulo, strsz se o caractere nulo não for encontrado.

### Notas

`strnlen_s` e `wcsnlen_s` são as únicas [funções com verificação de limites](<#/doc/error>) que não invocam o manipulador de restrições de tempo de execução. Elas são funções de utilidade pura usadas para fornecer suporte limitado para strings não terminadas em nulo. 

### Exemplo

Execute este código
```
    #define __STDC_WANT_LIB_EXT1__ 1
    #include <stdio.h>
    #include <string.h>
     
    int main(void)
    {
        const char str[] = "How many characters does this string contain?";
     
        printf("without null character: %zu\n", strlen(str));
        printf("with null character:    %zu\n", sizeof str);
     
    #ifdef __STDC_LIB_EXT1__
        printf("without null character: %zu\n", strnlen_s(str, sizeof str));
    #endif
    }
```

Saída possível: 
```
    without null character: 45
    with null character:    46
    without null character: 45
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.24.6.3 A função strlen (p: TBD) 

    

  * K.3.7.4.4 A função strnlen_s (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.24.6.3 A função strlen (p: TBD) 

    

  * K.3.7.4.4 A função strnlen_s (p: TBD) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.24.6.3 A função strlen (p: 372) 

    

  * K.3.7.4.4 A função strnlen_s (p: 623) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.21.6.3 A função strlen (p: 334) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.11.6.3 A função strlen 

### Veja também

[ wcslenwcsnlen_s](<#/doc/string/wide/wcslen>)(C95)(C11) |  retorna o comprimento de uma string larga   
(função)  
[ mblen](<#/doc/string/multibyte/mblen>) |  retorna o número de bytes no próximo caractere multibyte   
(função)  
[Documentação C++](<#/>) para strlen