# setjmp

Definido no cabeçalho [`<setjmp.h>`](<#/doc/program>)

```c
#define setjmp(env) /* implementation-defined */
```

  
Salva o contexto de execução atual em uma variável `env` do tipo [jmp_buf](<#/doc/program/jmp_buf>). Esta variável pode ser usada posteriormente para restaurar o contexto de execução atual pela função [longjmp](<#/doc/program/longjmp>). Ou seja, quando uma chamada para a função [longjmp](<#/doc/program/longjmp>) é feita, a execução continua no local da chamada específico que construiu a variável [jmp_buf](<#/doc/program/jmp_buf>) passada para [longjmp](<#/doc/program/longjmp>). Nesse caso, `setjmp` retorna o valor passado para [longjmp](<#/doc/program/longjmp>).

A invocação de `setjmp` deve aparecer apenas em um dos seguintes contextos:

  1. A expressão de controle completa de [`if`](<#/doc/language/if>), [`switch`](<#/doc/language/switch>), [`while`](<#/doc/language/while>), [`do-while`](<#/doc/language/do>), [`for`](<#/doc/language/for>).
`switch(setjmp(env)) { // ...
```

  2. Um operando de um operador relacional ou de igualdade com o outro operando sendo uma expressão constante inteira, com a expressão resultante sendo a expressão de controle completa de `if`, `switch`, `while`, `do-while`, `for`.
`if(setjmp(env) > 10) { // ...
```

  3. O operando de um operador unário ! com a expressão resultante sendo a expressão de controle completa de [`if`](<#/doc/language/if>), [`switch`](<#/doc/language/switch>), [`while`](<#/doc/language/while>), [`do-while`](<#/doc/language/do>), [`for`](<#/doc/language/for>).
`while(!setjmp(env)) { // ...
```

  4. A expressão completa de uma instrução de expressão (possivelmente convertida para `void`).
`setjmp(env);
```

Se `setjmp` aparecer em qualquer outro contexto, o comportamento é indefinido.

Ao retornar ao escopo de `setjmp`:

  * todos os objetos acessíveis, flags de status de ponto flutuante e outros componentes da máquina abstrata têm os mesmos valores que tinham quando [longjmp](<#/doc/program/longjmp>) foi executado,
  * exceto pelas variáveis locais não-[`volatile`](<#/doc/language/volatile>) na função que contém a invocação de `setjmp`, cujos valores são indeterminados se foram alterados desde a invocação de `setjmp`.

### Parâmetros

env  |  \-  |  variável para salvar o estado de execução do programa.   
  
### Valor de retorno

​0​ se a macro foi chamada pelo código original e o contexto de execução foi salvo em `env`.

Valor diferente de zero se um salto não-local acabou de ser realizado. O valor de retorno é o mesmo que foi passado para [longjmp](<#/doc/program/longjmp>).

### Notas

Os requisitos acima proíbem o uso do valor de retorno de `setjmp` no fluxo de dados (por exemplo, para inicializar ou atribuir um objeto com ele). O valor de retorno só pode ser usado no fluxo de controle ou descartado.

### Exemplo

Execute este código
```
    #include <stdio.h>
    #include <setjmp.h>
    #include <stdnoreturn.h>
     
    jmp_buf my_jump_buffer;
     
    noreturn void foo(int status) 
    {
        printf("foo(%d) called\n", status);
        longjmp(my_jump_buffer, status + 1); // will return status+1 out of setjmp
    }
     
    int main(void)
    {
        volatile int count = 0; // modified local vars in setjmp scope must be volatile
        if (setjmp(my_jump_buffer) != 5) // compare against constant in an if
            foo(++count);
    }
```

Saída:
```
    foo(1) called
    foo(2) called
    foo(3) called
    foo(4) called
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.13.1.1 A macro setjmp (p: 191)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.13.1.1 A macro setjmp (p: 262-263)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.13.1.1 A macro setjmp (p: 243-244)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.6.1 A macro setjmp

### Veja também

[ longjmp](<#/doc/program/longjmp>) |  salta para o local especificado   
(função)  
[Documentação C++](<#/>) para setjmp