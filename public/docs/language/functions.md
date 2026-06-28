# Funções

Uma função é uma construção da linguagem C que associa uma [instrução composta](<#/doc/language/statements>) (o corpo da função) com um [identificador](<#/doc/language/identifier>) (o nome da função). Todo programa C inicia a execução a partir da [função main](<#/doc/language/main_function>), que ou termina, ou invoca outras funções, definidas pelo usuário ou da biblioteca.
```
    // function definition.
    // defines a function with the name "sum" and with the body "{ return x+y; }"
    int sum(int x, int y)
    {
        return x + y;
    }
```

Uma função é introduzida por uma [declaração de função](<#/doc/language/function_declaration>) ou uma [definição de função](<#/doc/language/function_definition>).

Funções podem aceitar zero ou mais _parâmetros_, que são inicializados a partir dos _argumentos_ de um [operador de chamada de função](<#/doc/language/operator_other>), e podem retornar um valor para seu chamador por meio da [instrução return](<#/doc/language/return>).
```
    int n = sum(1, 2); // parameters x and y are initialized with the arguments 1 and 2
```

O corpo de uma função é fornecido em uma [definição de função](<#/doc/language/function_definition>). Cada função não-[inline](<#/doc/language/inline>)(desde C99) que é usada em uma expressão (a menos que [não avaliada](<#/doc/language/expressions>)) deve ser [definida apenas uma vez](<#/doc/language/extern>) em um programa.

Não existem funções aninhadas (exceto onde permitido por extensões de compilador não-padrão): cada definição de função deve aparecer no escopo de arquivo, e funções não têm acesso às variáveis locais do chamador:
```
    int main(void) // the main function definition
    {
        int sum(int, int); // function declaration (may appear at any scope)
        int x = 1;  // local variable in main
        sum(1, 2); // function call

    //    int sum(int a, int b) // error: no nested functions
    //    {
    //        return  a + b;
    //    }
    }
    int sum(int a, int b) // function definition
    {
    //    return x + a + b; //  error: main's x is not accessible within sum
        return a + b;
    }
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 6.7.7.4 Declaradores de função (incluindo protótipos) (p: TBD)

    

  * 6.9.2 Definições de função (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 6.7.6.3 Declaradores de função (incluindo protótipos) (p: 96-98)

    

  * 6.9.1 Definições de função (p: 113-115)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 6.7.6.3 Declaradores de função (incluindo protótipos) (p: 133-136)

    

  * 6.9.1 Definições de função (p: 156-158)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 6.7.5.3 Declaradores de função (incluindo protótipos) (p: 118-121)

    

  * 6.9.1 Definições de função (p: 141-143)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 3.5.4.3 Declaradores de função (incluindo protótipos)

    

  * 3.7.1 Definições de função

### Veja também

[documentação C++](<#/>) para Declaração de funções
---