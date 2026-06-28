# strtof, strtod, strtold

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
float strtof ( const char* restrict str, char** restrict str_end );  // desde C99
double strtod ( const char* str, char** str_end );  // ate C99
double strtod ( const char* restrict str, char** restrict str_end );  // desde C99
long double strtold( const char* restrict str, char** restrict str_end );  // desde C99
```

  
Interpreta um valor de ponto flutuante em uma string de bytes apontada por str.

A função descarta quaisquer caracteres de espaço em branco (conforme determinado por [isspace](<#/doc/string/byte/isspace>)) até que o primeiro caractere não-espaço em branco seja encontrado. Em seguida, ela pega o maior número possível de caracteres para formar uma representação de ponto flutuante válida e os converte para um valor de ponto flutuante. O valor de ponto flutuante válido pode ser um dos seguintes:

  * expressão de ponto flutuante decimal. Consiste nas seguintes partes:

    

  * (opcional) sinal de mais ou menos
  * sequência não vazia de dígitos decimais opcionalmente contendo um caractere de ponto decimal (conforme determinado pela [locale](<#/doc/locale/setlocale>) C atual) (define o significando)
  * (opcional) `e` ou `E` seguido por um sinal de menos ou mais opcional e uma sequência não vazia de dígitos decimais (define o expoente na base 10)

  * expressão de ponto flutuante hexadecimal. Consiste nas seguintes partes:

    

  * (opcional) sinal de mais ou menos
  * `0x` ou `0X`
  * sequência não vazia de dígitos hexadecimais opcionalmente contendo um caractere de ponto decimal (conforme determinado pela [locale](<#/doc/locale/setlocale>) C atual) (define o significando)
  * (opcional) `p` ou `P` seguido por um sinal de menos ou mais opcional e uma sequência não vazia de dígitos decimais (define o expoente na base 2)

  * expressão de infinito. Consiste nas seguintes partes:

    

  * (opcional) sinal de mais ou menos
  * `INF` ou `INFINITY` ignorando maiúsculas/minúsculas

  * expressão de não-número. Consiste nas seguintes partes:

    

  * (opcional) sinal de mais ou menos
  * `NAN` ou `NAN(`_char_sequence_`)` ignorando maiúsculas/minúsculas da parte `NAN`. _char_sequence_ pode conter apenas dígitos, letras latinas e underscores. O resultado é um valor de ponto flutuante NaN silencioso.

| (desde C99)  
  
  * qualquer outra expressão que possa ser aceita pela [locale](<#/doc/locale/setlocale>) C atualmente instalada

As funções definem o ponteiro apontado por str_end para apontar para o caractere após o último caractere interpretado. Se str_end for um ponteiro nulo, ele é ignorado.

### Parâmetros

str  |  \-  |  ponteiro para a string de bytes terminada em nulo a ser interpretada   
str_end  |  \-  |  ponteiro para um ponteiro para caractere   
  
### Valor de retorno

Valor de ponto flutuante correspondente ao conteúdo de str em caso de sucesso. Se o valor convertido estiver fora do intervalo do tipo de retorno correspondente, ocorre um erro de intervalo ([errno](<#/doc/error/errno>) é definido como [ERANGE](<#/doc/error/errno_macros>)) e [HUGE_VAL](<#/doc/numeric/math/HUGE_VAL>), [HUGE_VALF](<#/doc/numeric/math/HUGE_VAL>) ou [HUGE_VALL](<#/doc/numeric/math/HUGE_VAL>) é retornado. Se nenhuma conversão puder ser realizada, ​0​ é retornado.

### Exemplo

Execute este código
```c
    #include <errno.h>
    #include <stdio.h>
    #include <stdlib.h>
     
    int main(void)
    {
        // parsing with error handling
        const char* p = "111.11 -2.22 Nan nan(2) inF 0X1.BC70A3D70A3D7P+6  1.18973e+4932zzz";
        printf("Parsing '%s':\n", p);
        char* end = NULL;
        for (double f = strtod(p, &end); p != end; f = strtod(p, &end))
        {
            printf("'%.*s' -> ", (int)(end - p), p);
            p = end;
            if (errno == ERANGE)
            {
                printf("range error, got ");
                errno = 0;
            }
            printf("%f\n", f);
        }
     
        // parsing without error handling
        printf("\"  -0.0000000123junk\"  -->  %g\n", strtod("  -0.0000000123junk", NULL));
        printf("\"junk\"                 -->  %g\n", strtod("junk", NULL));
    }
```

Saída possível: 
```
    Parsing '111.11 -2.22 Nan nan(2) inF 0X1.BC70A3D70A3D7P+6  1.18973e+4932zzz':
    '111.11' -> 111.110000
    ' -2.22' -> -2.220000
    ' Nan' -> nan
    ' nan(2)' -> nan
    ' inF' -> inf
    ' 0X1.BC70A3D70A3D7P+6' -> 111.110000
    '  1.18973e+4932' -> range error, got inf
    "  -0.0000000123junk"  -->  -1.23e-08
    "junk"                 -->  0
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.22.1.3 As funções strtod, strtof e strtold (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.22.1.3 As funções strtod, strtof e strtold (p: 249-251)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.22.1.3 As funções strtod, strtof e strtold (p: 342-344)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.20.1.3 As funções strtod, strtof e strtold (p: 308-310)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.10.1.4 A função strtod

### Veja também

[ atof](<#/doc/string/byte/atof>) |  converte uma string de bytes para um valor de ponto flutuante   
(função)  
[ wcstofwcstodwcstold](<#/doc/string/wide/wcstof>)(C99)(C95)(C99) |  converte uma string larga para um valor de ponto flutuante   
(função)  
[documentação C++](<#/>) para strtof, strtod, strtold