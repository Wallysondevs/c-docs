# set_constraint_handler_s, constraint_handler_t

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
constraint_handler_t set_constraint_handler_s( constraint_handler_t handler );  // desde C11
typedef void (*constraint_handler_t)( const char* restrict msg,
void* restrict ptr,
errno_t error );  // desde C11
```

1) Configura o manipulador a ser chamado por todas as [funções com verificação de limites](<#/doc/error>) em caso de violação de restrição em tempo de execução ou restaura o manipulador padrão (se handler for um ponteiro nulo).

2) O ponteiro para um manipulador que será chamado em caso de violação de restrição em tempo de execução.

Se `set_constraint_handler_s` nunca for chamado, o manipulador padrão é definido pela implementação: pode ser abort_handler_s, ignore_handler_s, ou algum outro manipulador definido pela implementação.

Assim como todas as funções com verificação de limites, `set_constraint_handler_s` e `constraint_handler_t` são garantidos de estarem disponíveis apenas se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir [`<stdlib.h>`](<#/doc/program>).

### Parâmetros

- **handler** — ponteiro para função do tipo `constraint_handler_t` ou um ponteiro nulo
- **msg** — ponteiro para uma string de caracteres que descreve o erro
- **ptr** — ponteiro para um objeto definido pela implementação ou um ponteiro nulo. Exemplos de objetos definidos pela implementação são objetos que fornecem o nome da função que detectou a violação e o número da linha quando a violação foi detectada
- **error** — o erro prestes a ser retornado pela função chamadora, se for uma das funções que retornam `errno_t`

### Valor de retorno

Um ponteiro para o manipulador de restrições em tempo de execução previamente instalado. (Nota: este ponteiro nunca é um ponteiro nulo porque chamar set_constraint_handler_s([NULL](<#/doc/types/NULL>)) configura o manipulador padrão do sistema).

### Exemplo

Execute este código
```c
    #define __STDC_WANT_LIB_EXT1__ 1
    #include <string.h>
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(void)
    {
    #ifdef __STDC_LIB_EXT1__
        char dst[2];
        set_constraint_handler_s(ignore_handler_s);
        int r = strcpy_s(dst, sizeof dst, "Too long!");
        printf("dst = \"%s\", r = %d\n", dst, r);
        set_constraint_handler_s(abort_handler_s);
        r = strcpy_s(dst, sizeof dst, "Too long!");
        printf("dst = \"%s\", r = %d\n", dst, r);
    #endif
    }
```

Saída possível:
```
    dst = "", r = 22
    abort_handler_s was called in response to a runtime-constraint violation.
    
    The runtime-constraint violation was caused by the following expression in strcpy_s:
    (s1max <= (s2_len=strnlen_s(s2, s1max)) ) (in string_s.c:62)
    
    Note to end users: This program was terminated as a result
    of a bug present in the software. Please reach out to your
    software's vendor to get more help.
    Aborted
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * K.3.6/2 constraint_handler_t (p: TBD)

    

  * K.3.6.1.1 A função set_constraint_handler_s (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * K.3.6/2 constraint_handler_t (p: TBD)

    

  * K.3.6.1.1 A função set_constraint_handler_s (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * K.3.6/2 constraint_handler_t (p: 604)

    

  * K.3.6.1.1 A função set_constraint_handler_s (p: 604-605)

### Veja também

[ abort_handler_s](<#/doc/error/abort_handler_s>)(C11) | callback de aborto para as funções com verificação de limites
(função)
[ ignore_handler_s](<#/doc/error/ignore_handler_s>)(C11) | callback de ignorar para as funções com verificação de limites
(função)