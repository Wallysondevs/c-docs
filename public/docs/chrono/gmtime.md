# gmtime, gmtime_r, gmtime_s

Definido no cabeçalho [`<time.h>`](<#/doc/chrono>)

```c
struct tm* gmtime ( const time_t* timer );
struct tm* gmtime_r( const time_t* timer, struct tm* buf );  // desde C23
struct tm* gmtime_s( const time_t* restrict timer, struct tm* restrict buf );  // desde C11
```

1) Converte o tempo dado desde a época (um valor [time_t](<#/doc/chrono/time_t>) apontado por timer) em tempo de calendário, expresso em Tempo Universal Coordenado (UTC) no formato [`struct tm`](<#/doc/chrono/tm>). O resultado é armazenado em armazenamento estático e um ponteiro para esse armazenamento estático é retornado.

2) O mesmo que (1), exceto que a função usa o armazenamento buf fornecido pelo usuário para o resultado.

3) O mesmo que (1), exceto que a função usa o armazenamento buf fornecido pelo usuário para o resultado e que os seguintes erros são detectados em tempo de execução e chamam a função [constraint handler](<#/doc/error/set_constraint_handler_s>) atualmente instalada:

  * timer ou buf é um ponteiro nulo

Assim como todas as funções com verificação de limites, `gmtime_s` tem sua disponibilidade garantida apenas se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir [`<time.h>`](<#/>).

### Parâmetros

- **timer** — ponteiro para um objeto [time_t](<#/doc/chrono/time_t>) a ser convertido
- **buf** — ponteiro para um objeto struct [tm](<#/doc/chrono/tm>) para armazenar o resultado

### Valor de retorno

1) ponteiro para um objeto [tm](<#/doc/chrono/tm>) interno estático em caso de sucesso, ou ponteiro nulo caso contrário. A estrutura pode ser compartilhada entre `gmtime`, [localtime](<#/doc/chrono/localtime>) e [ctime](<#/doc/chrono/ctime>) e pode ser sobrescrita a cada invocação.

2,3) cópia do ponteiro buf, ou ponteiro nulo em caso de erro (o que pode ser uma violação de restrição em tempo de execução ou uma falha ao converter o tempo especificado para UTC).

### Observações

`gmtime` pode não ser seguro para threads.

POSIX exige que `gmtime` e `gmtime_r` definam [errno](<#/doc/error/errno>) para [EOVERFLOW](<#/doc/error/errno_macros>) se falharem porque o argumento é muito grande.

A implementação de `gmtime_s` no [Microsoft CRT](<https://docs.microsoft.com/en-us/cpp/c-runtime-library/reference/gmtime-s-gmtime32-s-gmtime64-s?view=vs-2019>) é incompatível com o padrão C, pois possui a ordem dos parâmetros invertida.

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
        printf("UTC:       %s", asctime(gmtime(&t)));
        printf("local:     %s", asctime(localtime(&t)));
        // POSIX-specific
        putenv("TZ=Asia/Singapore");
        printf("Singapore: %s", asctime(localtime(&t)));
    
    #ifdef __STDC_LIB_EXT1__
        struct tm buf;
        char str[26];
        asctime_s(str, sizeof str, gmtime_s(&t, &buf));
        printf("UTC:       %s", str);
        asctime_s(str, sizeof str, localtime_s(&t, &buf));
        printf("local:     %s", str);
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

    * 7.27.3.3 A função gmtime (p: TBD)

    * K.3.8.2.3 A função gmtime_s (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    * 7.27.3.3 A função gmtime (p: 288)

    * K.3.8.2.3 A função gmtime_s (p: 454-455)

  * Padrão C11 (ISO/IEC 9899:2011):

    * 7.27.3.3 A função gmtime (p: 393-394)

    * K.3.8.2.3 A função gmtime_s (p: 626-627)

  * Padrão C99 (ISO/IEC 9899:1999):

    * 7.23.3.3 A função gmtime (p: 343)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    * 4.12.3.3 A função gmtime

### Veja também

[ localtimelocaltime_rlocaltime_s](<#/doc/chrono/localtime>)(C23)(C11) | converte o tempo desde a época para tempo de calendário expresso como tempo local
(função)
[Documentação C++](<#/>) para gmtime