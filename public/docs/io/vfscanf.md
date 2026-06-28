# vscanf, vfscanf, vsscanf, vscanf_s, vfscanf_s, vsscanf_s

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
int vscanf( const char *restrict format, va_list vlist );  // desde C99
int vfscanf( FILE *restrict stream, const char *restrict format,
va_list vlist );  // desde C99
int vsscanf( const char *restrict buffer, const char *restrict format,
va_list vlist );  // desde C99
int vscanf_s(const char *restrict format, va_list vlist);  // desde C11
int vfscanf_s( FILE *restrict stream, const char *restrict format,
va_list vlist);  // desde C11
int vsscanf_s( const char *restrict buffer, const char *restrict format,
va_list vlist);  // desde C11
```

Lê dados de uma variedade de fontes, interpreta-os de acordo com `format` e armazena os resultados nos locais definidos por `vlist`.

1) Lê os dados de [stdin](<#/doc/io/std_streams>)

2) Lê os dados do fluxo de arquivo `stream`

3) Lê os dados da string de caracteres terminada em nulo `buffer`. Atingir o fim da string é equivalente a atingir a condição de fim de arquivo para `fscanf`

4-6) O mesmo que (1-3), exceto que os especificadores de conversão %c, %s e %[ esperam cada um dois argumentos (o ponteiro usual e um valor do tipo rsize_t indicando o tamanho do array de recebimento, que pode ser 1 ao ler com %c em um único char) e exceto que os seguintes erros são detectados em tempo de execução e chamam a função de [manipulador de restrição](<#/doc/error/set_constraint_handler_s>) atualmente instalada:

  * qualquer um dos argumentos do tipo ponteiro é um ponteiro nulo
  * `format`, `stream`, ou `buffer` é um ponteiro nulo
  * o número de caracteres que seriam escritos por %c, %s ou %[, mais o caractere nulo de terminação, excederia o segundo argumento (rsize_t) fornecido para cada um desses especificadores de conversão
  * opcionalmente, qualquer outro erro detectável, como um especificador de conversão desconhecido

Assim como todas as funções com verificação de limites, `vscanf_s`, `vfscanf_s` e `vsscanf_s` são garantidas de estarem disponíveis apenas se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir [`<stdio.h>`](<#/doc/io>).

### Parâmetros

- **stream** — fluxo de arquivo de entrada para ler
- **buffer** — ponteiro para uma string de caracteres terminada em nulo para ler
- **format** — ponteiro para uma string de caracteres terminada em nulo especificando como ler a entrada
- **vlist** — lista de argumentos variáveis contendo os argumentos de recebimento.

A string de **formato** consiste em

  * caracteres multibyte não-espaço em branco, exceto %: cada caractere desse tipo na string de formato consome exatamente um caractere idêntico do fluxo de entrada, ou faz com que a função falhe se o próximo caractere no fluxo não for igual.
  * caracteres de espaço em branco: qualquer caractere de espaço em branco único na string de formato consome todos os caracteres de espaço em branco consecutivos disponíveis da entrada (determinado como se chamando [`isspace`](<#/doc/string/byte/isspace>) em um loop). Note que não há diferença entre "\n", " ", "\t\t", ou outros espaços em branco na string de formato.
  * especificações de conversão. Cada especificação de conversão tem o seguinte formato:

  * caractere % introdutório.

  * (opcional) caractere * de supressão de atribuição. Se esta opção estiver presente, a função não atribui o resultado da conversão a nenhum argumento de recebimento.

  * (opcional) número inteiro (maior que zero) que especifica a _largura máxima do campo_, ou seja, o número máximo de caracteres que a função pode consumir ao fazer a conversão especificada pela especificação de conversão atual. Note que %s e %[ podem levar a estouro de buffer se a largura não for fornecida.

  * (opcional) _modificador de comprimento_ que especifica o tamanho do argumento de recebimento, ou seja, o tipo de destino real. Isso afeta a precisão da conversão e as regras de estouro. O tipo de destino padrão é diferente para cada tipo de conversão (veja a tabela abaixo).

  * especificador de formato de conversão.

Os seguintes especificadores de formato estão disponíveis:

Especificador de
conversão | Explicação | Tipo de argumento
**Modificador de comprimento →** | `hh` (C99) | `h` | (nenhum) | `l` | `ll` (C99) | `j` (C99) | `z` (C99) | `t` (C99) | `L`
`%` | Corresponde ao literal `%`. | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A
`c` |

    Corresponde a um **caractere** ou a uma sequência de **caracteres**.
Se um especificador de largura for usado, corresponde exatamente a _width_ caracteres (o argumento deve ser um ponteiro para um array com espaço suficiente). Ao contrário de %s e %[, não anexa o caractere nulo ao array. | N/A | N/A | char* | wchar_t* | N/A | N/A | N/A | N/A | N/A
`s` |

    Corresponde a uma sequência de caracteres não-espaço em branco (uma **string**).
Se um especificador de largura for usado, corresponde até _width_ ou até o primeiro caractere de espaço em branco, o que aparecer primeiro. Sempre armazena um caractere nulo além dos caracteres correspondidos (portanto, o array de argumento deve ter espaço para pelo menos _width+1_ caracteres)
`[`set`]` |

    Corresponde a uma sequência não vazia de caracteres de um conjunto de caracteres.
Se o primeiro caractere do conjunto for `^`, então todos os caracteres que não estão no conjunto são correspondidos. Se o conjunto começar com `]` ou `^]`, então o caractere `]` também é incluído no conjunto. É definido pela implementação se o caractere `-` na posição não inicial no scanset pode indicar um intervalo, como em `[0-9]`. Se um especificador de largura for usado, corresponde apenas até _width_. Sempre armazena um caractere nulo além dos caracteres correspondidos (portanto, o array de argumento deve ter espaço para pelo menos _width+1_ caracteres)
`d` |

    Corresponde a um **inteiro decimal**.
O formato do número é o mesmo esperado por [`strtol`](<#/doc/string/byte/strtol>) com o valor 10 para o argumento `base` | signed char* ou unsigned char* | signed short* ou unsigned short* | signed int* ou unsigned int* | signed long* ou unsigned long* | signed long long* ou unsigned long long* | [intmax_t](<#/doc/types/integer>)* ou [uintmax_t](<#/doc/types/integer>)* | [size_t](<#/doc/types/size_t>)* | [ptrdiff_t](<#/doc/types/ptrdiff_t>)* | N/A
`i` |

    Corresponde a um **inteiro**.
O formato do número é o mesmo esperado por [`strtol`](<#/doc/string/byte/strtol>) com o valor ​0​ para o argumento `base` (a base é determinada pelos primeiros caracteres analisados)
`u` |

    Corresponde a um **inteiro decimal** sem sinal.
O formato do número é o mesmo esperado por [`strtoul`](<#/doc/string/byte/strtoul>) com o valor 10 para o argumento `base`.
`o` |

    Corresponde a um **inteiro octal** sem sinal.
O formato do número é o mesmo esperado por [`strtoul`](<#/doc/string/byte/strtoul>) com o valor 8 para o argumento `base`
`x`, `X` |

    Corresponde a um **inteiro hexadecimal** sem sinal.
O formato do número é o mesmo esperado por [`strtoul`](<#/doc/string/byte/strtoul>) com o valor 16 para o argumento `base`
`n` |

    Retorna o **número de caracteres lidos até agora**.
Nenhuma entrada é consumida. Não incrementa a contagem de atribuições. Se o especificador tiver o operador de supressão de atribuição definido, o comportamento é indefinido
`a`, `A`(C99)
`e`, `E`
`f`, `F`(C99)
`g`, `G` |

    Corresponde a um **número de ponto flutuante**.
O formato do número é o mesmo esperado por [`strtof`](<#/doc/string/byte/strtof>) | N/A | N/A | float* | double* | N/A | N/A | N/A | N/A | long double*
`p` |

    Corresponde a uma sequência de caracteres definida pela implementação que define um **ponteiro**.
A família de funções `printf` deve produzir a mesma sequência usando o especificador de formato `%p` | N/A | N/A | void** | N/A | N/A | N/A | N/A | N/A | N/A

Para cada especificador de conversão diferente de n, a sequência mais longa de caracteres de entrada que não excede nenhuma largura de campo especificada e que é exatamente o que o especificador de conversão espera ou é um prefixo de uma sequência que ele esperaria, é o que é consumido do fluxo. O primeiro caractere, se houver, após esta sequência consumida permanece não lido. Se a sequência consumida tiver comprimento zero ou se a sequência consumida não puder ser convertida conforme especificado acima, ocorre uma falha de correspondência, a menos que o fim do arquivo, um erro de codificação ou um erro de leitura tenha impedido a entrada do fluxo, caso em que é uma falha de entrada.

Todos os especificadores de conversão, exceto [, c e n, consomem e descartam todos os caracteres de espaço em branco iniciais (determinados como se chamando [`isspace`](<#/doc/string/byte/isspace>)) antes de tentar analisar a entrada. Esses caracteres consumidos não contam para a largura máxima de campo especificada.

Os especificadores de conversão lc, ls e l[ realizam a conversão de caracteres multibyte para wide como se chamassem [`mbrtowc`](<#/doc/string/multibyte/mbrtowc>) com um objeto [`mbstate_t`](<#/doc/string/multibyte/mbstate_t>) inicializado para zero antes que o primeiro caractere seja convertido.

Os especificadores de conversão s e [ sempre armazenam o terminador nulo além dos caracteres correspondidos. O tamanho do array de destino deve ser pelo menos um maior do que a largura de campo especificada. O uso de %s ou %[, sem especificar o tamanho do array de destino, é tão inseguro quanto [`gets`](<#/doc/io/gets>).

As especificações de conversão corretas para os [tipos inteiros de largura fixa](<#/doc/types/integer>) ([int8_t](<#/doc/types/integer>), etc) são definidas no cabeçalho [`<inttypes.h>`](<#/doc/types/integer>) (embora [`SCNdMAX`](<#/doc/types/integer>), [`SCNuMAX`](<#/doc/types/integer>), etc seja sinônimo de %jd, %ju, etc).

Existe um [ponto de sequência](<#/doc/language/eval_order>) após a ação de cada especificador de conversão; isso permite armazenar múltiplos campos na mesma variável "sumidouro".

Ao analisar um valor de ponto flutuante incompleto que termina no expoente sem dígitos, como analisar "100er" com o especificador de conversão %f, a sequência "100e" (o prefixo mais longo de um número de ponto flutuante possivelmente válido) é consumida, resultando em um erro de correspondência (a sequência consumida não pode ser convertida em um número de ponto flutuante), com "r" restante. Algumas implementações existentes não seguem esta regra e retrocedem para consumir apenas "100", deixando "er", por exemplo, [bug 1765 do glibc](<https://sourceware.org/bugzilla/show_bug.cgi?id=1765>).

Uma especificação de conversão deve ser válida. Caso contrário, o comportamento é indefinido.

### Valor de retorno

1-3) Número de argumentos de recebimento atribuídos com sucesso, ou [EOF](<#/doc/io>) se ocorrer falha de leitura antes que o primeiro argumento de recebimento fosse atribuído.

4-6) O mesmo que (1-3), exceto que [EOF](<#/doc/io>) também é retornado se houver uma violação de restrição em tempo de execução.

### Notas

Todas essas funções invocam va_arg pelo menos uma vez, o valor de `arg` é indeterminado após o retorno. Essas funções não invocam va_end, e isso deve ser feito pelo chamador.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <stdbool.h>
    #include <stdarg.h>
    
    bool checked_sscanf(int count, const char* buf, const char *fmt, ...)
    {
        va_list ap;
        va_start(ap, fmt);
        int rc = vsscanf(buf, fmt, ap);
        va_end(ap);
        return rc == count;
    }
    
    int main(void)
    {
        int n, m;
    
        printf("Parsing '1 2'...");
        if(checked_sscanf(2, "1 2", "%d %d", &n, &m))
            puts("success");
        else
            puts("failure");
    
        printf("Parsing '1 a'...");
        if(checked_sscanf(2, "1 a", "%d %d", &n, &m))
            puts("success");
        else
            puts("failure");
    }
```

