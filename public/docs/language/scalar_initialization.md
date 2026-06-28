# Inicialização escalar

Ao [inicializar](<#/doc/language/initialization>) um objeto de [tipo escalar](<#/doc/language/compatible_type>), o inicializador deve ser uma única expressão

O inicializador para um escalar (um objeto de tipo inteiro, incluindo booleanos e tipos enumerados, tipo de ponto flutuante, incluindo complexos e imaginários, e tipo ponteiro, incluindo ponteiro para função) deve ser uma única expressão, opcionalmente entre chaves, ou um inicializador vazio (desde C23):

---
`=` expression | (1) |
`=` `{` expression `}` | (2) |
`=` `{` `}` | (3) | (desde C23)

1,2) A expressão é avaliada, e seu valor, após [conversão como se por atribuição](<#/doc/language/conversion>) para o tipo do objeto, torna-se o valor inicial do objeto que está sendo inicializado.

3) O objeto é [inicializado vazio](<#/doc/language/initialization>), ou seja, inicializado para zero numérico para um objeto de tipo aritmético ou de enumeração, ou valor de ponteiro nulo para um objeto de tipo ponteiro.

### Notas

Devido às regras que se aplicam às conversões como se por atribuição, os qualificadores [`const`](<#/doc/language/const>) e [`volatile`](<#/doc/language/volatile>) no tipo declarado são ignorados ao determinar para qual tipo a expressão deve ser convertida.

Consulte [inicialização](<#/doc/language/initialization>) para as regras que se aplicam quando nenhum inicializador é usado.

Assim como em todas as outras inicializações, a expressão deve ser uma [expressão constante](<#/doc/language/constant_expression>) ao inicializar objetos com [duração de armazenamento](<#/doc/language/storage_duration>) estática ou de thread-local.

A expressão não pode ser um [operador vírgula](<#/doc/language/operator_other>) (a menos que entre parênteses) porque a vírgula no nível superior seria interpretada como o início do próximo declarador.

Ao inicializar objetos de tipo de ponto flutuante, todos os cálculos para os objetos com [duração de armazenamento](<#/doc/language/storage_duration>) automática são feitos como se em tempo de execução e são afetados pelo [arredondamento atual](<#/doc/numeric/fenv/FE_round>); erros de ponto flutuante são relatados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>). Para objetos com duração de armazenamento estática e thread-local, os cálculos são feitos como se em tempo de compilação, e nenhuma exceção é levantada:
```c
    void f(void)
    {
    #pragma STDC FENV_ACCESS ON
        static float v = 1.1e75; // não levanta exceções: inicialização estática
    
        float u[] = { 1.1e75 }; // levanta FE_INEXACT
        float w = 1.1e75;       // levanta FE_INEXACT
    
        double x = 1.1e75; // pode levantar FE_INEXACT (depende de FLT_EVAL_METHOD)
        float y = 1.1e75f; // pode levantar FE_INEXACT (depende de FLT_EVAL_METHOD)
    
        long double z = 1.1e75; // não levanta exceções (conversão é exata)
    }
```

### Exemplo

Execute este código
```c
    #include <stdbool.h>
    int main(void)
    {
        bool b = true;
        const double d = 3.14;
        int k = 3.15; // conversão de double para int
        int n = {12}, // chaves opcionais
           *p = &n,   // expressão não-constante OK para variável automática
           (*fp)(void) = main;
        enum {RED, BLUE} e = RED; // enumerações também são tipos escalares
    }
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

  * 6.7.9/11 Inicialização (p: 101)

  * Padrão C11 (ISO/IEC 9899:2011):

  * 6.7.9/11 Inicialização (p: 140)

  * Padrão C99 (ISO/IEC 9899:1999):

  * 6.7.8/11 Inicialização (p: 126)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

  * 6.5.7 Inicialização