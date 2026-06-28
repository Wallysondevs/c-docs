# CLOCKS_PER_SEC

Definido no cabeçalho [`<time.h>`](<#/doc/chrono>)

```c
#define CLOCKS_PER_SEC /* implementation-defined */
```

Expande para uma expressão (não necessariamente uma constante em tempo de compilação) do tipo [clock_t](<#/doc/chrono/clock_t>) igual ao número de tiques de clock por segundo, conforme retornado por [clock()](<#/doc/chrono/clock>).

### Notas

POSIX define [`CLOCKS_PER_SEC`](<https://pubs.opengroup.org/onlinepubs/9799919799/basedefs/time.h.html>) como 1'000'000, independentemente da precisão real de [clock](<#/doc/chrono/clock>).

Até ser padronizado como CLOCKS_PER_SEC em C89, esta macro era por vezes conhecida pelo seu nome IEEE std 1003.1-1988 CLK_TCK: esse nome não foi incluído em C89 e foi removido do próprio POSIX em 1996 devido à ambiguidade com _SC_CLK_TCK, que fornece o número de clocks por segundo para a função [`times`](<https://pubs.opengroup.org/onlinepubs/9799919799/functions/times.html>)).

### Referências

*   Padrão C23 (ISO/IEC 9899:2024):

    *   7.27.1/2 Componentes de tempo (p: TBD)

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.27.1/2 Componentes de tempo (p: 284)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.27.1/2 Componentes de tempo (p: 388)

*   Padrão C99 (ISO/IEC 9899:1999):

    *   7.23.1/2 Componentes de tempo (p: 338)

*   Padrão C89/C90 (ISO/IEC 9899:1990):

    *   4.12.1 Componentes de tempo

### Veja também

[ clock](<#/doc/chrono/clock>) | retorna o tempo de clock bruto do processador desde o início do programa
(função)
[ clock_t](<#/doc/chrono/clock_t>) | tipo para tempo de processador desde uma era
(typedef)
[documentação C++](<#/>) para CLOCKS_PER_SEC