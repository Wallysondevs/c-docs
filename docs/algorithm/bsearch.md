# bsearch, bsearch_s

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
void* bsearch( const void *key, const void *ptr, size_t count, size_t size,
int (*comp)(const void*, const void*) );
void* bsearch_s( const void *key, const void *ptr, rsize_t count, rsize_t size,
int (*comp)(const void *, const void *, void *),
void *context );  // desde C11
/*QVoid*/* bsearch( const void *key, /*QVoid*/ *ptr, size_t count, size_t size,
int (*comp)(const void*, const void*) );  // desde C23
/*QVoid*/* bsearch_s( const void *key, /*QVoid*/ *ptr, rsize_t count, rsize_t size,
int (*comp)(const void *, const void *, void *),
void *context );  // desde C23
```

1) Encontra um elemento igual ao elemento apontado por `key` em um array apontado por `ptr`. O array contém `count` elementos de `size` bytes e deve ser particionado em relação a `key`, ou seja, todos os elementos que comparam como menores devem aparecer antes de todos os elementos que comparam como iguais, e estes devem aparecer antes de todos os elementos que comparam como maiores que o objeto `key`. Um array totalmente ordenado satisfaz esses requisitos. Os elementos são comparados usando a função apontada por `comp`. O comportamento é indefinido se o array não estiver já particionado em relação a `*key` em ordem crescente de acordo com o mesmo critério que `comp` usa.

2) O mesmo que (1), exceto que o argumento de estado adicional `context` é passado para `comp` e que os seguintes erros são detectados em tempo de execução e chamam a função [manipulador de restrição](<#/doc/error/set_constraint_handler_s>) atualmente instalada:

    * `count` ou `size` é maior que RSIZE_MAX
    * `key`, `ptr` ou `comp` é um ponteiro nulo (a menos que `count` seja zero)

    Assim como todas as funções com verificação de limites, `bsearch_s` (e a macro genérica de tipo correspondente)(desde C23) tem sua disponibilidade garantida apenas se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir [`<stdlib.h>`](<#/doc/program>).

3,4) Macros genéricas de tipo equivalentes a (1) e (2) respectivamente. Seja `T` um tipo de objeto não qualificado (incluindo void).

    * Se `ptr` for do tipo const T*, o tipo de retorno é const void*.
    * Caso contrário, se `ptr` for do tipo T*, o tipo de retorno é void*.
    * Caso contrário, o comportamento é indefinido.

Se uma definição de macro de cada uma dessas funções genéricas for suprimida para acessar uma função real (por exemplo, se (bsearch), (bsearch_s), ou um ponteiro de função for usado), a declaração de função real (1) ou (2) se torna visível.

Se o array contiver vários elementos que `comp` indicaria como iguais ao elemento procurado, então é não especificado qual elemento a função retornará como resultado.

Usos diretos das funções reais (1) e (2) são descontinuados. | (desde C23)

### Parâmetros

- **key** — ponteiro para o elemento a ser procurado
- **ptr** — ponteiro para o array a ser examinado
- **count** — número de elementos no array
- **size** — tamanho de cada elemento no array em bytes
- **comp** — função de comparação que retorna um valor inteiro negativo se o primeiro argumento for _menor_ que o segundo, um valor inteiro positivo se o primeiro argumento for _maior_ que o segundo e zero se os argumentos forem equivalentes. `key` é passado como o primeiro argumento, um elemento do array como o segundo.
A assinatura da função de comparação deve ser equivalente à seguinte: int cmp(const void *a, const void *b); A função não deve modificar os objetos passados a ela e deve retornar resultados consistentes quando chamada para os mesmos objetos, independentemente de suas posições no array. ​
- **context** — estado do comparador (por exemplo, sequência de ordenação), passado para `comp` como o terceiro argumento

### Valor de retorno

1) Ponteiro para um elemento no array que compara como igual a *key, ou ponteiro nulo se tal elemento não foi encontrado.

2) O mesmo que (1), exceto que o ponteiro nulo também é retornado em caso de violações de restrições em tempo de execução.

3,4) O mesmo que (1) e (2) respectivamente, exceto que a qualificação cv é ajustada.

### Notas

Apesar do nome, nem os padrões C nem POSIX exigem que esta função seja implementada usando busca binária ou que faça quaisquer garantias de complexidade.

Ao contrário de outras funções com verificação de limites, `bsearch_s` não trata arrays de tamanho zero como uma violação de restrição em tempo de execução e, em vez disso, indica que o elemento não foi encontrado (a outra função que aceita arrays de tamanho zero é qsort_s).

Até `bsearch_s`, os usuários de `bsearch` frequentemente usavam variáveis globais para representar o estado do comparador.

### Exemplo

Execute este código
```c
    #include <stdlib.h>
    #include <stdio.h>
    
    struct data {
        int nr;
        char const *value;
    } dat[] = {
        {1, "Foo"}, {2, "Bar"}, {3, "Hello"}, {4, "World"}
    };
    
    int data_cmp(void const *lhs, void const *rhs) 
    {
        struct data const *const l = lhs;
        struct data const *const r = rhs;
    
        if (l->nr < r->nr) return -1;
        else if (l->nr > r->nr) return 1;
        else return 0;
    
        // return (l->nr > r->nr) - (l->nr < r->nr); // possible shortcut
        // return l->nr - r->nr; // erroneous shortcut (fails if INT_MIN is present)
    }
    
    int main(void) 
    {
        struct data key = { .nr = 3 };
        struct data const *res = bsearch(&key, dat, sizeof dat / sizeof dat[0],
                                         sizeof dat[0], data_cmp);
        if (res) {
            printf("No %d: %s\n", res->nr, res->value);
        } else {
            printf("No %d not found\n", key.nr);
        }
    }
```

Saída:
```
    No 3: Hello
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    * 7.22.5.1 A função bsearch (p: 258)

    * K.3.6.3.1 A função bsearch_s (p: 441-442)

  * Padrão C11 (ISO/IEC 9899:2011):

    * 7.22.5.1 A função bsearch (p: 355)

    * K.3.6.3.1 A função bsearch_s (p: 608-609)

  * Padrão C99 (ISO/IEC 9899:1999):

    * 7.20.5.1 A função bsearch (p: 318-319)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    * 4.10.5.1 A função bsearch

### Veja também

[ qsortqsort_s](<#/doc/algorithm/qsort>)(C11) | ordena um intervalo de elementos com tipo não especificado
(função)
[Documentação C++](<#/>) para bsearch