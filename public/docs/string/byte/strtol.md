# strtol, strtoll

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
long strtol( const char* str, char** str_end, int base );  // até C99
long strtol( const char* restrict str, char** restrict str_end, int base );  // desde C99
long long strtoll( const char* restrict str, char** restrict str_end, int base );  // desde C99
```

  
Interpreta um valor inteiro em uma string de bytes apontada por `str`.

Descarta quaisquer caracteres de espaço em branco (identificados pela chamada a [`isspace`](<#/doc/string/byte/isspace>)) até que o primeiro caractere não-espaço em branco seja encontrado, então pega o máximo de caracteres possível para formar uma representação de número inteiro válida de _base-n_ (onde n=`base`) e os converte para um valor inteiro. O valor inteiro válido consiste nas seguintes partes:

  * (opcional) sinal de mais ou menos
  * (opcional) prefixo (`0`) indicando base octal (aplica-se apenas quando a base é 8 ou ​0​)
  * (opcional) prefixo (`0x` ou `0X`) indicando base hexadecimal (aplica-se apenas quando a base é 16 ou ​0​)
  * uma sequência de dígitos

O conjunto de valores válidos para `base` é `{0, 2, 3, ..., 36}`. O conjunto de dígitos válidos para inteiros de base-`2` é `{0, 1}`, para inteiros de base-`3` é `{0, 1, 2}`, e assim por diante. Para bases maiores que `10`, os dígitos válidos incluem caracteres alfabéticos, começando de `Aa` para inteiros de base-`11`, até `Zz` para inteiros de base-`36`. A caixa dos caracteres é ignorada.

Formatos numéricos adicionais podem ser aceitos pela [locale](<#/doc/locale/setlocale>) C atualmente instalada.

Se o valor de `base` for ​0​, a base numérica é auto-detectada: se o prefixo for `0`, a base é octal, se o prefixo for `0x` ou `0X`, a base é hexadecimal, caso contrário a base é decimal.

Se o sinal de menos fez parte da sequência de entrada, o valor numérico calculado a partir da sequência de dígitos é negado como se por [menos unário](<#/doc/language/operator_arithmetic>) no tipo de resultado.

As funções definem o ponteiro apontado por `str_end` para apontar para o caractere após o último caractere numérico interpretado. Se `str_end` for um ponteiro nulo, ele é ignorado.

Se `str` estiver vazio ou não tiver o formato esperado, nenhuma conversão é realizada, e (se `str_end` não for um ponteiro nulo) o valor de `str` é armazenado no objeto apontado por `str_end`.

### Parâmetros

str  |  \-  |  ponteiro para a string de bytes terminada em nulo a ser interpretada   
str_end  |  \-  |  ponteiro para um ponteiro para caractere   
base  |  \-  |  _base_ do valor inteiro interpretado   
  
### Valor de retorno

  * Em caso de sucesso, um valor inteiro correspondente ao conteúdo de `str` é retornado.
  * Se o valor convertido estiver fora do intervalo do tipo de retorno correspondente, ocorre um erro de intervalo (definindo [errno](<#/doc/error/errno>) para [ERANGE](<#/doc/error/errno_macros>)) e [LONG_MAX](<#/doc/types/limits>), [LONG_MIN](<#/doc/types/limits>), [LLONG_MAX](<#/doc/types/limits>) ou [LLONG_MIN](<#/doc/types/limits>) é retornado.
  * Se nenhuma conversão puder ser realizada, ​0​ é retornado.

### Exemplo

Execute este código
```c
    #include <errno.h>
    #include <limits.h>
    #include <stdbool.h>
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(void)
    {
        // parsing with error handling
        const char* p = "10 200000000000000000000000000000 30 -40 junk";
        printf("Parsing '%s':\n", p);
    
        for (;;)
        {
            // errno can be set to any non-zero value by a library function call
            // regardless of whether there was an error, so it needs to be cleared
            // in order to check the error set by strtol
            errno = 0;
            char* end;
            const long i = strtol(p, &end, 10);
            if (p == end)
                break;
    
            const bool range_error = errno == ERANGE;
            printf("Extracted '%.*s', strtol returned %ld.", (int)(end-p), p, i);
            p = end;
    
            if (range_error)
                printf("\n --> Range error occurred.");
    
            putchar('\n');
        }
    
        printf("Unextracted leftover: '%s'\n\n", p);
    
        // parsing without error handling
        printf("\"1010\" in binary  --> %ld\n", strtol("1010", NULL, 2));
        printf("\"12\"   in octal   --> %ld\n", strtol("12",   NULL, 8));
        printf("\"A\"    in hex     --> %ld\n", strtol("A",    NULL, 16));
        printf("\"junk\" in base-36 --> %ld\n", strtol("junk", NULL, 36));
        printf("\"012\"  in auto-detected base --> %ld\n", strtol("012",  NULL, 0));
        printf("\"0xA\"  in auto-detected base --> %ld\n", strtol("0xA",  NULL, 0));
        printf("\"junk\" in auto-detected base --> %ld\n", strtol("junk", NULL, 0));
    }
```

Saída possível:
```
    Parsing '10 200000000000000000000000000000 30 -40 junk':
    Extracted '10', strtol returned 10.
    Extracted ' 200000000000000000000000000000', strtol returned 9223372036854775807.
     --> Range error occurred.
    Extracted ' 30', strtol returned 30.
    Extracted ' -40', strtol returned -40.
    Unextracted leftover: ' junk'
    
    "1010" in binary  --> 10
    "12"   in octal   --> 10
    "A"    in hex     --> 10
    "junk" in base-36 --> 926192
    "012"  in auto-detected base --> 10
    "0xA"  in auto-detected base --> 10
    "junk" in auto-detected base --> 0
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.22.1.4 As funções strtol, strtoll, strtoul e strtoull (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.22.1.4 As funções strtol, strtoll, strtoul e strtoull (p: 251-252) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.22.1.4 As funções strtol, strtoll, strtoul e strtoull (p: 344-345) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.20.1.4 As funções strtol, strtoll, strtoul e strtoull (p: 310-311) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.10.1.5 A função strtol 

### Veja também

[ atoiatolatoll](<#/doc/string/byte/atoi>)(C99) |  converte uma string de bytes para um valor inteiro   
(função)  
[ strtoul strtoull](<#/doc/string/byte/strtoul>)(C99) |  converte uma string de bytes para um valor inteiro sem sinal   
(função)  
[ wcstolwcstoll](<#/doc/string/wide/wcstol>)(C95)(C99) |  converte uma wide string para um valor inteiro   
(função)  
[ wcstoulwcstoull](<#/doc/string/wide/wcstoul>)(C95)(C99) |  converte uma wide string para um valor inteiro sem sinal   
(função)  
[Documentação C++](<#/>) para strtol, strtoll