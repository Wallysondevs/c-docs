# memalignment

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
size_t memalignment( const void *p );  // desde C23
```

Retorna o alinhamento máximo satisfeito pelo endereço fornecido. O valor de retorno pode ser maior do que qualquer valor de alinhamento suportado pela implementação. Se `p` for um valor de ponteiro nulo, ​0​ é retornado para indicar que o ponteiro não pode ser usado para acessar um objeto de qualquer tipo.

Se o valor de retorno for maior ou igual a alignof(T), o requisito de alinhamento para o tipo `T` é satisfeito pelo ponteiro.

Uma [implementação independente](<#/doc/language/conformance>) precisa fornecer `memalignment`.

### Parâmetros

- **p** — ponteiro para consultar o alinhamento

### Valor de retorno

O valor de alinhamento de `p`, ou ​0​ se `p` for um valor de ponteiro nulo.

### Notas

Em plataformas comuns onde

*   ponteiros nulos são convertidos para o inteiro ​0​,
*   valores de ponteiro são diretamente convertidos para os valores numéricos de endereços virtuais, e
*   [size_t](<#/doc/types/size_t>) é o mesmo que [uintptr_t](<#/doc/types/integer>),

esta função pode ser implementada como `return ((size_t)p & -((size_t)p));`.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
    
    int main()
    {
        alignas(128) int i = 0;
        printf("%zu\n%zu\n", memalignment(nullptr), memalignment(&i));
    }
```

Saída possível:
```
    0
    128
```

### Referências

*   Padrão C23 (ISO/IEC 9899:2024):

*   7.24.9.1 A função memalignment (p: 374)

### Veja também

[ aligned_alloc](<#/doc/memory/aligned_alloc>)(C11) | aloca memória alinhada
(função)
[ free_aligned_sized](<#/doc/memory/free_aligned_sized>)(C23) | desaloca memória alinhada e dimensionada previamente alocada
(função)