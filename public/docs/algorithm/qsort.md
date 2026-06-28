# qsort, qsort_s

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
void qsort( void* ptr, size_t count, size_t size,
int (*comp)(const void*, const void*) );
errno_t qsort_s( void* ptr, rsize_t count, rsize_t size,
int (*comp)(const void*, const void*, void*),
void* context );  // desde C11
```

1) Ordena o array fornecido apontado por ptr em ordem crescente. O array contém count elementos de size bytes. A função apontada por comp é usada para comparação de objetos.

2) O mesmo que (1), exceto que o parâmetro de contexto adicional context é passado para comp e que os seguintes erros são detectados em tempo de execução e chamam a função [manipulador de restrição](<#/doc/error/set_constraint_handler_s>) atualmente instalada:

  * count ou size é maior que RSIZE_MAX
  * ptr ou comp é um ponteiro nulo (a menos que count seja zero)

Assim como todas as funções com verificação de limites, `qsort_s` é garantida de estar disponível apenas se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir [`<stdlib.h>`](<#/doc/program>).

Se comp indicar dois elementos como equivalentes, a ordem deles no array ordenado resultante é não especificada.

### Parâmetros

- **ptr** — ponteiro para o array a ser ordenado
- **count** — número de elementos no array
- **size** — tamanho de cada elemento no array em bytes
- **comp** — função de comparação que retorna um valor inteiro negativo se o primeiro argumento for _menor_ que o segundo, um valor inteiro positivo se o primeiro argumento for _maior_ que o segundo e zero se os argumentos forem equivalentes.
A assinatura da função de comparação deve ser equivalente à seguinte: int cmp(const void *a, const void *b); A função não deve modificar os objetos passados a ela e deve retornar resultados consistentes quando chamada para os mesmos objetos, independentemente de suas posições no array. ​
- **context** — informação adicional (por exemplo, sequência de ordenação), passada para comp como o terceiro argumento

### Valor de retorno

1) (nenhum)

2) zero em caso de sucesso, diferente de zero se uma violação de restrições em tempo de execução for detectada

### Notas

Apesar do nome, nem os padrões C nem POSIX exigem que esta função seja implementada usando [quicksort](<https://en.wikipedia.org/wiki/Quicksort> "enwiki:Quicksort") ou fazem quaisquer garantias de complexidade ou estabilidade.

Ao contrário de outras funções com verificação de limites, `qsort_s` não trata arrays de tamanho zero como uma violação de restrição em tempo de execução e, em vez disso, retorna com sucesso sem alterar o array (a outra função que aceita arrays de tamanho zero é bsearch_s).

A implementação de `qsort_s` no [Windows CRT](<https://learn.microsoft.com/en-us/cpp/c-runtime-library/reference/qsort-s>) é incompatível com o padrão C. A versão da Microsoft é declarada como: void qsort_s(void *base, [size_t](<#/doc/types/size_t>) num, [size_t](<#/doc/types/size_t>) width,
int (*compare )(void *, const void *, const void *), void * context);. Ela não retorna um valor, e a função de comparação tem uma ordem de parâmetros invertida em relação ao padrão: o contexto é passado primeiro.

### Exemplo

Execute este código
```c
    #include <limits.h>
    #include <stdio.h>
    #include <stdlib.h>
    
    int compare_ints(const void* a, const void* b)
    {
        int arg1 = *(const int*)a;
        int arg2 = *(const int*)b;
    
        if (arg1 < arg2) return -1;
        if (arg1 > arg2) return 1;
        return 0;
    
        // return (arg1 > arg2) - (arg1 < arg2); // possible shortcut
    
        // return arg1 - arg2; // erroneous shortcut: undefined behavior in case of
                               // integer overflow, such as with INT_MIN here
    }
    
    int main(void)
    {
        int ints[] = {-2, 99, 0, -743, 2, INT_MIN, 4};
        int size = sizeof ints / sizeof *ints;
    
        qsort(ints, size, sizeof(int), compare_ints);
    
        for (int i = 0; i < size; i++)
            printf("%d ", ints[i]);
    
        printf("\n");
    }
```

Saída:
```
    -2147483648 -743 -2 0 2 4 99
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    * 7.22.5.2 A função qsort (p: TBD)

    * K.3.6.3.2 A função qsort_s (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    * 7.22.5.2 A função qsort (p: 258-259)

    * K.3.6.3.2 A função qsort_s (p: 442-443)

  * Padrão C11 (ISO/IEC 9899:2011):

    * 7.22.5.2 A função qsort (p: 355-356)

    * K.3.6.3.2 A função qsort_s (p: 609)

  * Padrão C99 (ISO/IEC 9899:1999):

    * 7.20.5.2 A função qsort (p: 319)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    * 4.10.5.2 A função qsort

### Veja também

[ bsearchbsearch_s](<#/doc/algorithm/bsearch>)(C11) | busca um elemento de tipo não especificado em um array
(função)
[Documentação C++](<#/>) para qsort