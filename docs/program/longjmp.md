# longjmp

Definido no cabeçalho [`<setjmp.h>`](<#/doc/program>)

```c
void longjmp( jmp_buf env, int status );  // até C11
_Noreturn void longjmp( jmp_buf env, int status );  // desde C11
(até C23)  // até C23
[[noreturn]] void longjmp( jmp_buf env, int status );  // desde C23
```

Carrega o contexto de execução `env` salvo por uma chamada anterior a [setjmp](<#/doc/program/setjmp>). Esta função não retorna. O controle é transferido para o local da chamada da macro [setjmp](<#/doc/program/setjmp>) que configurou `env`. Esse [setjmp](<#/doc/program/setjmp>) então retorna o valor, passado como `status`.

Se a função que chamou [setjmp](<#/doc/program/setjmp>) tiver sido encerrada (seja por retorno ou por um `longjmp` diferente mais acima na pilha), o comportamento é indefinido. Em outras palavras, apenas saltos longos para cima na pilha de chamadas são permitidos.

Saltar entre threads (se a função que chamou `setjmp` foi executada por outra thread) também é comportamento indefinido. | (desde C11)
Se, quando [setjmp](<#/doc/program/setjmp>) foi chamado, uma [VLA](<#/doc/language/array>) ou outra variável de [tipo modificado variavelmente](<#/doc/language/declarations>) estava no escopo e o controle saiu desse escopo, um `longjmp` para esse `setjmp` invoca comportamento indefinido, mesmo que o controle tenha permanecido dentro da função. No caminho de volta pela pilha, `longjmp` não desaloca nenhuma VLA; vazamentos de memória podem ocorrer se suas durações de vida forem encerradas dessa maneira:
```c
    void g(int n)
    {
        int a[n]; // a pode permanecer alocado
        h(n); // não retorna
    }
    void h(int n)
    {
        int b[n]; // b pode permanecer alocado
        longjmp(buf, 2); // pode causar um vazamento de memória para b de h e a de g
    }
```

| (desde C99)

### Parâmetros

- **env** — variável que se refere ao estado de execução do programa salvo por [setjmp](<#/doc/program/setjmp>)
- **status** — o valor a ser retornado de [setjmp](<#/doc/program/setjmp>). Se for igual a ​0​, 1 é usado em vez disso

### Valor de retorno

(nenhum)

### Observações

`longjmp` é destinado ao tratamento de condições de erro inesperadas onde a função não pode retornar de forma significativa. Isso é semelhante ao tratamento de exceções em outras linguagens de programação.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <setjmp.h>
    #include <stdnoreturn.h>
    
    jmp_buf my_jump_buffer;
    
    noreturn void foo(int status) 
    {
        printf("foo(%d) called\n", status);
        longjmp(my_jump_buffer, status + 1); // retornará status+1 de setjmp
    }
    
    int main(void)
    {
        volatile int count = 0; // variáveis locais modificadas no escopo de setjmp devem ser volatile
        if (setjmp(my_jump_buffer) != 5) // compara com uma constante em um if
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

    

  * 7.13.2.1 A macro longjmp (p: 191-192) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.13.2.1 A macro longjmp (p: 263-264) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.13.2.1 A macro longjmp (p: 244-245) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.6.2.1 A função longjmp 

### Veja também

[ setjmp](<#/doc/program/setjmp>) | salva o contexto
(macro de função)
[Documentação C++](<#/>) para longjmp