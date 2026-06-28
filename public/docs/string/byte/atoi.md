# atoi, atol, atoll

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
int atoi ( const char* str );
long atol ( const char* str );
long long atoll( const char* str );  // desde C99
```

Interpreta um valor inteiro em uma string de bytes apontada por str. A base implícita é sempre 10.

Descarta quaisquer caracteres de espaço em branco até que o primeiro caractere não-espaço em branco seja encontrado, então pega o máximo de caracteres possível para formar uma representação de número inteiro válida e os converte para um valor inteiro. O valor inteiro válido consiste nas seguintes partes:

  * sinal de mais ou menos (opcional)
  * dígitos numéricos

Se o valor do resultado não puder ser representado, ou seja, o valor convertido estiver fora do intervalo do tipo de retorno correspondente, o comportamento é indefinido.

### Parâmetros

- **str** — ponteiro para a string de bytes terminada em nulo a ser interpretada

### Valor de retorno

Valor inteiro correspondente ao conteúdo de str em caso de sucesso.

Se nenhuma conversão puder ser realizada, ​0​ é retornado.

### Notas

O nome significa "ASCII para inteiro".

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(void)
    {
        printf("%i\n", atoi(" -123junk"));
        printf("%i\n", atoi(" +321dust"));
        printf("%i\n", atoi("0"));
        printf("%i\n", atoi("0042")); // treated as a decimal number with leading zeros
        printf("%i\n", atoi("0x2A")); // only leading zero is converted discarding "x2A"
        printf("%i\n", atoi("junk")); // no conversion can be performed
        printf("%i\n", atoi("2147483648")); // UB: out of range of int
    }
```

Saída possível:
```
    -123
    321
    0
    42
    0
    0
    -2147483648
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.22.1.2 As funções atoi, atol e atoll (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.22.1.2 As funções atoi, atol e atoll (p: 249)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.22.1.2 As funções atoi, atol e atoll (p: 341)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.20.1.2 As funções atoi, atol e atoll (p: 307)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.10.1.2 A função atoi

    

  * 4.10.1.3 A função atol

### Veja também

[ strtolstrtoll](<#/doc/string/byte/strtol>)(C99) | converte uma string de bytes para um valor inteiro
(função)
[ strtoul strtoull](<#/doc/string/byte/strtoul>)(C99) | converte uma string de bytes para um valor inteiro sem sinal
(função)
[ wcstolwcstoll](<#/doc/string/wide/wcstol>)(C95)(C99) | converte uma wide string para um valor inteiro
(função)
[ wcstoulwcstoull](<#/doc/string/wide/wcstoul>)(C95)(C99) | converte uma wide string para um valor inteiro sem sinal
(função)
[Documentação C++](<#/>) para atoi, atol, atoll