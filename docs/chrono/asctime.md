# asctime, asctime_s

Definido no cabeçalho [`<time.h>`](<#/doc/chrono>)

```c
char* asctime( const struct tm* time_ptr );  // até C23
[[deprecated]] char* asctime( const struct tm* time_ptr );  // desde C23
errno_t asctime_s( char* buf, rsize_t bufsz, const struct tm* time_ptr );  // desde C11
```

1) Converte o tempo de calendário [tm](<#/doc/chrono/tm>) fornecido para uma representação textual do seguinte formato fixo de 25 caracteres: Www Mmm dd hh:mm:ss yyyy\n

  * `Www` \- dia da semana abreviado em inglês com três letras de time_ptr->tm_wday, um de `Mon`, `Tue`, `Wed`, `Thu`, `Fri`, `Sat`, `Sun`.
  * `Mmm` \- nome do mês abreviado em inglês com três letras de time_ptr->tm_mon, um de `Jan`, `Feb`, `Mar`, `Apr`, `May`, `Jun`, `Jul`, `Aug`, `Sep`, `Oct`, `Nov`, `Dec`.
  * `dd` \- dia do mês com 2 dígitos de timeptr->tm_mday como se impresso por [sprintf](<#/doc/io/fprintf>) usando %2d.
  * `hh` \- hora com 2 dígitos de timeptr->tm_hour como se impresso por [sprintf](<#/doc/io/fprintf>) usando %.2d.
  * `mm` \- minuto com 2 dígitos de timeptr->tm_min como se impresso por [sprintf](<#/doc/io/fprintf>) usando %.2d.
  * `ss` \- segundo com 2 dígitos de timeptr->tm_sec como se impresso por [sprintf](<#/doc/io/fprintf>) usando %.2d.
  * `yyyy` \- ano com 4 dígitos de timeptr->tm_year + 1900 como se impresso por [sprintf](<#/doc/io/fprintf>) usando %4d.

O comportamento é indefinido se qualquer membro de *time_ptr estiver fora de seu intervalo normal.

O comportamento é indefinido se o ano de calendário indicado por time_ptr->tm_year tiver mais de 4 dígitos ou for menor que o ano 1000.

A função não suporta localização, e o caractere de nova linha não pode ser removido.

A função modifica armazenamento estático e não é thread-safe.

Esta função está obsoleta e não deve ser usada em código novo. | (desde C23)

2) O mesmo que (1), exceto que a mensagem é escrita no armazenamento buf fornecido pelo usuário, que é garantido ser terminado em nulo, e os seguintes erros são detectados em tempo de execução e chamam a função [constraint handler](<#/doc/error/set_constraint_handler_s>) atualmente instalada:

  * `buf` ou `time_ptr` é um ponteiro nulo
  * `bufsz` é menor que 26 ou maior que `RSIZE_MAX`
  * nem todos os membros de `*time_ptr` estão dentro de seus intervalos normais
  * o ano indicado por `time_ptr->tm_year` é menor que 0 ou maior que 9999.

Assim como todas as funções com verificação de limites, `asctime_s` é garantida estar disponível apenas se `__STDC_LIB_EXT1__` for definido pela implementação e se o usuário definir `__STDC_WANT_LIB_EXT1__` para a constante inteira 1 antes de incluir `[`<time.h>`](<#/doc/chrono>)`.

### Parâmetros

- **time_ptr** — ponteiro para um objeto [tm](<#/doc/chrono/tm>) especificando o tempo a ser impresso
- **buf** — ponteiro para um buffer fornecido pelo usuário com pelo menos 26 bytes de comprimento
- **bufsz** — tamanho do buffer fornecido pelo usuário

### Valor de retorno

1) ponteiro para uma string de caracteres estática terminada em nulo contendo a representação textual de data e hora conforme descrito acima. A string pode ser compartilhada entre `asctime` e [ctime](<#/doc/chrono/ctime>), e pode ser sobrescrita a cada invocação de qualquer uma dessas funções.

2) zero em caso de sucesso, diferente de zero em caso de falha, caso em que buf[0] é definido como zero (a menos que buf seja um ponteiro nulo ou bufsz seja zero ou maior que RSIZE_MAX).

### Notas

`asctime` retorna um ponteiro para dados estáticos e não é thread-safe. POSIX marca esta função como obsoleta e recomenda [strftime](<#/doc/chrono/strftime>) em seu lugar. O padrão C também recomenda [strftime](<#/doc/chrono/strftime>) em vez de `asctime` e `asctime_s` porque `strftime` é mais flexível e sensível à localidade.

POSIX limita comportamentos indefinidos apenas para quando a string de saída seria mais longa que 25 caracteres, quando timeptr->tm_wday ou timeptr->tm_mon não estão dentro dos intervalos esperados, ou quando timeptr->tm_year excede [INT_MAX](<#/doc/types/limits>) - 1990.

Algumas implementações tratam timeptr->tm_mday == 0 como significando o último dia do mês anterior.

### Exemplo

Execute este código
```c
    #define __STDC_WANT_LIB_EXT1__ 1
    #include <stdio.h>
    #include <time.h>
    
    int main(void)
    {
        struct tm tm = *localtime(&((time_t){time(NULL)}));
        printf("%s", asctime(&tm)); // note implicit trailing '\n'
    
    #ifdef __STDC_LIB_EXT1__
        char str[26];
        asctime_s(str, sizeof str, &tm);
        printf("%s", str);
    #endif
    }
```

Saída possível:
```
    Tue May 26 21:51:50 2015
    Tue May 26 21:51:50 2015
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    * 7.27.2.1 A função asctime (p: 287)

    * K.3.8.2.1 A função asctime_s (p: 453-454)

  * Padrão C11 (ISO/IEC 9899:2011):

    * 7.27.2.1 A função asctime (p: 392-393)

    * K.3.8.2.1 A função asctime_s (p: 624-625)

  * Padrão C99 (ISO/IEC 9899:1999):

    * 7.23.3.1 A função asctime (p: 341-342)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    * 4.12.3.1 A função asctime

### Veja também

[ ctimectime_s](<#/doc/chrono/ctime>)(obsoleto em C23)(C11) | converte um objeto [time_t](<#/doc/chrono/time_t>) para uma representação textual
(função)
[ strftime](<#/doc/chrono/strftime>) | converte um objeto [tm](<#/doc/chrono/tm>) para uma representação textual personalizada
(função)
[Documentação C++](<#/>) para asctime