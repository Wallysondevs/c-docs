# scanf, fscanf, sscanf, scanf_s, fscanf_s, sscanf_s

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
int scanf( const char *format, ... );  // até C99
int scanf( const char *restrict format, ... );  // desde C99
int fscanf( FILE *stream, const char *format, ... );  // até C99
int fscanf( FILE *restrict stream, const char *restrict format, ... );  // desde C99
int sscanf( const char *buffer, const char *format, ... );  // até C99
int sscanf( const char *restrict buffer, const char *restrict format, ... );  // desde C99
int scanf_s(const char *restrict format, ...);  // desde C11
int fscanf_s(FILE *restrict stream, const char *restrict format, ...);  // desde C11
int sscanf_s(const char *restrict buffer, const char *restrict format, ...);  // desde C11
```

  
Lê dados de uma variedade de fontes, interpreta-os de acordo com `format` e armazena os resultados nos locais fornecidos.

1) lê os dados de [stdin](<#/doc/io/std_streams>)

2) lê os dados do fluxo de arquivo `stream`

3) lê os dados da string de caracteres terminada em nulo `buffer`. Atingir o fim da string é equivalente a atingir a condição de fim de arquivo para `fscanf`

4-6) O mesmo que (1-3), exceto que os especificadores de conversão %c, %s e %[ esperam cada um dois argumentos (o ponteiro usual e um valor do tipo rsize_t indicando o tamanho do array de recebimento, que pode ser 1 ao ler com %c em um único char) e exceto que os seguintes erros são detectados em tempo de execução e chamam a função [constraint handler](<#/doc/error/set_constraint_handler_s>) atualmente instalada:

    

  * qualquer um dos argumentos do tipo ponteiro é um ponteiro nulo
  * `format`, `stream` ou `buffer` é um ponteiro nulo
  * o número de caracteres que seriam escritos por %c, %s ou %[, mais o caractere nulo de terminação, excederia o segundo argumento (`rsize_t`) fornecido para cada um desses especificadores de conversão
  * opcionalmente, qualquer outro erro detectável, como especificador de conversão desconhecido

    Assim como todas as funções com verificação de limites, `scanf_s`, `fscanf_s` e `sscanf_s` são garantidas de estarem disponíveis apenas se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir [`<stdio.h>`](<#/doc/io>).

### Parâmetros

stream  |  \-  |  fluxo de arquivo de entrada para ler   
buffer  |  \-  |  ponteiro para uma string de caracteres terminada em nulo para ler   
format  |  \-  |  ponteiro para uma string de caracteres terminada em nulo especificando como ler a entrada   
...  |  \-  |  argumentos de recebimento.   
  
  
A string de **formato** consiste em

  * caracteres multibyte não-espaço em branco, exceto %: cada um desses caracteres na string de formato consome exatamente um caractere idêntico do fluxo de entrada, ou faz com que a função falhe se o próximo caractere no fluxo não for igual.
  * caracteres de espaço em branco: qualquer caractere de espaço em branco único na string de formato consome todos os caracteres de espaço em branco consecutivos disponíveis da entrada (determinado como se chamando [`isspace`](<#/doc/string/byte/isspace>) em um loop). Note que não há diferença entre "\n", " ", "\t\t", ou outros espaços em branco na string de formato.
  * especificações de conversão. Cada especificação de conversão tem o seguinte formato:

    

  * caractere % introdutório.

    

  * (opcional) caractere * de supressão de atribuição. Se esta opção estiver presente, a função não atribui o resultado da conversão a nenhum argumento de recebimento.

    

  * (opcional) número inteiro (maior que zero) que especifica a _largura máxima do campo_, ou seja, o número máximo de caracteres que a função pode consumir ao fazer a conversão especificada pela especificação de conversão atual. Note que %s e %[ podem levar a estouro de buffer se a largura não for fornecida.

    

  * (opcional) _modificador de comprimento_ que especifica o tamanho do argumento de recebimento, ou seja, o tipo de destino real. Isso afeta a precisão da conversão e as regras de estouro. O tipo de destino padrão é diferente para cada tipo de conversão (veja a tabela abaixo).

    

  * especificador de formato de conversão.

Os seguintes especificadores de formato estão disponíveis:

Conversão  
especificador  | Explicação  | Tipo de argumento   
**Modificador de comprimento →** | `hh` (C99) | `h` | (nenhum)  | `l` | `ll` (C99) | `j` (C99) | `z` (C99) | `t` (C99) | `L`  
`%` | Corresponde ao literal `%`.  |  N/A |  N/A |  N/A |  N/A |  N/A |  N/A |  N/A |  N/A |  N/A  
`c` | 

    Corresponde a um **caractere** ou uma sequência de **caracteres**. 
Se um especificador de largura for usado, corresponde exatamente a _width_ caracteres (o argumento deve ser um ponteiro para um array com espaço suficiente). Ao contrário de %s e %[, não anexa o caractere nulo ao array.  |  N/A |  N/A | char* | wchar_t* |  N/A |  N/A |  N/A |  N/A |  N/A  
`s` | 

    Corresponde a uma sequência de caracteres não-espaço em branco (uma **string**). 
Se um especificador de largura for usado, corresponde até _width_ ou até o primeiro caractere de espaço em branco, o que ocorrer primeiro. Sempre armazena um caractere nulo além dos caracteres correspondidos (portanto, o array de argumento deve ter espaço para pelo menos _width+1_ caracteres)   
`[`set`]` | 

    Corresponde a uma sequência não vazia de caracteres de um conjunto de caracteres. 
Se o primeiro caractere do conjunto for `^`, então todos os caracteres que não estão no conjunto são correspondidos. Se o conjunto começar com `]` ou `^]`, então o caractere `]` também é incluído no conjunto. É definido pela implementação se o caractere `-` na posição não inicial no scanset pode indicar um intervalo, como em `[0-9]`. Se um especificador de largura for usado, corresponde apenas até _width_. Sempre armazena um caractere nulo além dos caracteres correspondidos (portanto, o array de argumento deve ter espaço para pelo menos _width+1_ caracteres)   
`d` | 

    Corresponde a um **inteiro decimal**. 
O formato do número é o mesmo esperado por [`strtol`](<#/doc/string/byte/strtol>) com o valor 10 para o argumento `base`  | signed char* ou unsigned char* | signed short* ou unsigned short* | signed int* ou unsigned int* | signed long* ou unsigned long* | signed long long* ou unsigned long long* | [intmax_t](<#/doc/types/integer>)* ou [uintmax_t](<#/doc/types/integer>)* | [size_t](<#/doc/types/size_t>)* | [ptrdiff_t](<#/doc/types/ptrdiff_t>)* |  N/A  
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
O formato do número é o mesmo esperado por [`strtof`](<#/doc/string/byte/strtof>) |  N/A |  N/A | float* | double* |  N/A |  N/A |  N/A |  N/A | long double*  
`p` | 

    Corresponde a uma sequência de caracteres definida pela implementação que define um **ponteiro**. 
A família de funções `printf` deve produzir a mesma sequência usando o especificador de formato `%p`  |  N/A |  N/A | void** |  N/A |  N/A |  N/A |  N/A |  N/A |  N/A  
  
Para cada especificador de conversão diferente de n, a sequência mais longa de caracteres de entrada que não excede nenhuma largura de campo especificada e que é exatamente o que o especificador de conversão espera ou é um prefixo de uma sequência que ele esperaria, é o que é consumido do fluxo. O primeiro caractere, se houver, após esta sequência consumida permanece não lido. Se a sequência consumida tiver comprimento zero ou se a sequência consumida não puder ser convertida conforme especificado acima, ocorre uma falha de correspondência, a menos que o fim do arquivo, um erro de codificação ou um erro de leitura tenha impedido a entrada do fluxo, caso em que é uma falha de entrada.

Todos os especificadores de conversão, exceto [, c e n, consomem e descartam todos os caracteres de espaço em branco iniciais (determinado como se chamando [`isspace`](<#/doc/string/byte/isspace>)) antes de tentar analisar a entrada. Esses caracteres consumidos não contam para a largura máxima de campo especificada.

Os especificadores de conversão lc, ls e l[ realizam a conversão de caracteres multibyte para wide como se chamassem [`mbrtowc`](<#/doc/string/multibyte/mbrtowc>) com um objeto [`mbstate_t`](<#/doc/string/multibyte/mbstate_t>) inicializado com zero antes que o primeiro caractere seja convertido.

Os especificadores de conversão s e [ sempre armazenam o terminador nulo além dos caracteres correspondidos. O tamanho do array de destino deve ser pelo menos um maior que a largura de campo especificada. O uso de %s ou %[, sem especificar o tamanho do array de destino, é tão inseguro quanto [gets](<#/doc/io/gets>).

As especificações de conversão corretas para os [tipos inteiros de largura fixa](<#/doc/types/integer>) ([int8_t](<#/doc/types/integer>), etc) são definidas no cabeçalho [`<inttypes.h>`](<#/doc/types/integer>) (embora [`SCNdMAX`](<#/doc/types/integer>), [`SCNuMAX`](<#/doc/types/integer>), etc sejam sinônimos de %jd, %ju, etc).

Existe um [ponto de sequência](<#/doc/language/eval_order>) após a ação de cada especificador de conversão; isso permite armazenar múltiplos campos na mesma variável "sumidouro".

Ao analisar um valor de ponto flutuante incompleto que termina no expoente sem dígitos, como analisar "100er" com o especificador de conversão %f, a sequência "100e" (o prefixo mais longo de um número de ponto flutuante possivelmente válido) é consumida, resultando em um erro de correspondência (a sequência consumida não pode ser convertida em um número de ponto flutuante), com "r" restante. Algumas implementações existentes não seguem esta regra e retrocedem para consumir apenas "100", deixando "er", por exemplo, [bug 1765 do glibc](<https://sourceware.org/bugzilla/show_bug.cgi?id=1765>).

Uma especificação de conversão deve ser válida. Caso contrário, o comportamento é indefinido.

Se uma especificação de conversão for inválida, o comportamento é indefinido.

### Valor de retorno

1-3) Número de argumentos de recebimento atribuídos com sucesso (que pode ser zero caso uma falha de correspondência tenha ocorrido antes que o primeiro argumento de recebimento fosse atribuído), ou [EOF](<#/doc/io>) se ocorrer uma falha de entrada antes que o primeiro argumento de recebimento fosse atribuído.

4-6) O mesmo que (1-3), exceto que [EOF](<#/doc/io>) também é retornado se houver uma violação de restrição em tempo de execução.

### Complexidade

Não garantida. Notavelmente, algumas implementações de `sscanf` são O(N), onde N = [strlen](<#/doc/string/byte/strlen>)(buffer) [1](<https://sourceware.org/bugzilla/show_bug.cgi?id=17577>).

### Notas

Como a maioria dos especificadores de conversão primeiro consome todos os espaços em branco consecutivos, código como
```c
    scanf("%d", &a);
    scanf("%d", &b);
