# srand

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
void srand( unsigned seed );
```

Inicializa o gerador de números pseudoaleatórios usado por [rand()](<#/doc/numeric/random/rand>) com o valor `seed`.

Se `rand()` for usado antes de qualquer chamada a `srand()`, `rand()` se comporta como se tivesse sido inicializado com srand(1).

Cada vez que `rand()` é inicializado com a mesma `seed`, ele deve produzir a mesma sequência de valores.

`srand()` não tem garantia de ser thread-safe.

### Parâmetros

- **seed** — o valor da semente

### Valor de retorno

(nenhum)

### Notas

De modo geral, o gerador de números pseudoaleatórios deve ser inicializado apenas uma vez, antes de qualquer chamada a `rand()`, e no início do programa. Ele não deve ser inicializado repetidamente, ou reinicializado toda vez que você desejar gerar um novo lote de números pseudoaleatórios.

A prática padrão é usar o resultado de uma chamada a [time](<#/doc/chrono/time>)(0) como semente. No entanto, `time()` retorna um valor [time_t](<#/doc/chrono/time_t>), e `time_t` não tem garantia de ser um tipo integral. Na prática, porém, toda implementação principal define `time_t` como um tipo integral, e isso também é o que o POSIX exige.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
    #include <time.h>
    
    int main(void)
    {
        srand(time(NULL)); //usa o tempo atual como semente para o gerador aleatório
        int random_variable = rand();
        printf("Random value on [0,%d]: %d\n", RAND_MAX, random_variable);
    }
```

Saída possível:
```
    Random value on [0 2147483647]: 1373858591
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.22.2.2 A função srand (p: 252-253)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.22.2.2 A função srand (p: 346-347)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.20.2.2 A função srand (p: 312-313)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.10.2.2 A função srand

### Veja também

[ rand](<#/doc/numeric/random/rand>) | gera um número pseudoaleatório
(função)
[ RAND_MAX](<#/doc/numeric/random/RAND_MAX>) | valor máximo possível gerado por [rand](<#/doc/numeric/random/rand>)()
(macro constante)
[Documentação C++](<#/>) para srand