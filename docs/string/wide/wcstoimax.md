# wcstoimax, wcstoumax

Definido no cabeçalho [`<inttypes.h>`](<#/doc/types/integer>)

```c
intmax_t wcstoimax( const wchar_t *restrict nptr,
wchar_t **restrict endptr, int base );  // desde C99
uintmax_t wcstoumax( const wchar_t *restrict nptr,
wchar_t **restrict endptr, int base );  // desde C99
```

Interpreta um valor inteiro sem sinal em uma wide string apontada por `nptr`.

Descarta quaisquer caracteres de espaço em branco (identificados pela chamada de [`iswspace`](<#/doc/string/wide/iswspace>)) até que o primeiro caractere não-espaço em branco seja encontrado, então pega o máximo de caracteres possível para formar uma representação numérica inteira sem sinal válida de _base-n_ (onde n=`base`) e os converte para um valor inteiro. O valor inteiro sem sinal válido consiste nas seguintes partes:

  * (opcional) sinal de mais ou menos
  * (opcional) prefixo (`0`) indicando base octal (aplica-se apenas quando a base é 8 ou ​0​)
  * (opcional) prefixo (`0x` ou `0X`) indicando base hexadecimal (aplica-se apenas quando a base é 16 ou ​0​)
  * uma sequência de dígitos

O conjunto de valores válidos para `base` é `{0, 2, 3, ..., 36}`. O conjunto de dígitos válidos para inteiros de base-`2` é `{0, 1}`, para inteiros de base-`3` é `{0, 1, 2}`, e assim por diante. Para bases maiores que `10`, os dígitos válidos incluem caracteres alfabéticos, começando de `Aa` para inteiros de base-`11`, até `Zz` para inteiros de base-`36`. A distinção entre maiúsculas e minúsculas dos caracteres é ignorada.

Formatos numéricos adicionais podem ser aceitos pelo [locale](<#/doc/locale/setlocale>) C atualmente instalado.

Se o valor de `base` for ​0​, a base numérica é auto-detectada: se o prefixo for `0`, a base é octal, se o prefixo for `0x` ou `0X`, a base é hexadecimal, caso contrário a base é decimal.

Se o sinal de menos fez parte da sequência de entrada, o valor numérico calculado a partir da sequência de dígitos é negado como se por [menos unário](<#/doc/language/operator_arithmetic>) no tipo de resultado, o que aplica as regras de "wraparound" de inteiros sem sinal.

As funções definem o ponteiro apontado por `endptr` para apontar para o wide character após o último caractere interpretado. Se `endptr` for um ponteiro nulo, ele é ignorado.

### Parâmetros

- **nptr** — ponteiro para a wide string terminada em nulo a ser interpretada
- **endptr** — ponteiro para um ponteiro para um wide character.
- **base** — _base_ do valor inteiro interpretado

### Valor de retorno

Valor inteiro correspondente ao conteúdo de `str` em caso de sucesso. Se o valor convertido estiver fora do intervalo do tipo de retorno correspondente, ocorre um erro de intervalo e [INTMAX_MAX](<#/doc/types/integer>), [INTMAX_MIN](<#/doc/types/integer>), [UINTMAX_MAX](<#/doc/types/integer>), ou ​0​ é retornado, conforme apropriado. Se nenhuma conversão puder ser realizada, ​0​ é retornado.

### Exemplo

Run this code
```c
    #include <errno.h>
    #include <inttypes.h>
    #include <stdio.h>
    #include <string.h>
    #include <wchar.h>
    
    int main(void)
    {
      wchar_t* endptr;
    
      wprintf(L"%ld\n", wcstoimax(L" -123junk", &endptr, 10)); /* base 10                    */
      wprintf(L"%ld\n", wcstoimax(L"11111111", &endptr, 2));   /* base 2                     */
      wprintf(L"%ld\n", wcstoimax(L"XyZ", &endptr, 36));       /* base 36                    */
      wprintf(L"%ld\n", wcstoimax(L"010", &endptr, 0));        /* auto-detecção octal        */
      wprintf(L"%ld\n", wcstoimax(L"10", &endptr, 0));         /* auto-detecção decimal      */
      wprintf(L"%ld\n", wcstoimax(L"0x10", &endptr, 0));       /* auto-detecção hexadecimal  */
    
      /* erro de intervalo       */
      /* LONG_MAX+1 --> LONG_MAX */
      errno = 0;
      wprintf(L"%ld\n", wcstoimax(L"9223372036854775808", &endptr, 10));
      wprintf(L"%s\n", strerror(errno));
    }
```

Output:
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

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.8.2.4 As funções wcstoimax e wcstoumax (p: 220)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.8.2.4 As funções wcstoimax e wcstoumax (p: 201)

### Veja também

[ strtoimaxstrtoumax](<#/doc/string/byte/strtoimax>)(C99)(C99) | converte uma string de bytes para [intmax_t](<#/doc/types/integer>) ou [uintmax_t](<#/doc/types/integer>)
(função)
[ wcstolwcstoll](<#/doc/string/wide/wcstol>)(C95)(C99) | converte uma wide string para um valor inteiro
(função)
[ wcstoulwcstoull](<#/doc/string/wide/wcstoul>)(C95)(C99) | converte uma wide string para um valor inteiro sem sinal
(função)
[Documentação C++](<#/>) para wcstoimax, wcstoumax