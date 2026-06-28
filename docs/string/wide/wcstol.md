# wcstol, wcstoll

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
long wcstol( const wchar_t * str, wchar_t ** str_end, int base );  // desde C95
(até C99)  // até C99
long wcstol( const wchar_t * restrict str, wchar_t ** restrict str_end,
int base );  // desde C99
long long wcstoll( const wchar_t * restrict str, wchar_t ** restrict str_end,
int base );  // desde C99
```

  
Interpreta um valor inteiro em uma string larga apontada por `str`.

Descarta quaisquer caracteres de espaço em branco (identificados pela chamada a [`iswspace`](<#/doc/string/wide/iswspace>)) até que o primeiro caractere não-espaço em branco seja encontrado, então pega tantos caracteres quanto possível para formar uma representação de número inteiro válida de _base-n_ (onde n=`base`) e os converte para um valor inteiro. O valor inteiro válido consiste nas seguintes partes:

  * (opcional) sinal de mais ou menos
  * (opcional) prefixo (`0`) indicando base octal (aplica-se apenas quando a base é 8 ou ​0​)
  * (opcional) prefixo (`0x` ou `0X`) indicando base hexadecimal (aplica-se apenas quando a base é 16 ou ​0​)
  * uma sequência de dígitos

O conjunto de valores válidos para `base` é `{0, 2, 3, ..., 36}`. O conjunto de dígitos válidos para inteiros de base-`2` é `{0, 1}`, para inteiros de base-`3` é `{0, 1, 2}`, e assim por diante. Para bases maiores que `10`, os dígitos válidos incluem caracteres alfabéticos, começando de `Aa` para inteiros de base-`11`, até `Zz` para inteiros de base-`36`. A caixa dos caracteres é ignorada.

Formatos numéricos adicionais podem ser aceitos pela [locale](<#/doc/locale/setlocale>) C atualmente instalada.

Se o valor de `base` for ​0​, a base numérica é auto-detectada: se o prefixo for `0`, a base é octal, se o prefixo for `0x` ou `0X`, a base é hexadecimal, caso contrário a base é decimal.

Se o sinal de menos fez parte da sequência de entrada, o valor numérico calculado a partir da sequência de dígitos é negado como se por [menos unário](<#/doc/language/operator_arithmetic>) no tipo de resultado.

As funções definem o ponteiro apontado por `str_end` para apontar para o caractere largo após o último caractere interpretado. Se `str_end` for um ponteiro nulo, ele é ignorado.

### Parâmetros

str  |  \-  |  ponteiro para a string larga terminada em nulo a ser interpretada   
str_end  |  \-  |  ponteiro para um ponteiro para caractere largo   
base  |  \-  |  _base_ do valor inteiro interpretado   
  
### Valor de retorno

Valor inteiro correspondente ao conteúdo de `str` em caso de sucesso. Se o valor convertido estiver fora do intervalo do tipo de retorno correspondente, ocorre um erro de intervalo e [LONG_MAX](<#/doc/types/limits>), [LONG_MIN](<#/doc/types/limits>), [LLONG_MAX](<#/doc/types/limits>) ou [LLONG_MIN](<#/doc/types/limits>) é retornado. Se nenhuma conversão puder ser realizada, ​0​ é retornado.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <errno.h>
    #include <wchar.h>
     
    int main(void)
    {
        const wchar_t *p = L"10 200000000000000000000000000000 30 -40";
        printf("Parsing L'%ls':\n", p);
        wchar_t *end;
        for (long i = wcstol(p, &end, 10);
             p != end;
             i = wcstol(p, &end, 10))
        {
            printf("'%.*ls' -> ", (int)(end-p), p);
            p = end;
            if (errno == ERANGE){
                printf("range error, got ");
                errno = 0;
            }
            printf("%ld\n", i);
        }
    }
```

Saída:
```
    Parsing L'10 200000000000000000000000000000 30 -40':
    '10' -> 10
    ' 200000000000000000000000000000' -> range error, got 9223372036854775807
    ' 30' -> 30
    ' -40' -> -40
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.29.4.1.2 As funções wcstol, wcstoll, wcstoul e wcstoull (p: 429-430) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.24.4.1.2 As funções wcstol, wcstoll, wcstoul e wcstoull (p: 375-376) 

### Veja também

[ strtolstrtoll](<#/doc/string/byte/strtol>)(desde C99) |  converte uma string de bytes para um valor inteiro   
(função)  
[ wcstoulwcstoull](<#/doc/string/wide/wcstoul>)(desde C95)(desde C99) |  converte uma string larga para um valor inteiro sem sinal   
(função)  
[Documentação C++](<#/>) para wcstol, wcstoll