```

lerá dois inteiros que são inseridos em linhas diferentes (o segundo %d consumirá a quebra de linha deixada pelo primeiro) ou na mesma linha, separados por espaços ou tabulações (o segundo %d consumirá os espaços ou tabulações).

Os especificadores de conversão que não consomem espaços em branco iniciais, como %c, podem ser feitos para fazê-lo usando um caractere de espaço em branco na string de formato:
```c
    scanf("%d", &a);
    scanf(" %c", &c); // consome todos os espaços em branco consecutivos após %d, então lê um char
```

### Exemplo

Execute este código
```c
    #define __STDC_WANT_LIB_EXT1__ 1
    #include <stdio.h>
    #include <stddef.h>
    #include <locale.h>
    
    int main(void)
    {
        int i, j;
        float x, y;
        char str1[10], str2[4];
        wchar_t warr[2];
        setlocale(LC_ALL, "en_US.utf8");
    
        char input[] = "25 54.32E-1 Thompson 56789 0123 56ß水";
        /* analisa da seguinte forma:
          %d: um inteiro
          %f: um valor de ponto flutuante
          %9s: uma string de no máximo 9 caracteres não-espaço em branco
          %2d: inteiro de dois dígitos (dígitos 5 e 6)
          %f:  um valor de ponto flutuante (dígitos 7, 8, 9)
          %*d: um inteiro que não é armazenado em lugar nenhum
           ' ': todos os espaços em branco consecutivos
          %3[0-9]: uma string de no máximo 3 dígitos decimais (dígitos 5 e 6)
          %2lc: dois caracteres wide, usando conversão multibyte para wide  */
        int ret = sscanf(input, "%d%f%9s%2d%f%*d %3[0-9]%2lc",
                         &i, &x, str1, &j, &y, str2, warr);
    
        printf("Campos convertidos %d:\n"
               "i = %d\n"
               "x = %f\n"
               "str1 = %s\n"
               "j = %d\n"
               "y = %f\n"
               "str2 = %s\n"
               "warr[0] = U+%x\n"
               "warr[1] = U+%x\n",
               ret, i, x, str1, j, y, str2, warr[0], warr[1]);
    
    #ifdef __STDC_LIB_EXT1__
        int n = sscanf_s(input, "%d%f%s", &i, &x, str1, (rsize_t)sizeof str1);
        // escreve 25 em i, 5.432 em x, os 9 bytes "Thompson\0" em str1, e 3 em n.
    #endif
    }
