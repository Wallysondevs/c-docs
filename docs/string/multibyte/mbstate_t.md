# mbstate_t

Definido no cabeçalho [`<uchar.h>`](<#/doc/string/multibyte>) | | (desde C11)

```c
Definido no cabeçalho ``<wchar.h>``
struct mbstate_t;  // desde C95
```

O tipo `mbstate_t` é um tipo trivial não-array que pode representar qualquer um dos estados de conversão que podem ocorrer em um conjunto de regras de codificação de caracteres multibyte suportadas e definidas pela implementação. Um valor de `mbstate_t` inicializado com zero representa o estado de conversão inicial, embora outros valores de `mbstate_t` possam existir que também representem o estado de conversão inicial.

Uma possível implementação de `mbstate_t` é um tipo `struct` que contém um array representando o caractere multibyte incompleto, um contador inteiro indicando o número de bytes no array que foram processados, e uma representação do estado de deslocamento atual.

As seguintes funções não devem ser chamadas de múltiplas threads sem sincronização com o argumento `mbstate_t*` de um ponteiro nulo devido a possíveis condições de corrida de dados: [mbrlen](<#/doc/string/multibyte/mbrlen>), [mbrtowc](<#/doc/string/multibyte/mbrtowc>), [mbsrtowcs](<#/doc/string/multibyte/mbsrtowcs>), [mbtowc](<#/doc/string/multibyte/mbtowc>), [wcrtomb](<#/doc/string/multibyte/wcrtomb>), [wcsrtombs](<#/doc/string/multibyte/wcsrtombs>), [wctomb](<#/doc/string/multibyte/wctomb>).

### Referências

* Padrão C11 (ISO/IEC 9899:2011):

  * 7.29.1/2 Introdução (p: 402)

* Padrão C99 (ISO/IEC 9899:1999):

  * 7.24.1/2 Introdução (p: 348)

### Veja também

[ mbsinit](<#/doc/string/multibyte/mbsinit>)(C95) | verifica se o objeto mbstate_t representa o estado de deslocamento inicial
(função)
[Documentação C++](<#/>) para mbstate_t