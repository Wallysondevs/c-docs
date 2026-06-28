# atof

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
double atof( const char* str );
```

Interpreta um valor de ponto flutuante em uma string de bytes apontada por `str`.

A função descarta quaisquer caracteres de espaço em branco (conforme determinado por [isspace](<#/doc/string/byte/isspace>)) até que o primeiro caractere não-espaço em branco seja encontrado. Em seguida, ela pega o máximo de caracteres possível para formar uma representação de ponto flutuante válida e os converte para um valor de ponto flutuante. O valor de ponto flutuante válido pode ser um dos seguintes:

  * expressão de ponto flutuante decimal. Consiste nas seguintes partes:

    

  * (opcional) sinal de mais ou menos
  * sequência não vazia de dígitos decimais opcionalmente contendo um caractere de ponto decimal (conforme determinado pela [locale](<#/doc/locale/setlocale>) C atual) (define a mantissa)
  * (opcional) `e` ou `E` seguido por um sinal de menos ou mais opcional e uma sequência não vazia de dígitos decimais (define o expoente na base 10)

  * expressão de ponto flutuante hexadecimal. Consiste nas seguintes partes:

    

  * (opcional) sinal de mais ou menos
  * `0x` ou `0X`
  * sequência não vazia de dígitos hexadecimais opcionalmente contendo um caractere de ponto decimal (conforme determinado pela [locale](<#/doc/locale/setlocale>) C atual) (define a mantissa)
  * (opcional) `p` ou `P` seguido por um sinal de menos ou mais opcional e uma sequência não vazia de dígitos decimais (define o expoente na base 2)

  * expressão de infinito. Consiste nas seguintes partes:

    

  * (opcional) sinal de mais ou menos
  * `INF` ou `INFINITY` ignorando maiúsculas/minúsculas

  * expressão de não-é-um-número. Consiste nas seguintes partes:

    

  * (opcional) sinal de mais ou menos
  * `NAN` ou `NAN(`_char_sequence_`)` ignorando maiúsculas/minúsculas da parte `NAN`. _char_sequence_ pode conter apenas dígitos, letras latinas e underscores. O resultado é um valor de ponto flutuante NaN silencioso.

| (desde C99)
  * qualquer outra expressão que possa ser aceita pela [locale](<#/doc/locale/setlocale>) C atualmente instalada

### Parâmetros

- **str** — ponteiro para a string de bytes terminada em nulo a ser interpretada

### Valor de retorno

Valor double correspondente ao conteúdo de `str` em caso de sucesso. Se o valor convertido estiver fora do intervalo do tipo de retorno, o valor de retorno é comportamento indefinido. Se nenhuma conversão puder ser realizada, 0.0 é retornado.

### Notas

O nome significa "ASCII para float".

### Exemplo

Execute este código
```c
    #include <stdlib.h>
    #include <stdio.h>
     
    int main(void)
    {
        printf("%g\n", atof("  -0.0000000123junk"));
        printf("%g\n", atof("0.012"));
        printf("%g\n", atof("15e16"));
        printf("%g\n", atof("-0x1afp-2"));
        printf("%g\n", atof("inF"));
        printf("%g\n", atof("Nan"));
        printf("%g\n", atof("1.0e+309"));   // UB: out of range of double
        printf("%g\n", atof("0.0"));
        printf("%g\n", atof("junk"));       // no conversion can be performed
    }
```

Saída possível:
```
    -1.23e-08
    0.012
    1.5e+17
    -107.75
    inf
    nan
    inf
    0
    0
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.22.1.1 A função atof (p: 341)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.20.1.1 A função atof (p: 307)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.10.1.1 A função atof

### Veja também

[ strtofstrtodstrtold](<#/doc/string/byte/strtof>)(C99)(C99) | converte uma string de bytes para um valor de ponto flutuante
(função)
[Documentação C++](<#/>) para atof