# strtoimax, strtoumax

Definido no cabeçalho [`<inttypes.h>`](<#/doc/types/integer>)

```c
intmax_t strtoimax( const char* restrict nptr,
char** restrict endptr, int base );  // desde C99
uintmax_t strtoumax( const char* restrict nptr,
char** restrict endptr, int base );  // desde C99
```

Interpreta um valor inteiro em uma string de bytes apontada por nptr.

Descarta quaisquer caracteres de espaço em branco (identificados pela chamada de [`isspace`](<#/doc/string/byte/isspace>)) até que o primeiro caractere não-espaço em branco seja encontrado, então pega o máximo de caracteres possível para formar uma representação de número inteiro válida de _base-n_ (onde n=`base`) e os converte para um valor inteiro. O valor inteiro válido consiste nas seguintes partes:

* (opcional) sinal de mais ou menos
* (opcional) prefixo (`0`) indicando base octal (aplica-se apenas quando a base é 8 ou ​0​)
* (opcional) prefixo (`0x` ou `0X`) indicando base hexadecimal (aplica-se apenas quando a base é 16 ou ​0​)
* uma sequência de dígitos

O conjunto de valores válidos para base é `{0, 2, 3, ..., 36}`. O conjunto de dígitos válidos para inteiros de base-`2` é `{0, 1}`, para inteiros de base-`3` é `{0, 1, 2}`, e assim por diante. Para bases maiores que `10`, os dígitos válidos incluem caracteres alfabéticos, começando de `Aa` para inteiros de base-`11`, até `Zz` para inteiros de base-`36`. A distinção entre maiúsculas e minúsculas dos caracteres é ignorada.

Formatos numéricos adicionais podem ser aceitos pela [locale](<#/doc/locale/setlocale>) C atualmente instalada.

Se o valor de `base` for ​0​, a base numérica é auto-detectada: se o prefixo for `0`, a base é octal; se o prefixo for `0x` ou `0X`, a base é hexadecimal; caso contrário, a base é decimal.

Se o sinal de menos fez parte da sequência de entrada, o valor numérico calculado a partir da sequência de dígitos é negado como se por [menos unário](<#/doc/language/operator_arithmetic>) no tipo de resultado.

As funções definem o ponteiro apontado por endptr para apontar para o caractere após o último caractere interpretado. Se endptr for um ponteiro nulo, ele é ignorado.

Se nptr estiver vazio ou não tiver o formato esperado, nenhuma conversão é realizada, e (se endptr não for um ponteiro nulo) o valor de nptr é armazenado no objeto apontado por endptr.

### Parâmetros

- **nptr** — ponteiro para a string de bytes terminada em nulo a ser interpretada
- **endptr** — ponteiro para um ponteiro para caractere
- **base** — _base_ do valor inteiro interpretado

### Valor de retorno

* Em caso de sucesso, um valor inteiro correspondente ao conteúdo de `str` é retornado.
* Se o valor convertido estiver fora do intervalo do tipo de retorno correspondente, ocorre um erro de intervalo (definindo [errno](<#/doc/error/errno>) para [ERANGE](<#/doc/error/errno_macros>)) e [INTMAX_MAX](<#/doc/types/integer>), [INTMAX_MIN](<#/doc/types/integer>), [UINTMAX_MAX](<#/doc/types/integer>) ou ​0​ é retornado, conforme apropriado.
* Se nenhuma conversão puder ser realizada, ​0​ é retornado.

### Exemplo

Execute este código
```c
    #include <errno.h>
    #include <inttypes.h>
    #include <stdio.h>
    #include <string.h>
    
    int main(void)
    {
        char* endptr = NULL;
    
        printf("%ld\n", strtoimax(" -123junk", &endptr, 10)); // base 10
        printf("%ld\n", strtoimax("11111111", &endptr, 2));   // base 2
        printf("%ld\n", strtoimax("XyZ", &endptr, 36));       // base 36
        printf("%ld\n", strtoimax("010", &endptr, 0));        // octal auto-detection
        printf("%ld\n", strtoimax("10", &endptr, 0));         // decimal auto-detection
        printf("%ld\n", strtoimax("0x10", &endptr, 0));       // hexadecimal auto-detection
    
        // range error: LONG_MAX+1 --> LONG_MAX
        errno = 0;
        printf("%ld\n", strtoimax("9223372036854775808", &endptr, 10));
        printf("%s\n", strerror(errno));
    }
```

Saída:
```
    -123
    255
    44027
    8
    10
    16
    9223372036854775807
    Numerical result out of range
```

### Referências

* Padrão C23 (ISO/IEC 9899:2024):

  * 7.8.2.3 As funções strtoimax e strtoumax (p: TBD)

* Padrão C17 (ISO/IEC 9899:2018):

  * 7.8.2.3 As funções strtoimax e strtoumax (p: TBD)

* Padrão C11 (ISO/IEC 9899:2011):

  * 7.8.2.3 As funções strtoimax e strtoumax (p: 219)

* Padrão C99 (ISO/IEC 9899:1999):

  * 7.8.2.3 As funções strtoimax e strtoumax (p: 200)

### Veja também

[ wcstoimaxwcstoumax](<#/doc/string/wide/wcstoimax>)(C99)(C99) | converte uma string larga para [intmax_t](<#/doc/types/integer>) ou [uintmax_t](<#/doc/types/integer>)
(função)
[ strtolstrtoll](<#/doc/string/byte/strtol>)(C99) | converte uma string de bytes para um valor inteiro
(função)
[ strtoul strtoull](<#/doc/string/byte/strtoul>)(C99) | converte uma string de bytes para um valor inteiro sem sinal
(função)
[Documentação C++](<#/>) para strtoimax, strtoumax