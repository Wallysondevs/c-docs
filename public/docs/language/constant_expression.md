# Expressões Constantes

Diversas variedades de expressões são conhecidas como _expressões constantes_

### Expressão Constante do Pré-processador

A expressão que segue [`#if` ou `#elif`](<#/doc/preprocessor/conditional>) deve se expandir para

*   [operadores](<#/doc/language/expressions>) que não sejam de [atribuição](<#/doc/language/operator_assignment>), [incremento, decremento](<#/doc/language/operator_incdec>), [chamada de função](<#/doc/language/operator_other>), ou [vírgula](<#/doc/language/operator_other>) cujos argumentos são expressões constantes do pré-processador
*   [constantes inteiras](<#/doc/language/integer_constant>)
*   [constantes de caractere](<#/doc/language/character_constant>)
*   o operador especial do pré-processador `defined`

Constantes de caractere, quando avaliadas em expressões `#if`, podem ser interpretadas no conjunto de caracteres de origem, no conjunto de caracteres de execução, ou em algum outro conjunto de caracteres definido pela implementação.

A aritmética inteira em expressões `#if` é realizada usando a semântica de [intmax_t](<#/doc/types/integer>) para tipos com sinal e [uintmax_t](<#/doc/types/integer>) para tipos sem sinal. | (desde C99)

### Expressão Constante Inteira

Uma expressão constante inteira é uma expressão que consiste apenas em

*   [operadores](<#/doc/language/expressions>) que não sejam de [atribuição](<#/doc/language/operator_assignment>), [incremento, decremento](<#/doc/language/operator_incdec>), [chamada de função](<#/doc/language/operator_other>), ou [vírgula](<#/doc/language/operator_other>), exceto que operadores de [conversão de tipo (cast)](<#/doc/language/cast>) só podem converter tipos aritméticos para tipos inteiros, a menos que façam parte de um operando para um operador sizeof , _Alignof(desde C11)(até C23), alignas(desde C23) ou typeof/typeof_unqual(desde C23).
*   [constantes inteiras](<#/doc/language/integer_constant>)
*   [constantes de enumeração](<#/doc/language/enum>)
*   [constantes de caractere](<#/doc/language/character_constant>)
*   [constantes de ponto flutuante](<#/doc/language/floating_constant>), mas apenas se forem usadas imediatamente como operandos de conversões de tipo (casts) para tipo inteiro
*   operadores [`sizeof`](<#/doc/language/sizeof>) cujos operandos não são VLA(desde C99)
*   operadores _Alignof(até C23)alignas(desde C23)

| (desde C11)

*   constantes literais nomeadas e compostas que são do tipo inteiro ou que são do tipo aritmético e são os operandos imediatos de conversões de tipo (casts)

| (desde C23)

Expressões constantes inteiras são avaliadas em tempo de compilação. Os seguintes contextos exigem expressões que são conhecidas como _expressões constantes inteiras_ :

*   O tamanho de um [campo de bits](<#/doc/language/bit_field>).
*   O valor de uma [constante de enumeração](<#/doc/language/enum>)
*   O rótulo `case` de uma [instrução switch](<#/doc/language/switch>)
*   O tamanho de um array não-VLA(desde C99)
*   [Conversão](<#/doc/language/conversion>) implícita de inteiro para ponteiro.
*   O índice em um [designador de array](<#/doc/language/array_initialization>)

| (desde C99)

*   O primeiro argumento de [`_Static_assert`](<#/doc/language/static_assert>)
*   O argumento inteiro de [`_Alignof`](<#/doc/language/alignof>)(até C23)[`alignof`](<#/doc/language/alignof>)(desde C23)

| (desde C11)

*   O número de bits N de um tipo inteiro de precisão de bits (_BitInt(N))

| (desde C23)

### Inicializador Estático

Expressões que são usadas nos [inicializadores](<#/doc/language/initialization>) de objetos com [duração de armazenamento](<#/doc/language/storage_duration>) static e thread_local ou declaradas com o especificador de classe de armazenamento constexpr(desde C23) devem ser literais de string ou expressões que podem ser uma das seguintes

1) _expressão constante aritmética_ , que é uma expressão de qualquer tipo aritmético que consiste em

*   [operadores](<#/doc/language/expressions>) que não sejam de [atribuição](<#/doc/language/operator_assignment>), [incremento, decremento](<#/doc/language/operator_incdec>), [chamada de função](<#/doc/language/operator_other>), ou [vírgula](<#/doc/language/operator_other>), exceto que operadores de [conversão de tipo (cast)](<#/doc/language/cast>) devem estar convertendo tipos aritméticos para outros tipos aritméticos, a menos que façam parte de um operando para um operador sizeof , _Alignof(desde C11)(até C23), alignof(desde C23) ou typeof/typeof_unqual(desde C23)
*   [constantes inteiras](<#/doc/language/integer_constant>)
*   [constantes de ponto flutuante](<#/doc/language/floating_constant>)
*   [constantes de enumeração](<#/doc/language/enum>)
*   [constantes de caractere](<#/doc/language/character_constant>)
*   operadores [`sizeof`](<#/doc/language/sizeof>) cujos operandos não são VLA(desde C99)
*   operadores [`_Alignof`](<#/doc/language/alignof>)(até C23)[`alignof`](<#/doc/language/alignof>)(desde C23)

| (desde C11)

*   constantes literais nomeadas ou compostas de tipo aritmético

| (desde C23)

2) uma constante de ponteiro nulo (ex: [NULL](<#/doc/types/NULL>))

3) _expressão constante de endereço_ , que é

*   um ponteiro nulo
*   [lvalue](<#/doc/language/value_category>) designando um objeto com [duração de armazenamento](<#/doc/language/storage_duration>) static ou um designador de função, convertido para um ponteiro, seja
    *   usando o operador unário de endereço-de
    *   convertendo (casting) uma constante inteira para um ponteiro
    *   por [conversão](<#/doc/language/conversion>) implícita de array para ponteiro ou de função para ponteiro

4) _expressão constante de endereço_ de algum tipo de objeto completo, mais ou menos uma _expressão constante inteira_

5) uma _constante nomeada_ que é, um identificador que é

*   uma constante de enumeração
*   uma constante predefinida (uma de true, false ou nullptr)
*   declarada com o especificador de classe de armazenamento constexpr e tem um tipo de objeto

ou uma expressão postfix que aplica o operador de acesso a membro `.` a uma constante nomeada de tipo struct ou union, mesmo recursivamente.
6) uma _constante literal composta_ , que é

*   um [literal composto](<#/doc/language/compound_literal>) com o especificador de classe de armazenamento constexpr
*   uma expressão postfix que aplica o operador de acesso a membro `.` a uma constante literal composta de tipo struct ou union, mesmo recursivamente.

Uma _constante de struct ou union_ é uma constante nomeada ou constante literal composta com tipo struct ou union, respectivamente. Se o operador de acesso a membro `.` acessa um membro de uma constante union, o membro acessado deve ser o mesmo que o membro que é inicializado pelo inicializador da constante union. | (desde C23)

7) expressão constante de uma das outras formas aceitas pela implementação.

Ao contrário das expressões constantes inteiras, as expressões de inicializador estático não são obrigadas a ser avaliadas em tempo de compilação; o compilador tem a liberdade de transformar tais inicializadores em código executável que é invocado antes do início do programa.
```c
    static int i = 2 || 1 / 0; // initializes i to value 1
```

| Esta seção está incompleta
Razão: outros mini-exemplos

O valor de um inicializador estático de ponto flutuante nunca é menos preciso do que o valor da mesma expressão executada em tempo de execução, mas pode ser melhor.

### Expressões Constantes de Ponto Flutuante

Expressões constantes aritméticas de tipos de ponto flutuante que não são usadas em inicializadores estáticos são sempre avaliadas como se fossem em tempo de execução e são afetadas pelo [arredondamento atual](<#/doc/numeric/fenv/FE_round>) (se [`FENV_ACCESS`](<#/doc/preprocessor/impl>) estiver ativado) e reportam erros conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>).
```c
    void f(void)
    {
    #pragma STDC FENV_ACCESS ON
        static float x = 0.0 / 0.0; // static initializer: does not raise an exception
        float w[] = { 0.0 / 0.0 };  // raises an exception
        float y = 0.0 / 0.0;        // raises an exception
        double z = 0.0 / 0.0;       // raises an exception
    }
```

### Notas

Se uma expressão avalia para um valor que não é representável por seu tipo, ela não pode ser usada como uma expressão constante.

Implementações podem aceitar outras formas de expressões constantes. No entanto, essas expressões constantes não são consideradas expressões constantes inteiras, expressões constantes aritméticas ou expressões constantes de endereço, e, portanto, não podem ser usadas nos contextos que exigem esses tipos de expressões constantes. Por exemplo, int arr[(int)+1.0]; declara um VLA.

### Referências

*   Padrão C23 (ISO/IEC 9899:2024):
    *   6.6 Expressões constantes (p: TBD)
*   Padrão C17 (ISO/IEC 9899:2018):
    *   6.6 Expressões constantes (p: 76-77)
*   Padrão C11 (ISO/IEC 9899:2011):
    *   6.6 Expressões constantes (p: 106-107)
*   Padrão C99 (ISO/IEC 9899:1999):
    *   6.6 Expressões constantes (p: 95-96)
*   Padrão C89/C90 (ISO/IEC 9899:1990):
    *   3.4 EXPRESSÕES CONSTANTES

### Veja também

[Documentação C++](<#/>) para Expressões constantes
---