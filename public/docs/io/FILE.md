# FILE

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
typedef /* unspecified */ FILE;
```

Cada objeto `FILE` denota um fluxo C.

O padrão C não especifica se `FILE` é um tipo de objeto completo. Embora possa ser possível copiar um `FILE` válido, usar um ponteiro para tal cópia como argumento para uma função de E/S invoca comportamento não especificado. Em outras palavras, `FILE` pode ser semanticamente não copiável.

Fluxos de E/S podem ser usados tanto para entrada e saída não formatadas quanto formatadas. Além disso, as funções que lidam com entrada e saída também podem ser sensíveis à localidade (locale-sensitive), de modo que conversões wide/multibyte são realizadas conforme necessário.

### Estado do Fluxo

Além das informações específicas do sistema necessárias para acessar o dispositivo (_e.g.,_ um descritor de arquivo POSIX), cada objeto `FILE` direta ou indiretamente contém o seguinte:

1.  (C95) Largura do caractere: não definida, estreita (narrow) ou larga (wide).
2.  (C95) Estado de análise para conversões entre caracteres multibyte e wide (um objeto do tipo [mbstate_t](<#/doc/string/multibyte/mbstate_t>))
3.  Estado de bufferização: sem buffer (unbuffered), bufferizado por linha (line-buffered), totalmente bufferizado (fully buffered).
4.  O buffer, que pode ser substituído por um buffer externo fornecido pelo usuário.
5.  Modo de E/S: entrada, saída ou atualização (ambos entrada e saída).
6.  Indicador de modo binário/texto.
7.  Indicador de status de fim de arquivo.
8.  Indicador de status de erro.
9.  Indicador de posição do arquivo, acessível como um objeto do tipo [fpos_t](<#/doc/io/fpos_t>), que, para fluxos wide, inclui o estado de análise.
10. (C11) Trava reentrante usada para prevenir condições de corrida (data races) quando múltiplas threads leem, escrevem, posicionam ou consultam a posição de um fluxo.

#### Orientação estreita (narrow) e larga (wide)

Um fluxo recém-aberto não possui orientação. A primeira chamada para fwide ou para qualquer função de E/S estabelece a orientação: uma função de E/S wide torna o fluxo wide-oriented; uma função de E/S narrow torna o fluxo narrow-oriented. Uma vez definida, a orientação pode ser alterada apenas com [freopen](<#/doc/io/freopen>). Funções de E/S narrow não podem ser chamadas em um fluxo wide-oriented; funções de E/S wide não podem ser chamadas em um fluxo narrow-oriented. Funções de E/S wide convertem entre caracteres wide e multibyte como se chamassem [mbrtowc](<#/doc/string/multibyte/mbrtowc>) ou [wcrtomb](<#/doc/string/multibyte/wcrtomb>) com o estado de conversão conforme descrito pelo fluxo. Ao contrário das strings de caracteres multibyte que são válidas em um programa, sequências de caracteres multibyte no arquivo podem conter nulos embutidos e não precisam começar ou terminar no estado de mudança inicial (initial shift state).

O estado de conversão de um fluxo com orientação wide é estabelecido pela localidade C (C locale) que está instalada no momento em que a orientação do fluxo é definida.

#### Modos binário e texto

Um _fluxo de texto_ é uma sequência ordenada de caracteres que pode ser composta em linhas; uma linha pode ser decomposta em zero ou mais caracteres mais um caractere '\n' ("nova linha") terminador. Se a última linha requer um '\n' terminador é definido pela implementação. Além disso, caracteres podem ter que ser adicionados, alterados ou excluídos na entrada e saída para se conformar às convenções de representação de texto no SO (em particular, fluxos C no SO Windows convertem '\n' para '\r\n' na saída, e convertem '\r\n' para '\n' na entrada).

Dados lidos de um fluxo de texto são garantidos a serem comparáveis aos dados que foram anteriormente escritos para esse fluxo somente se cada um dos seguintes for verdadeiro:

*   Os dados consistem apenas em caracteres imprimíveis e/ou os caracteres de controle '\t' e '\n' (em particular, no SO Windows, o caractere '\0x1A' termina a entrada).
*   Nenhum caractere '\n' é imediatamente precedido por caracteres de espaço (tais caracteres de espaço podem desaparecer quando tal saída é lida posteriormente como entrada).
*   O último caractere é '\n'.

Um _fluxo binário_ é uma sequência ordenada de caracteres que pode registrar dados internos de forma transparente. Dados lidos de um fluxo binário sempre são iguais aos dados que foram anteriormente escritos para esse fluxo, exceto que uma implementação pode anexar um número indeterminado de caracteres nulos ao final do fluxo. Um fluxo binário wide não precisa terminar no estado de mudança inicial.

### Notas

POSIX exige explicitamente que a faceta `LC_CTYPE` da localidade C (C locale) atualmente instalada seja armazenada dentro do objeto `FILE` no momento em que a orientação do fluxo se torna wide; POSIX exige que esta faceta `LC_CTYPE` seja usada para toda E/S futura neste fluxo até que a orientação seja alterada, independentemente de qualquer chamada subsequente para [setlocale](<#/doc/locale/setlocale>).

Pretende-se que cada linha de texto seja composta por dados que são essencialmente legíveis por humanos. Implementações POSIX não distinguem entre fluxos de texto e binários (não há mapeamento especial para '\n' ou quaisquer outros caracteres).

### Referências

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.21 Entrada/saída <stdio.h> (p: 217-247)

    *   7.29 Utilitários estendidos de caracteres multibyte e wide <wchar.h> (p: 295-325)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.21 Entrada/saída <stdio.h> (p: 296-339)

    *   7.29 Utilitários estendidos de caracteres multibyte e wide <wchar.h> (p: 402-446)

*   Padrão C99 (ISO/IEC 9899:1999):

    *   7.19 Entrada/saída <stdio.h> (p: 262-305)

    *   7.24 Utilitários estendidos de caracteres multibyte e wide <wchar.h> (p: 348-392)

*   Padrão C89/C90 (ISO/IEC 9899:1990):

    *   4.9 ENTRADA/SAÍDA <stdio.h>

### Veja também

[ stdinstdoutstderr](<#/doc/io/std_streams>) | expressão do tipo FILE* associada ao fluxo de entrada
expressão do tipo FILE* associada ao fluxo de saída
expressão do tipo FILE* associada ao fluxo de saída de erro
(constante de macro)
[documentação C++](<#/>) para FILE