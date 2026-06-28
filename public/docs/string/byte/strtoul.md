# strtoul, strtoull

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
unsigned long strtoul( const char *str, char **str_end,
int base );  // ate C99
unsigned long strtoul( const char *restrict str, char **restrict str_end,
int base );  // desde C99
unsigned long long strtoull( const char *restrict str, char **restrict str_end,
int base );  // desde C99
```

Interpreta um valor inteiro sem sinal em uma string de bytes apontada por `str`.

Descarta quaisquer caracteres de espaço em branco (identificados pela chamada de [`isspace`](<#/doc/string/byte/isspace>)) até que o primeiro caractere não-espaço em branco seja encontrado, então pega o máximo de caracteres possível para formar uma representação válida de número inteiro sem sinal de _base-n_ (onde n=`base`) e os converte para um valor inteiro. O valor inteiro sem sinal válido consiste nas seguintes partes:

  * (opcional) sinal de mais ou menos
  * (opcional) prefixo (`0`) indicando base octal (aplica-se apenas quando a base é 8 ou ​0​)
  * (opcional) prefixo (`0x` ou `0X`) indicando base hexadecimal (aplica-se apenas quando a base é 16 ou ​0​)
  * uma sequência de dígitos

O conjunto de valores válidos para `base` é `{0, 2, 3, ..., 36}`. O conjunto de dígitos válidos para inteiros de base-`2` é `{0, 1}`, para inteiros de base-`3` é `{0, 1, 2}`, e assim por diante. Para bases maiores que `10`, os dígitos válidos incluem caracteres alfabéticos, começando de `Aa` para inteiros de base-`11`, até `Zz` para inteiros de base-`36`. A caixa dos caracteres é ignorada.

Formatos numéricos adicionais podem ser aceitos pela [locale](<#/doc/locale/setlocale>) C atualmente instalada.

Se o valor de `base` for ​0​, a base numérica é auto-detectada: se o prefixo for `0`, a base é octal, se o prefixo for `0x` ou `0X`, a base é hexadecimal, caso contrário a base é decimal.

Se o sinal de menos fez parte da sequência de entrada, o valor numérico calculado a partir da sequência de dígitos é negado como se por [menos unário](<#/doc/language/operator_arithmetic>) no tipo de resultado, o que aplica as regras de *wraparound* de inteiros sem sinal.

As funções definem o ponteiro apontado por `str_end` para apontar para o caractere após o último caractere interpretado. Se `str_end` for um ponteiro nulo, ele é ignorado.

### Parâmetros

- **str** — ponteiro para a string de bytes terminada em nulo a ser interpretada
- **str_end** — ponteiro para um ponteiro para caractere, pode ser definido para uma posição após o último caractere interpretado
- **base** — _base_ do valor inteiro interpretado

### Valor de retorno

Valor inteiro correspondente ao conteúdo de `str` em caso de sucesso. Se o valor convertido estiver fora do intervalo do tipo de retorno correspondente, ocorre um erro de intervalo ([errno](<#/doc/error/errno>) é definido como `ERANGE`) e [ULONG_MAX](<#/doc/types/limits>) ou [ULLONG_MAX](<#/doc/types/limits>) é retornado. Se nenhuma conversão puder ser realizada, ​0​ é retornado.

### Exemplo

Execute este código
```c
    #include <errno.h>
    #include <stdio.h>
    #include <stdlib.h>
     
    int main(void)
    {
        const char *p = "10 200000000000000000000000000000 30 -40 - 42";
        printf("Parsing '%s':\n", p);
        char *end = NULL;
        for (unsigned long i = strtoul(p, &end, 10);
             p != end;
             i = strtoul(p, &end, 10))
        {
            printf("'%.*s' -> ", (int)(end - p), p);
            p = end;
            if (errno == ERANGE)
            {
                errno = 0;
                printf("range error, got ");
            }
            printf("%lu\n", i);
        }
        printf("After the loop p points to '%s'\n", p);
    }
```

Saída:
```
    Parsing '10 200000000000000000000000000000 30 -40 - 42':
    '10' -> 10
    ' 200000000000000000000000000000' -> range error, got 18446744073709551615
    ' 30' -> 30
    ' -40' -> 18446744073709551576
    After the loop p points to ' - 42'
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.24.1.7 As funções strtol, strtoll, strtoul e strtoull (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.22.1.4 As funções strtol, strtoll, strtoul e strtoull (p: 251-252)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.22.1.4 As funções strtol, strtoll, strtoul e strtoull (p: 344-345)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.20.1.4 As funções strtol, strtoll, strtoul e strtoull (p: 310-311)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.10.1.6 A função strtoul

### Veja também

[ wcstoulwcstoull](<#/doc/string/wide/wcstoul>)(C95)(C99) | converte uma string larga para um valor inteiro sem sinal
(função)
[ atoiatolatoll](<#/doc/string/byte/atoi>)(C99) | converte uma string de bytes para um valor inteiro
(função)
[ strtolstrtoll](<#/doc/string/byte/strtol>)(C99) | converte uma string de bytes para um valor inteiro
(função)
[documentação C++](<#/>) para strtoul