# wcstoul, wcstoull

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
unsigned long wcstoul( const wchar_t* str, wchar_t** str_end, int base );  // desde C95
(ate C99)  // ate C99
unsigned long wcstoul( const wchar_t * restrict str,
wchar_t ** restrict str_end, int base );  // desde C99
unsigned long long wcstoull( const wchar_t * restrict str,
wchar_t ** restrict str_end, int base );  // desde C99
```

Interpreta um valor inteiro sem sinal em uma wide string apontada por `str`.

Descarta quaisquer caracteres de espaço em branco (identificados pela chamada a [`iswspace`](<#/doc/string/wide/iswspace>)) até que o primeiro caractere não-espaço em branco seja encontrado, então pega o máximo de caracteres possível para formar uma representação válida de número inteiro sem sinal de _base-n_ (onde n=`base`) e os converte para um valor inteiro. O valor inteiro sem sinal válido consiste nas seguintes partes:

  * (opcional) sinal de mais ou menos
  * (opcional) prefixo (`0`) indicando base octal (aplica-se apenas quando a base é 8 ou ​0​)
  * (opcional) prefixo (`0x` ou `0X`) indicando base hexadecimal (aplica-se apenas quando a base é 16 ou ​0​)
  * uma sequência de dígitos

O conjunto de valores válidos para `base` é `{0, 2, 3, ..., 36}`. O conjunto de dígitos válidos para inteiros de base-`2` é `{0, 1}`, para inteiros de base-`3` é `{0, 1, 2}`, e assim por diante. Para bases maiores que `10`, os dígitos válidos incluem caracteres alfabéticos, começando de `Aa` para inteiros de base-`11`, até `Zz` para inteiros de base-`36`. A distinção entre maiúsculas e minúsculas dos caracteres é ignorada.

Formatos numéricos adicionais podem ser aceitos pela [locale](<#/doc/locale/setlocale>) C atualmente instalada.

Se o valor de `base` for ​0​, a base numérica é auto-detectada: se o prefixo for `0`, a base é octal, se o prefixo for `0x` ou `0X`, a base é hexadecimal, caso contrário a base é decimal.

Se o sinal de menos fez parte da sequência de entrada, o valor numérico calculado a partir da sequência de dígitos é negado como se por [menos unário](<#/doc/language/operator_arithmetic>) no tipo de resultado, o que aplica as regras de "wraparound" de inteiros sem sinal.

As funções definem o ponteiro apontado por `str_end` para apontar para o wide character após o último caractere interpretado. Se `str_end` for um ponteiro nulo, ele é ignorado.

### Parâmetros

- **str** — ponteiro para a wide string terminada em nulo a ser interpretada
- **str_end** — ponteiro para um ponteiro para um wide character.
- **base** — _base_ do valor inteiro interpretado

### Valor de retorno

Valor inteiro correspondente ao conteúdo de `str` em caso de sucesso. Se o valor convertido estiver fora do intervalo do tipo de retorno correspondente, ocorre um erro de intervalo e [ULONG_MAX](<#/doc/types/limits>) ou [ULLONG_MAX](<#/doc/types/limits>) é retornado. Se nenhuma conversão puder ser realizada, ​0​ é retornado.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <errno.h>
    #include <wchar.h>
    
    int main(void)
    {
        const wchar_t *p = L"10 200000000000000000000000000000 30 40";
        printf("Parsing L'%ls':\n", p);
        wchar_t *end;
        for (unsigned long i = wcstoul(p, &end, 10);
             p != end;
             i = wcstoul(p, &end, 10))
        {
            printf("'%.*ls' -> ", (int)(end-p), p);
            p = end;
            if (errno == ERANGE){
                printf("range error, got ");
                errno = 0;
            }
            printf("%lu\n", i);
        }
    }
```

Saída:
```
    Parsing '10 200000000000000000000000000000 30 40':
    '10' -> 10
    ' 200000000000000000000000000000' -> range error, got 18446744073709551615
    ' 30' -> 30
    ' 40' -> 40
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.29.4.1.2 As funções wcstol, wcstoll, wcstoul e wcstoull (p: 429-430)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.24.4.1.2 As funções wcstol, wcstoll, wcstoul e wcstoull (p: 375-376)

### Veja também

[ strtoul strtoull](<#/doc/string/byte/strtoul>)(C99) | converte uma string de bytes para um valor inteiro sem sinal
(função)
[ wcstolwcstoll](<#/doc/string/wide/wcstol>)(C95)(C99) | converte uma wide string para um valor inteiro
(função)
[Documentação C++](<#/>) para wcstoul, wcstoull