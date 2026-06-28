# timespec

Definido no cabeçalho [`<time.h>`](<#/doc/chrono>)

```c
struct timespec;  // desde C11
```

Estrutura que armazena um intervalo dividido em segundos e nanossegundos.

### Membros

Membro | Descrição
[time_t](<#/doc/chrono/time_t>) `tv_sec` | segundos inteiros (valores válidos são >= ​0​)
/* veja abaixo */ `tv_nsec` | nanossegundos (valores válidos são `[`​0​`, `999999999`]`)
O tipo de `tv_nsec` é long. | (até C23)
O tipo de `tv_nsec` é um tipo inteiro assinado definido pela implementação que pode representar inteiros em `[`​0​`, `999999999`]`. | (desde C23)

A ordem de declaração de `tv_sec` e `tv_nsec` não é especificada. A implementação pode adicionar outros membros à struct timespec.

### Observações

O tipo de `tv_nsec` é long long em algumas plataformas, o que é conforme apenas desde C23.

### Exemplo

Execute este código
```c
    #include <stdint.h>
    #include <stdio.h>
    #include <time.h>
     
    int main(void)
    {
        struct timespec ts;
        timespec_get(&ts, TIME_UTC);
        char buff[100];
        strftime(buff, sizeof buff, "%D %T", gmtime(&ts.tv_sec));
        printf("Current time: %s.%09ld UTC\n", buff, ts.tv_nsec);
        printf("Raw timespec.tv_sec: %jd\n", (intmax_t)ts.tv_sec);
        printf("Raw timespec.tv_nsec: %09ld\n", ts.tv_nsec);
    }
```

Saída possível:
```
    Current time: 04/04/24 14:45:17.885909786 UTC
    Raw timespec.tv_sec: 1712241917
    Raw timespec.tv_nsec: 885909786
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.27.1/3 Componentes de tempo (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.27.1/3 Componentes de tempo (p: 284)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.27.1/3 Componentes de tempo (p: 388)

### Veja também

[ timespec_get](<#/doc/chrono/timespec_get>)(C11) | retorna o tempo de calendário em segundos e nanossegundos com base em uma dada base de tempo
(função)
[ tm](<#/doc/chrono/tm>) | tipo de tempo de calendário
(struct)
[Documentação C++](<#/>) para timespec