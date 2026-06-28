# Instrução return

Termina a função atual e retorna o valor especificado para a função chamadora.

### Sintaxe

---
attr-spec-seq(optional) `return` expression `;` | (1) |
attr-spec-seq(optional) `return` `;` | (2) |
- **expression** — expressão usada para inicializar o valor de retorno da função
- **attr-spec-seq** — (C23) lista opcional de [atributos](<#/doc/language/attributes>), aplicada à instrução `return`

### Explicação

1) Avalia a expressão, termina a função atual e retorna o resultado da expressão para o chamador (o valor retornado torna-se o valor da expressão de chamada da função). Válido apenas se o tipo de retorno da função não for void.

2) Termina a função atual. Válido apenas se o tipo de retorno da função for void.

Se o tipo da expressão for diferente do tipo de retorno da função, seu valor é [convertido](<#/doc/language/conversion>) como se por atribuição a um objeto cujo tipo é o tipo de retorno da função, exceto que a sobreposição entre representações de objetos é permitida:
```c
    struct s { double i; } f(void); // function returning struct s
    union { struct { int f1; struct s f2; } u1;
            struct { struct s f3; int f4; } u2; } g;
    struct s f(void)
    {
        return g.u1.f2;
    }
    int main(void)
    {
    // g.u2.f3 = g.u1.f2; // undefined behavior (overlap in assignment)
       g.u2.f3 = f();     // well-defined
    }
```

Se o tipo de retorno for um tipo de ponto flutuante real, o resultado pode ser representado com [maior faixa e precisão](<#/doc/types/limits/FLT_EVAL_METHOD>) do que o implícito pelo novo tipo.

Atingir o final de uma função que retorna void é equivalente a `return;`. Atingir o final de qualquer outra função que retorna valor é [comportamento indefinido](<#/>) se o resultado da função for usado em uma expressão (é permitido descartar tal valor de retorno). Para `main`, veja [função main](<#/doc/language/main_function>).

Executar a instrução `return` em uma [função no-return](<#/doc/language/_Noreturn>) é [comportamento indefinido](<#/>). | (desde C11)

### Palavras-chave

[`return`](<#/doc/keyword/return>)

### Exemplo

| Esta seção está incompleta
Razão: melhorar

Execute este código
```c
    #include <stdio.h>
    
    void fa(int i)
    {
        if (i == 2)
           return;
        printf("fa():  %d\n", i);
    } // implied return;
    
    int fb(int i)
    {
        if (i > 4)
           return 4;
        printf("fb():  %d\n", i);
        return 2;
    }
    
    int main(void)
    {
        fa(2);
        fa(1);
        int i = fb(5);   // the return value 4 used to initializes i
        i = fb(i);       // the return value 2 used as rhs of assignment
        printf("main(): %d\n", i);
    }
```

Saída:
```
    fa():   1
    fb():   4
    main(): 2
```

### Referências

* Padrão C17 (ISO/IEC 9899:2018):

  * 6.8.6.4 A instrução return (p: 111-112)

* Padrão C11 (ISO/IEC 9899:2011):

  * 6.8.6.4 A instrução return (p: 154)

* Padrão C99 (ISO/IEC 9899:1999):

  * 6.8.6.4 A instrução return (p: 139)

* Padrão C89/C90 (ISO/IEC 9899:1990):

  * 3.6.6.4 A instrução return

### Veja também

[Documentação C++](<#/>) para a instrução `return`