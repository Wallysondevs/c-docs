# _Exit

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
void _Exit( int exit_code );  // desde C99
(até C11)  // até C11
_Noreturn void _Exit( int exit_code );  // desde C11
(até C23)  // até C23
[[noreturn]] void _Exit( int exit_code );  // desde C23
```

Causa o término normal do programa sem limpar completamente os recursos.

Funções passadas para [at_quick_exit()](<#/doc/program/at_quick_exit>) ou [atexit()](<#/doc/program/atexit>) não são chamadas. Se fluxos abertos com dados em buffer não gravados são descarregados, fluxos abertos são fechados ou arquivos temporários são removidos é definido pela implementação.

Se `exit_code` for 0 ou [EXIT_SUCCESS](<#/doc/program/EXIT_status>), um status definido pela implementação indicando término bem-sucedido é retornado ao ambiente hospedeiro. Se `exit_code` for [EXIT_FAILURE](<#/doc/program/EXIT_status>), um status definido pela implementação, indicando término _mal-sucedido_, é retornado. Em outros casos, um valor de status definido pela implementação é retornado.

### Parâmetros

- **exit_code** — status de saída do programa

### Valor de retorno

(nenhum)

### Exemplo

Execute este código
```c
    #include <stdlib.h>
    #include <stdio.h>
    
    /* _Exit does not call functions registered with atexit. */
    void f1(void)
    {
        puts("pushed first");
    }
    
    void f2(void)
    {
        puts("pushed second");
    }
    
    int main(void)
    {
        printf("Enter main()\n");
        atexit(f1);
        atexit(f2);
        fflush(stdout);   /* _Exit may not flush unwritten buffered data */
        _Exit(0);
    }
```

Saída:
```
    Enter main()
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.22.4.5 A função _Exit (p: 256)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.22.4.5 A função _Exit (p: 352)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.20.4.4 A função _Exit (p: 316)

### Veja também

[ abort](<#/doc/program/abort>) | causa o término anormal do programa (sem limpeza)
(função)
[ exit](<#/doc/program/exit>) | causa o término normal do programa com limpeza
(função)
[Documentação C++](<#/>) para _Exit