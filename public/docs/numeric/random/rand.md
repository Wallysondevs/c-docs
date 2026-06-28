# rand

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
int rand();
```

Retorna um valor inteiro pseudoaleatório entre 0 e [RAND_MAX](<#/doc/numeric/random/RAND_MAX>) (0 e `RAND_MAX` incluídos).

[srand()](<#/doc/numeric/random/srand>) inicializa o gerador de números pseudoaleatórios usado por `rand()`. Se `rand()` for usado antes de qualquer chamada a `srand()`, `rand()` se comporta como se tivesse sido inicializado com [srand](<#/doc/numeric/random/srand>)(1). Cada vez que `rand()` é inicializado com `srand()`, ele deve produzir a mesma sequência de valores.

`rand()` não tem garantia de ser thread-safe.

### Parâmetros

(nenhum)

### Valor de retorno

Valor inteiro pseudoaleatório entre 0 e [RAND_MAX](<#/doc/numeric/random/RAND_MAX>), inclusive.

### Notas

Não há garantias quanto à qualidade da sequência aleatória produzida. No passado, algumas implementações de `rand()` apresentaram sérias deficiências na aleatoriedade, distribuição e período da sequência produzida (em um exemplo bem conhecido, o bit de baixa ordem simplesmente alternava entre `1` e `0` entre as chamadas). `rand()` não é recomendado para necessidades sérias de geração de números aleatórios, como criptografia.

POSIX exige que o período do gerador de números pseudoaleatórios usado por `rand` seja de pelo menos 232.

POSIX ofereceu uma versão thread-safe de rand chamada `rand_r`, que está obsoleta em favor da família de funções [`drand48`](<http://pubs.opengroup.org/onlinepubs/9699919799/functions/drand48.html>).

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
    #include <time.h>
    
    int main(void)
    {
        srand(time(NULL)); // use current time as seed for random generator
        int random_variable = rand();
        printf("Random value on [0,%d]: %d\n", RAND_MAX, random_variable);
    
        // roll a 6-sided die 20 times
        for (int n=0; n != 20; ++n) {
            int x = 7;
            while(x > 6) 
                x = 1 + rand()/((RAND_MAX + 1u)/6); // Note: 1+rand()%6 is biased
            printf("%d ",  x); 
        }
    }
```

Saída possível:
```
    Random value on [0,2147483647]: 448749574
    3 1 3 1 4 2 2 1 3 6 4 4 3 1 6 2 3 2 6 1
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.22.2.1 A função rand (p: 252)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.22.2.1 A função rand (p: 346)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.20.2.1 A função rand (p: 312)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.10.2.1 A função rand

### Veja também

[ srand](<#/doc/numeric/random/srand>) | inicializa o gerador de números pseudoaleatórios
(função)
[ RAND_MAX](<#/doc/numeric/random/RAND_MAX>) | valor máximo possível gerado por rand()
(macro constante)
[Documentação C++](<#/>) para rand