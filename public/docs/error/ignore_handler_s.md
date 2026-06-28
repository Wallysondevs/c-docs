# ignore_handler_s

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
void ignore_handler_s( const char * restrict msg,
void * restrict ptr,
errno_t error
);  // desde C11
```

A função simplesmente retorna para o chamador sem realizar nenhuma outra ação.

Um ponteiro para esta função pode ser passado para [set_constraint_handler_s](<#/doc/error/set_constraint_handler_s>) para estabelecer um manipulador de violação de restrições em tempo de execução que não faz nada.

Assim como todas as funções com verificação de limites, `ignore_handler_s` tem sua disponibilidade garantida apenas se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir `<stdlib.h>`.

### Parâmetros

- **msg** — ponteiro para uma string de caracteres que descreve o erro
- **ptr** — ponteiro para um objeto definido pela implementação ou um ponteiro nulo. Exemplos de objetos definidos pela implementação são objetos que fornecem o nome da função que detectou a violação e o número da linha quando a violação foi detectada
- **error** — o erro prestes a ser retornado pela função chamadora, se for uma das funções que retornam errno_t

### Valor de retorno

(nenhum)

### Observações

Se `ignore_handler_s` for usado como manipulador de restrições em tempo de execução, as violações podem ser detectadas examinando os resultados das chamadas de função com verificação de limites, que podem ser diferentes para diferentes funções (errno_t diferente de zero, caractere nulo escrito no primeiro byte da string de saída, etc)

Se `set_constraint_handler_s` nunca for chamado, o manipulador padrão é definido pela implementação: pode ser abort_handler_s, ignore_handler_s, ou algum outro manipulador definido pela implementação.

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
        printf("dst = \"%s\", r = %d\n", dst, r);
        set_constraint_handler_s(abort_handler_s);
        r = strcpy_s(dst, sizeof dst, "Too long!");
        printf("dst = \"%s\", r = %d\n", dst, r);
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

* Padrão C11 (ISO/IEC 9899:2011):

* K.3.6.1.3 A função ignore_handler_s (p: 606)

### Veja também

[ abort_handler_s](<#/doc/error/abort_handler_s>)(C11) | callback de aborto para as funções com verificação de limites
(função)
[ set_constraint_handler_s](<#/doc/error/set_constraint_handler_s>)(C11) | define o callback de erro para as funções com verificação de limites
(função)