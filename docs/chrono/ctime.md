# ctime, ctime_s

Definido no cabeçalho [`<time.h>`](<#/doc/chrono>)

```c
char* ctime( const time_t* timer );  // até C23
[[deprecated]] char* ctime( const time_t* timer );  // desde C23
errno_t ctime_s( char *buf, rsize_t bufsz, const time_t* timer );  // desde C11
```

1) Converte o tempo dado desde a época para um tempo local de calendário e então para uma representação textual, como se chamasse [asctime](<#/doc/chrono/asctime>)([localtime](<#/doc/chrono/localtime>)(timer)) ou [asctime](<#/doc/chrono/asctime>)(localtime_r(timer, &(struct [tm](<#/doc/chrono/tm>)){0}))(desde C23). Esta função está obsoleta e não deve ser usada em código novo.(desde C23)

2) O mesmo que (1), exceto que a função é equivalente a asctime_s(buf, bufsz, localtime_s(timer, &(struct [tm](<#/doc/chrono/tm>)){0})), e os seguintes erros são detectados em tempo de execução e chamam a função [manipulador de restrição](<#/doc/error/set_constraint_handler_s>) atualmente instalada:

  * `buf` ou `timer` é um ponteiro nulo
  * `bufsz` é menor que 26 ou maior que RSIZE_MAX

    Assim como todas as funções com verificação de limites, `ctime_s` só é garantida como disponível se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir [`<time.h>`](<#/doc/chrono>).

A string resultante tem o seguinte formato:
```
    Www Mmm dd hh:mm:ss yyyy\n
```

  * `Www` - o dia da semana (um de `Mon`, `Tue`, `Wed`, `Thu`, `Fri`, `Sat`, `Sun`).
  * `Mmm` - o mês (um de `Jan`, `Feb`, `Mar`, `Apr`, `May`, `Jun`, `Jul`, `Aug`, `Sep`, `Oct`, `Nov`, `Dec`).
  * `dd` - o dia do mês
  * `hh` - horas
  * `mm` - minutos
  * `ss` - segundos
  * `yyyy` - anos

A função não suporta localização.

### Parâmetros

- **timer** — ponteiro para um objeto [time_t](<#/doc/chrono/time_t>) especificando o tempo a ser impresso
- **buf** — ponteiro para o primeiro elemento de um array de char de tamanho mínimo `bufsz`
- **bufsz** — número máximo de bytes a serem gerados, tipicamente o tamanho do buffer apontado por `buf`

### Valor de retorno

1) ponteiro para uma string de caracteres estática terminada em nulo contendo a representação textual de data e hora. A string pode ser compartilhada entre [asctime](<#/doc/chrono/asctime>) e `ctime`, e pode ser sobrescrita a cada invocação de qualquer uma dessas funções.

2) zero em caso de sucesso (nesse caso, a representação da string de tempo foi escrita no array apontado por `buf`), ou diferente de zero em caso de falha (nesse caso, o caractere nulo de terminação é sempre escrito em buf[0], a menos que `buf` seja um ponteiro nulo ou `bufsz` seja zero ou maior que RSIZE_MAX.

### Notas

`ctime` retorna um ponteiro para dados estáticos e não é thread-safe. Além disso, ela modifica o objeto estático [tm](<#/doc/chrono/tm>) que pode ser compartilhado com [gmtime](<#/doc/chrono/gmtime>) e [localtime](<#/doc/chrono/localtime>). POSIX marca esta função como obsoleta e recomenda [strftime](<#/doc/chrono/strftime>) em seu lugar. O padrão C também recomenda [strftime](<#/doc/chrono/strftime>) em vez de `ctime` e `ctime_s` porque `strftime` é mais flexível e sensível à localidade.

O comportamento de `ctime` é indefinido para os valores de [time_t](<#/doc/chrono/time_t>) que resultam em uma string com mais de 25 caracteres (por exemplo, ano 10000).

### Exemplo

Execute este código
```c
    #define __STDC_WANT_LIB_EXT1__ 1
    #include <time.h>
    #include <stdio.h>
    
    int main(void)
    {
        time_t result = time(NULL);
        printf("%s", ctime(&result));
    
    #ifdef __STDC_LIB_EXT1__
        char str[26];
        ctime_s(str,sizeof str,&result);
        printf("%s", str);
    #endif
    }
```

Saída possível:
```
    Tue May 26 21:51:03 2015
    Tue May 26 21:51:03 2015
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.27.3.2 A função ctime (p: 287-288)

    

  * K.3.8.2.2 A função ctime_s (p: 454)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.27.3.2 A função ctime (p: 393)

    

  * K.3.8.2.2 A função ctime_s (p: 626)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.23.3.2 A função ctime (p: 342)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.12.3.2 A função ctime

### Veja também

[ asctimeasctime_s](<#/doc/chrono/asctime>)(obsoleta em C23)(C11) | converte um objeto [tm](<#/doc/chrono/tm>) para uma representação textual
(função)
[ strftime](<#/doc/chrono/strftime>) | converte um objeto [tm](<#/doc/chrono/tm>) para uma representação textual personalizada
(função)
[Documentação C++](<#/>) para ctime