```

Saída possível:
```
    Converted 7 fields:
    i = 25
    x = 5.432000
    str1 = Thompson
    j = 56
    y = 789.000000
    str2 = 56
    warr[0] = U+df
    warr[1] = U+6c34
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.21.6.2 A função fscanf (p: 231-236)

    

  * 7.21.6.4 A função scanf (p: 236-237)

    

  * 7.21.6.7 A função sscanf (p: 238-239)

    

  * K.3.5.3.2 A função fscanf_s (p: 430-431)

    

  * K.3.5.3.4 A função scanf_s (p: 432)

    

  * K.3.5.3.7 A função sscanf_s (p: 433)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.21.6.2 A função fscanf (p: 317-324)

    

  * 7.21.6.4 A função scanf (p: 325)

    

  * 7.21.6.7 A função sscanf (p: 326)

    

  * K.3.5.3.2 A função fscanf_s (p: 592-593)

    

  * K.3.5.3.4 A função scanf_s (p: 594)

    

  * K.3.5.3.7 A função sscanf_s (p: 596)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.19.6.2 A função fscanf (p: 282-289)

    

  * 7.19.6.4 A função scanf (p: 290)

    

  * 7.19.6.7 A função sscanf (p: 291)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.9.6.2 A função fscanf

    

  * 4.9.6.4 A função scanf

    

  * 4.9.6.6 A função sscanf

### Veja também

[ vscanfvfscanfvsscanfvscanf_svfscanf_svsscanf_s](<#/doc/io/vfscanf>)(C99)(C99)(C99)(C11)(C11)(C11) |  lê entrada formatada de [stdin](<#/doc/io/std_streams>), um fluxo de arquivo ou um buffer usando lista de argumentos variáveis   
(função)  
[ fgets](<#/doc/io/fgets>) |  obtém uma string de caracteres de um fluxo de arquivo   
(função)  
[ printffprintfsprintfsnprintfprintf_sfprintf_ssprintf_ssnprintf_s](<#/doc/io/fprintf>)(C99)(C11)(C11)(C11)(C11) |  imprime saída formatada para [stdout](<#/doc/io/std_streams>), um fluxo de arquivo ou um buffer   
(função)  
[Documentação C++](<#/>) para scanf, fscanf, sscanf