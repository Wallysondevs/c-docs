# thrd_sleep

Definido no cabeçalho [`<threads.h>`](<#/doc/thread>)

```c
int thrd_sleep( const struct timespec* duration,
struct timespec* remaining );  // desde C11
```

Bloqueia a execução da thread atual por _pelo menos_ até que a duração baseada em TIME_UTC apontada por `duration` tenha decorrido.

O sono pode ser retomado mais cedo se um [sinal](<#/doc/program/signal>) que não é ignorado for recebido. Nesse caso, se `remaining` não for [NULL](<#/doc/types/NULL>), a duração de tempo restante é armazenada no objeto apontado por `remaining`.

### Parâmetros

- **duration** — ponteiro para a duração do sono
- **remaining** — ponteiro para o objeto onde colocar o tempo restante em caso de interrupção. Pode ser [NULL](<#/doc/types/NULL>), caso em que é ignorado

### Valor de retorno

`0` em caso de sono bem-sucedido, -1 se um sinal ocorreu, outro valor negativo se um erro ocorreu.

### Notas

`duration` e `remaining` podem apontar para o mesmo objeto, o que simplifica a reexecução da função após um sinal.

O tempo de sono real pode ser maior do que o solicitado porque é arredondado para a granularidade do temporizador e devido à sobrecarga de escalonamento e troca de contexto.

O equivalente POSIX desta função é [`nanosleep`](<http://pubs.opengroup.org/onlinepubs/9699919799/functions/nanosleep.html>).

### Exemplo

Execute este código
```
    #include <threads.h>
    #include <time.h>
    #include <stdio.h>
    
    int main(void)
    {
        printf("Time: %s", ctime(&(time_t){time(NULL)}));
        thrd_sleep(&(struct timespec){.tv_sec=1}, NULL); // sleep 1 sec
        printf("Time: %s", ctime(&(time_t){time(NULL)}));
    }
```

Saída:
```
    Time: Mon Feb  2 16:18:41 2015
    Time: Mon Feb  2 16:18:42 2015
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.26.5.7 A função thrd_sleep (p: 281)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.26.5.7 A função thrd_sleep (p: 385)

### Veja também

[ thrd_yield](<#/doc/thread/thrd_yield>)(C11) | cede a fatia de tempo atual
(função)
[Documentação C++](<#/>) para sleep_for