Saída:
```
    Parsing '1 2'...success
    Parsing '1 a'...failure
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

  * 7.21.6.9 A função vfscanf (p: 327)

  * 7.21.6.11 A função vscanf (p: 328)

  * 7.21.6.14 A função vsscanf (p: 330)

  * K.3.5.3.9 A função vfscanf_s (p: 597-598)

  * K.3.5.3.11 A função vscanf_s (p: 599)

  * K.3.5.3.14 A função vsscanf_s (p: 602)

  * Padrão C99 (ISO/IEC 9899:1999):

  * 7.19.6.9 A função vfscanf (p: 293)

  * 7.19.6.11 A função vscanf (p: 294)

  * 7.19.6.14 A função vsscanf (p: 295)

### Veja também

[ scanffscanfsscanfscanf_sfscanf_ssscanf_s](<#/doc/io/fscanf>)(C11)(C11)(C11) | lê entrada formatada de [stdin](<#/doc/io/std_streams>), um fluxo de arquivo ou um buffer
(função)
[ vprintfvfprintfvsprintfvsnprintfvprintf_svfprintf_svsprintf_svsnprintf_s](<#/doc/io/vfprintf>)(C99)(C11)(C11)(C11)(C11) | imprime saída formatada para [stdout](<#/doc/io/std_streams>), um fluxo de arquivo ou um buffer
usando lista de argumentos variáveis
(função)
[Documentação C++](<#/>) para vscanf, vfscanf, vsscanf