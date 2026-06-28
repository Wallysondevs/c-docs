# calloc

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
void* calloc( size_t num, size_t size );
```

Aloca memória para um array de `num` objetos de `size` e inicializa todos os bytes no armazenamento alocado com zero.

Se a alocação for bem-sucedida, retorna um ponteiro para o byte mais baixo (primeiro) no bloco de memória alocado que está adequadamente alinhado para qualquer tipo de objeto com [alinhamento fundamental](<#/doc/language/object>).

Se `size` for zero, o comportamento é definido pela implementação (um ponteiro nulo pode ser retornado, ou um ponteiro não nulo pode ser retornado que não pode ser usado para acessar o armazenamento).

`calloc` é thread-safe: ele se comporta como se acessasse apenas os locais de memória visíveis através de seu argumento, e não qualquer armazenamento estático. Uma chamada anterior a [free](<#/doc/memory/free>), free_sized, e free_aligned_sized(desde C23) ou [realloc](<#/doc/memory/realloc>) que desaloca uma região de memória _sincroniza-se com_ uma chamada a `calloc` que aloca a mesma ou parte da mesma região de memória. Essa sincronização ocorre após qualquer acesso à memória pela função de desalocação e antes de qualquer acesso à memória por `calloc`. Existe uma única ordem total de todas as funções de alocação e desalocação operando em cada região de memória particular. | (desde C11)

### Parâmetros

- **num** — número de objetos
- **size** — tamanho de cada objeto

### Valor de retorno

Em caso de sucesso, retorna o ponteiro para o início da memória recém-alocada. Para evitar um vazamento de memória, o ponteiro retornado deve ser desalocado com [free()](<#/doc/memory/free>) ou [realloc()](<#/doc/memory/realloc>).

Em caso de falha, retorna um ponteiro nulo.

### Notas

Devido aos requisitos de alinhamento, o número de bytes alocados não é necessariamente igual a `num * size`.

A inicialização para todos os bits zero não garante que um ponto flutuante ou um ponteiro seriam inicializados para 0.0 e o valor de ponteiro nulo, respectivamente (embora isso seja verdade em todas as plataformas comuns).

Originalmente (em C89), o suporte para tamanho zero foi adicionado para acomodar código como
```c
    OBJ* p = calloc(0, sizeof(OBJ)); // "zero-length" placeholder
    ...
    while(1)
    {
        p = realloc(p, c * sizeof(OBJ)); // reallocations until size settles
        ... // code that may change c or break out of loop
    }
```

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(void)
    {
        int* p1 = calloc(4, sizeof(int));    // aloca e zera um array de 4 inteiros
        int* p2 = calloc(1, sizeof(int[4])); // o mesmo, nomeando o tipo do array diretamente
        int* p3 = calloc(4, sizeof *p3);     // o mesmo, sem repetir o nome do tipo
    
        if (p2)
        {
            for (int n = 0; n < 4; ++n) // imprime o array
                printf("p2[%d] == %d\n", n, p2[n]);
        }
    
        free(p1);
        free(p2);
        free(p3);
    }
```

Saída:
```
    p2[0] == 0
    p2[1] == 0
    p2[2] == 0
    p2[3] == 0
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.22.3.2 A função calloc (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.22.3.2 A função calloc (p: 253)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.22.3.2 A função calloc (p: 348)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.20.3.1 A função calloc (p: 313)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.10.3.1 A função calloc

### Veja também

[Documentação C++](<#/>) para calloc
---