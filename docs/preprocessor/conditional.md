# Inclusão condicional

O pré-processador suporta a compilação condicional de partes do arquivo fonte. Este comportamento é controlado pelas diretivas `#if`, `#else`, `#elif`, `#ifdef`, `#ifndef`, `#elifdef`, `#elifndef`(desde C23), e `#endif`.

### Sintaxe

---
`#if` expression
`#ifdef` identifier
`#ifndef` identifier
`#elif` expression
`#elifdef` identifier | | (desde C23)
`#elifndef` identifier | | (desde C23)
`#else`
`#endif`

### Explicação

O bloco de pré-processamento condicional começa com a diretiva `#if`, `#ifdef` ou `#ifndef`, então opcionalmente inclui qualquer número de diretivas `#elif`, `#elifdef`, ou `#elifndef`(desde C23), então opcionalmente inclui no máximo uma diretiva `#else` e é terminado com a diretiva `#endif`. Quaisquer blocos de pré-processamento condicional internos são processados separadamente.

Cada uma das diretivas `#if`, `#ifdef`, `#ifndef`, `#elif`, `#elifdef`, `#elifndef`(desde C23), e `#else` controla um bloco de código até a primeira diretiva `#elif`, `#elifdef`, `#elifndef`(desde C23), `#else`, `#endif` que não pertença a nenhum bloco de pré-processamento condicional interno.

As diretivas `#if`, `#ifdef` e `#ifndef` testam a condição especificada (veja abaixo) e, se ela for avaliada como verdadeira, compilam o bloco de código controlado. Nesse caso, as diretivas subsequentes `#else`, `#elifdef`, `#elifndef`,(desde C23) e `#elif` são ignoradas. Caso contrário, se a condição especificada for avaliada como falsa, o bloco de código controlado é ignorado e a diretiva subsequente `#else`, `#elifdef`, `#elifndef`,(desde C23) ou `#elif` (se houver) é processada. Se a diretiva subsequente for `#else`, o bloco de código controlado pela diretiva `#else` é compilado incondicionalmente. Caso contrário, a diretiva `#elif`, `#elifdef`, ou `#elifndef`(desde C23) age como se fosse uma diretiva `#if`: verifica a condição, compila ou ignora o bloco de código controlado com base no resultado, e neste último caso processa as diretivas subsequentes `#elif`, `#elifdef`, `#elifndef`,(desde C23) e `#else`. O bloco de pré-processamento condicional é terminado pela diretiva `#endif`.

### Avaliação condicional

#### #if, #elif

A expressão é uma expressão constante, usando apenas [constantes](<#/doc/language/expressions>) e identificadores, definidos usando a diretiva [` #define`](<#/doc/preprocessor/replace>). Qualquer identificador, que não seja literal, não definido usando a diretiva [` #define`](<#/doc/preprocessor/replace>), é avaliado como ​0​ exceto true que é avaliado como 1(desde C23).

A expressão pode conter operadores unários na forma `defined` identifier ou `defined (`identifier`)` que retornam 1 se o identificador foi definido usando a diretiva [` #define`](<#/doc/preprocessor/replace>) e ​0​ caso contrário. Neste contexto, __has_include, __has_embed e __has_c_attribute são tratados como se fossem o nome de macros definidas.(desde C23) Se a expressão for avaliada como um valor diferente de zero, o bloco de código controlado é incluído e ignorado caso contrário. Se qualquer identificador usado não for uma constante, ele é substituído por ​0​.

No contexto de uma diretiva de pré-processador, uma expressão `__has_c_attribute` detecta se um determinado token de atributo é suportado e sua versão suportada. Veja [Teste de atributos](<#/doc/language/attributes>). | (desde C23)

Nota: Até [DR 412](<https://open-std.org/JTC1/SC22/WG14/www/docs/dr_412.htm>), `#if _cond1_` ... `#elif _cond2_` é diferente de `#if _cond1_` ... `#else` seguido por `#if _cond3_` porque se `_cond1_` for verdadeiro, o segundo `#if` é ignorado e `_cond3_` não precisa ser bem-formado, enquanto o `_cond2_` do `#elif` deve ser uma expressão válida. A partir de [DR 412](<https://open-std.org/JTC1/SC22/WG14/www/docs/dr_412.htm>), o `#elif` que leva ao bloco de código ignorado também é ignorado.

#### Diretivas combinadas

Verifica se o identificador foi [definido como um nome de macro](<#/doc/preprocessor/replace>).

`#ifdef` identifier é essencialmente equivalente a `#if defined` identifier.

`#ifndef` identifier é essencialmente equivalente a `#if !defined` identifier.

`#elifdef` identifier é essencialmente equivalente a `#elif defined` identifier. `#elifndef` identifier é essencialmente equivalente a `#elif !defined` identifier. | (desde C23)

### Notas

Embora as diretivas `#elifdef` e `#elifndef` visem o C23, as implementações podem fazer o backport delas para modos de linguagem mais antigos como extensões conformes.

### Exemplo

Execute este código
```c
    #define ABCD 2
    #include <stdio.h>
    
    int main(void)
    {
    
    #ifdef ABCD
        printf("1: yes\n");
    #else
        printf("1: no\n");
    #endif
    
    #ifndef ABCD
        printf("2: no1\n");
    #elif ABCD == 2
        printf("2: yes\n");
    #else
        printf("2: no2\n");
    #endif
    
    #if !defined(DCBA) && (ABCD < 2 * 4 - 3)
        printf("3: yes\n");
    #endif
    
    // C23 directives #elifdef/#elifndef
    #ifdef CPU
        printf("4: no1\n");
    #elifdef GPU
        printf("4: no2\n");
    #elifndef RAM
        printf("4: yes\n"); // selecionado no modo C23, pode ser selecionado no modo pré-C23
    #else
        printf("4: no3\n"); // pode ser selecionado no modo pré-C23
    #endif
    }
```

Saída possível:
```
    1: yes
    2: yes
    3: yes
    4: yes
```

### Relatórios de defeitos

Os seguintes relatórios de defeitos que alteram o comportamento foram aplicados retroativamente a padrões C publicados anteriormente.

DR | Aplicado a | Comportamento conforme publicado | Comportamento correto
[DR 412](<https://www.open-std.org/jtc1/sc22/wg14/www/docs/n2396.htm#dr_412>) | C89 | a expressão do `#elif` falho era exigida como válida | `#elif` falho é ignorado

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 6.10.1 Inclusão condicional (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 6.10.1 Inclusão condicional (p: 118-119)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 6.10.1 Inclusão condicional (p: 162-164)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 6.10.1 Inclusão condicional (p: 147-149)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 3.8.1 Inclusão condicional

### Veja também

[Documentação C++](<#/>) para Inclusão condicional
---