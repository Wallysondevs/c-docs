# Especificador de função _Noreturn (desde C11)(obsoleto em C23)

Especifica que a função não retorna ao seu ponto de invocação.

### Sintaxe

---
_Noreturn function_declaration | | (desde C11)(obsoleto em C23)

### Explicação

A palavra-chave `_Noreturn` aparece em uma declaração de função e especifica que a função não retorna pela execução da instrução `return` ou por atingir o final do corpo da função (ela pode retornar pela execução de [longjmp](<#/doc/program/longjmp>)). Se a função declarada `_Noreturn` retornar, o comportamento é indefinido. Um diagnóstico do compilador é recomendado se isso puder ser detectado.

O especificador `_Noreturn` pode aparecer mais de uma vez na mesma declaração de função, o comportamento é o mesmo como se tivesse aparecido uma vez.

Este especificador é tipicamente usado através da macro de conveniência [`noreturn`](<#/doc/types>), que é fornecida no cabeçalho `<stdnoreturn.h>`.

O especificador de função `_Noreturn` está obsoleto. O atributo `[[[noreturn](<#/doc/language/attributes/noreturn>)]]` deve ser usado em vez disso. A macro `noreturn` também está obsoleta. | (desde C23)

### Palavras-chave

[`_Noreturn`](<#/doc/keyword/_Noreturn>)

### Biblioteca padrão

As seguintes funções são `noreturn` na biblioteca padrão:

*   [abort()](<#/doc/program/abort>)
*   [exit()](<#/doc/program/exit>)
*   [_Exit()](<#/doc/program/_Exit>)
*   [quick_exit()](<#/doc/program/quick_exit>)
*   [thrd_exit()](<#/doc/thread/thrd_exit>)
*   [longjmp()](<#/doc/program/longjmp>)

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
    #include <stdnoreturn.h>
    
    // causes undefined behavior if i <= 0
    // exits if i > 0
    noreturn void exit_now(int i) // or _Noreturn void exit_now(int i)
    {
        if (i > 0)
            exit(i);
    }
    
    int main(void)
    {
        puts("Preparing to exit...");
        exit_now(2);
        puts("This code is never executed.");
    }
```

Saída:
```
    Preparing to exit...
```

### Referências

*   Padrão C23 (ISO/IEC 9899:2024):

    *   6.7.4 Especificadores de função (p: TBD)

    *   7.23 _Noreturn <stdnoreturn.h> (p: TBD)

*   Padrão C17 (ISO/IEC 9899:2018):

    *   6.7.4 Especificadores de função (p: 90-91)

    *   7.23 _Noreturn <stdnoreturn.h> (p: 263)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   6.7.4 Especificadores de função (p: 125-127)

    *   7.23 _Noreturn <stdnoreturn.h> (p: 361)

### Veja também

`[[[noreturn](<#/doc/language/attributes/noreturn>)]]`(C23)
`[[[_Noreturn](<#/doc/language/attributes/noreturn>)]]`(C23)(obsoleto) | indica que a função não retorna
(especificador de atributo)
[Documentação C++](<#/>) para `[[noreturn]]`