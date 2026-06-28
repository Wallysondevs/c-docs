# aligned_alloc

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
void *aligned_alloc( size_t alignment, size_t size );  // desde C11
```

Aloca `size` bytes de armazenamento não inicializado cujo alinhamento é especificado por `alignment`. O parâmetro `size` deve ser um múltiplo integral de `alignment`.

`aligned_alloc` é thread-safe: ele se comporta como se acessasse apenas os locais de memória visíveis através de seu argumento, e não qualquer armazenamento estático.

Uma chamada anterior a [free](<#/doc/memory/free>), free_sized, e free_aligned_sized(desde C23) ou [realloc](<#/doc/memory/realloc>) que desaloca uma região de memória _sincroniza-se com_ uma chamada a `aligned_alloc` que aloca a mesma ou parte da mesma região de memória. Esta sincronização ocorre após qualquer acesso à memória pela função de desalocação e antes de qualquer acesso à memória por `aligned_alloc`. Existe uma única ordem total de todas as funções de alocação e desalocação operando em cada região particular de memória.

### Parâmetros

- **alignment** — especifica o alinhamento. Deve ser um alinhamento válido suportado pela implementação.
- **size** — número de bytes a alocar. Um múltiplo integral de `alignment`.

### Valor de retorno

Em caso de sucesso, retorna o ponteiro para o início da memória recém-alocada. Para evitar um vazamento de memória, o ponteiro retornado deve ser desalocado com [free](<#/doc/memory/free>) ou [realloc](<#/doc/memory/realloc>).

Em caso de falha, retorna um ponteiro nulo.

### Observações

Passar um `size` que não seja um múltiplo integral de `alignment` ou um `alignment` que não seja válido ou não suportado pela implementação faz com que a função falhe e retorne um ponteiro nulo (C11, conforme publicado, especificava comportamento indefinido neste caso, o que foi corrigido por [DR460](<https://open-std.org/JTC1/SC22/WG14/www/docs/summary.htm#dr_460>)). A remoção das restrições de `size` para possibilitar a alocação de pequenos objetos em limites de alinhamento restritivos (semelhante a [`alignas`](<#/doc/language/alignas>)) foi proposta por [N2072](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2072.htm>).

Como exemplo do requisito "suportado pela implementação", a função POSIX [`posix_memalign`](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/posix_memalign.html>) aceita qualquer alinhamento que seja uma potência de dois e um múltiplo de `sizeof(void *)`, e as implementações de `aligned_alloc` baseadas em POSIX herdam esses requisitos.

Alinhamentos fundamentais são sempre suportados. Se `alignment` for uma potência de dois e não for maior que `_Alignof([max_align_t](<#/doc/types/max_align_t>))`, `aligned_alloc` pode simplesmente chamar [malloc](<#/doc/memory/malloc>).

[malloc](<#/doc/memory/malloc>) regular alinha a memória adequada para qualquer tipo de objeto com um alinhamento fundamental. O `aligned_alloc` é útil para alocações super-alinhadas, como para [SSE](<https://en.wikipedia.org/wiki/Streaming_SIMD_Extensions> "enwiki:Streaming SIMD Extensions"), linha de cache, ou limite de [página de VM](<https://en.wikipedia.org/wiki/Page_\(computer_memory\)#Multiple_page_sizes> "enwiki:Page \(computer memory\)")

Esta função não é suportada na biblioteca de tempo de execução C da Microsoft porque sua implementação de `std::free` é [incapaz de lidar com alocações alinhadas](<https://learn.microsoft.com/en-us/cpp/standard-library/cstdlib#remarks-6>) de qualquer tipo. Em vez disso, o MS CRT fornece [`_aligned_malloc`](<https://learn.microsoft.com/en-us/cpp/c-runtime-library/reference/aligned-malloc>) (a ser liberado com [`_aligned_free`](<https://learn.microsoft.com/en-us/cpp/c-runtime-library/reference/aligned-free>)).

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
     
    int main(void)
    {
        int *p1 = malloc(10*sizeof *p1);
        printf("default-aligned addr:   %p\n", (void*)p1);
        free(p1);
     
        int *p2 = aligned_alloc(1024, 1024*sizeof *p2);
        printf("1024-byte aligned addr: %p\n", (void*)p2);
        free(p2);
    }
```

Saída possível:
```
    default-aligned addr:   0x1e40c20
    1024-byte aligned addr: 0x1e41000
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.22.3.1 A função aligned_alloc (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.22.3.1 A função aligned_alloc (p: 253)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.22.3.1 A função aligned_alloc (p: 347-348)

### Veja também

[Documentação C++](<#/>) para aligned_alloc
---