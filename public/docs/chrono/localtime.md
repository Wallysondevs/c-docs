# localtime, localtime_r, localtime_s

Definido no cabeçalho [`<time.h>`](<#/doc/chrono>)

```c
struct tm* localtime ( const time_t* timer );
struct tm* localtime_r( const time_t* timer, struct tm* buf );  // desde C23
struct tm* localtime_s( const time_t* restrict timer, struct tm* restrict buf );  // desde C11
```

1) Converte o tempo dado desde a época (um valor [time_t](<#/doc/chrono/time_t>) apontado por timer) em tempo de calendário, expresso em tempo local, no formato [`struct tm`](<#/doc/chrono/tm>). O resultado é armazenado em memória estática e um ponteiro para essa memória estática é retornado.

2) O mesmo que (1), exceto que a função usa o armazenamento buf fornecido pelo usuário para o resultado.

3) O mesmo que (1), exceto que a função usa o armazenamento buf fornecido pelo usuário para o resultado e que os seguintes erros são detectados em tempo de execução e chamam a função [manipulador de restrição](<#/doc/error/set_constraint_handler_s>) atualmente instalada:

* timer ou buf é um ponteiro nulo

Assim como todas as funções com verificação de limites, `localtime_s` tem sua disponibilidade garantida apenas se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir [`<time.h>`](<#/doc/chrono>).

### Parâmetros

- **timer** — ponteiro para um objeto [time_t](<#/doc/chrono/time_t>) a ser convertido
- **buf** — ponteiro para um objeto struct [tm](<#/doc/chrono/tm>) para armazenar o resultado

### Valor de retorno

1) ponteiro para um objeto [tm](<#/doc/chrono/tm>) estático interno em caso de sucesso, ou ponteiro nulo caso contrário. A estrutura pode ser compartilhada entre [gmtime](<#/doc/chrono/gmtime>), `localtime` e [ctime](<#/doc/chrono/ctime>) e pode ser sobrescrita a cada invocação.

2,3) cópia do ponteiro buf, ou ponteiro nulo em caso de erro (o que pode ser uma violação de restrição em tempo de execução ou uma falha ao converter o tempo especificado para tempo de calendário local).

### Observações

A função `localtime` pode não ser thread-safe.

POSIX exige que `localtime` e `localtime_r` definam [errno](<#/doc/error/errno>) para [EOVERFLOW](<#/doc/error/errno_macros>) se falhar porque o argumento é muito grande.

[POSIX especifica](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/localtime.html>) que as informações de fuso horário são determinadas por `localtime` e `localtime_r` como se chamando [`tzset`](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/tzset.html>), que lê a variável de ambiente TZ.

A implementação de `localtime_s` no [Microsoft CRT](<https://docs.microsoft.com/en-us/cpp/c-runtime-library/reference/localtime-s-localtime32-s-localtime64-s?view=vs-2019>) é incompatível com o padrão C, pois possui a ordem dos parâmetros invertida e retorna errno_t.

### Exemplo

Execute este código
```c
    #define __STDC_WANT_LIB_EXT1__ 1
    #define _XOPEN_SOURCE // for putenv
    #include <stdio.h>
    #include <stdlib.h>   // for putenv
    #include <time.h>
    
    int main(void)
    {
        time_t t = time(NULL);
        printf("UTC:      %s", asctime(gmtime(&t)));
        printf("local:    %s", asctime(localtime(&t)));
        // POSIX-specific
        putenv("TZ=Asia/Singapore");
        printf("Singapore: %s", asctime(localtime(&t)));
    
    #ifdef __STDC_LIB_EXT1__
        struct tm buf;
        char str[26];
        asctime_s(str, sizeof str, gmtime_s(&t, &buf));
        printf("UTC:      %s", str);
        asctime_s(str, sizeof str, localtime_s(&t, &buf));
        printf("local:    %s", str);
    #endif
    }
```

Saída possível:
```
    UTC:       Fri Sep 15 14:22:05 2017
    local:     Fri Sep 15 14:22:05 2017
    Singapore: Fri Sep 15 22:22:05 2017
    UTC:       Fri Sep 15 14:22:05 2017
    local:     Fri Sep 15 14:22:05 2017
```

### Referências

* Padrão C23 (ISO/IEC 9899:2024):

  * 7.27.3.4 A função localtime (p: TBD)

  * K.3.8.2.4 A função localtime_s (p: TBD)

* Padrão C17 (ISO/IEC 9899:2018):

  * 7.27.3.4 A função localtime (p: 288)

  * K.3.8.2.4 A função localtime_s (p: 455)

* Padrão C11 (ISO/IEC 9899:2011):

  * 7.27.3.4 A função localtime (p: 394)

  * K.3.8.2.4 A função localtime_s (p: 627)

* Padrão C99 (ISO/IEC 9899:1999):

  * 7.23.3.4 A função localtime (p: 343)

* Padrão C89/C90 (ISO/IEC 9899:1990):

  * 4.12.3.4 A função localtime

### Veja também

[ gmtimegmtime_rgmtime_s](<#/doc/chrono/gmtime>)(C23)(C11) | converte o tempo desde a época para tempo de calendário expresso como Tempo Universal Coordenado (UTC)
(função)
[Documentação C++](<#/>) para localtime