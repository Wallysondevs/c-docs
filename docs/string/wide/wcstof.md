# wcstof, wcstod, wcstold

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
float wcstof( const wchar_t* restrict str, wchar_t** restrict str_end );  // desde C99
double wcstod( const wchar_t* str, wchar_t** str_end );  // desde C95
(ate C99)  // ate C99
double wcstod( const wchar_t* restrict str, wchar_t** restrict str_end );  // desde C99
long double wcstold( const wchar_t* restrict str, wchar_t** restrict str_end );  // desde C99
```

  
Interpreta um valor de ponto flutuante em uma string larga apontada por str.

A função descarta quaisquer caracteres de espaço em branco (conforme determinado por [iswspace](<#/doc/string/wide/iswspace>)) até que o primeiro caractere não-espaço em branco seja encontrado. Em seguida, ela pega o maior número possível de caracteres para formar uma representação de ponto flutuante válida e os converte para um valor de ponto flutuante. O valor de ponto flutuante válido pode ser um dos seguintes:

  * expressão de ponto flutuante decimal. Consiste nas seguintes partes: 

    

  * (opcional) sinal de mais ou menos 
  * sequência não vazia de dígitos decimais opcionalmente contendo um caractere de ponto decimal (conforme determinado pela [locale](<#/doc/locale/setlocale>) C atual) (define a significância) 
  * (opcional) `e` ou `E` seguido por um sinal de menos ou mais opcional e uma sequência não vazia de dígitos decimais (define o expoente na base 10) 

  * expressão de ponto flutuante hexadecimal. Consiste nas seguintes partes: 

    

  * (opcional) sinal de mais ou menos 
  * `0x` ou `0X`
  * sequência não vazia de dígitos hexadecimais opcionalmente contendo um caractere de ponto decimal (conforme determinado pela [locale](<#/doc/locale/setlocale>) C atual) (define a significância) 
  * (opcional) `p` ou `P` seguido por um sinal de menos ou mais opcional e uma sequência não vazia de dígitos decimais (define o expoente na base 2) 

  * expressão de infinito. Consiste nas seguintes partes: 

    

  * (opcional) sinal de mais ou menos 
  * `INF` ou `INFINITY` ignorando maiúsculas/minúsculas 

  * expressão de não-número. Consiste nas seguintes partes: 

    

  * (opcional) sinal de mais ou menos 
  * `NAN` ou `NAN(`_sequência_de_caracteres_`)` ignorando maiúsculas/minúsculas da parte `NAN`. _sequência_de_caracteres_ pode conter apenas dígitos, letras latinas e underscores. O resultado é um valor de ponto flutuante NaN silencioso. 

| (desde C99)  
  
  * qualquer outra expressão que possa ser aceita pela [locale](<#/doc/locale/setlocale>) C atualmente instalada

As funções definem o ponteiro apontado por str_end para apontar para o caractere largo após o último caractere interpretado. Se str_end for um ponteiro nulo, ele é ignorado.

### Parâmetros

str  |  \-  |  ponteiro para a string larga terminada em nulo a ser interpretada   
str_end  |  \-  |  ponteiro para um ponteiro para um caractere largo.   
  
### Valor de retorno

Valor de ponto flutuante correspondente ao conteúdo de str em caso de sucesso. Se o valor convertido estiver fora do intervalo do tipo de retorno correspondente, ocorre um erro de intervalo e [HUGE_VAL](<#/doc/numeric/math/HUGE_VAL>), [HUGE_VALF](<#/doc/numeric/math/HUGE_VAL>) ou [HUGE_VALL](<#/doc/numeric/math/HUGE_VAL>) é retornado. Se nenhuma conversão puder ser realizada, ​0​ é retornado. 

### Exemplo

Execute este código
```c
    #include <errno.h>
    #include <stdio.h>
    #include <wchar.h>
     
    int main(void)
    {
        const wchar_t* p = L"111.11 -2.22 0X1.BC70A3D70A3D7P+6  1.18973e+4932zzz";
        printf("Parsing L\"%ls\":\n", p);
        wchar_t* end;
        for (double f = wcstod(p, &end); p != end; f = wcstod(p, &end))
        {
            printf("'%.*ls' -> ", (int)(end-p), p);
            p = end;
            if (errno == ERANGE){
                printf("range error, got ");
                errno = 0;
            }
            printf("%f\n", f);
        }
    }
```

Saída: 
```
    Parsing L"111.11 -2.22 0X1.BC70A3D70A3D7P+6  1.18973e+4932zzz":
    '111.11' -> 111.110000
    ' -2.22' -> -2.220000
    ' 0X1.BC70A3D70A3D7P+6' -> 111.110000
    '  1.18973e+4932' -> range error, got inf
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.29.4.1.1 As funções wcstod, wcstof e wcstold (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.29.4.1.1 As funções wcstod, wcstof e wcstold (p: TBD) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.29.4.1.1 As funções wcstod, wcstof e wcstold (p: 426-428) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.24.4.1.1 As funções wcstod, wcstof e wcstold (p: 372-374) 

### Veja também

[ strtofstrtodstrtold](<#/doc/string/byte/strtof>)(C99)(C99) |  converte uma string de bytes para um valor de ponto flutuante   
(função)  
[Documentação C++](<#/>) para wcstof, wcstod, wcstold