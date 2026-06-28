# Definições externas e tentativas

No nível superior de uma [unidade de tradução](<#/doc/language/translation_phases>) (ou seja, um arquivo fonte com todos os #includes após o pré-processador), todo programa C é uma sequência de [declarações](<#/doc/language/declarations>), que declaram funções e objetos com [ligação externa ou interna](<#/doc/language/storage_duration>). Essas declarações são conhecidas como _declarações externas_ porque aparecem fora de qualquer função.
```c
    extern int n; // external declaration with external linkage
    int b = 1;    // external definition with external linkage
    static const char *c = "abc"; // external definition with internal linkage
    
    int f(void)    // external definition with external linkage
    {
        int a = 1; // non-external
        return b;
    }
    
    static void x(void) // external definition with internal linkage
    {
    }
```
Objetos declarados com uma declaração externa têm [duração de armazenamento](<#/doc/language/storage_duration>) estática e, como tal, não podem usar os especificadores auto ou register, exceto que auto pode ser usado para inferência de tipo (desde C23). Os identificadores introduzidos por declarações externas têm [escopo de arquivo](<#/doc/language/scope>).

### Definições tentativas

Uma _definição tentativa_ é uma declaração externa sem um inicializador, e sem um [especificador de classe de armazenamento](<#/doc/language/storage_duration>) ou com o especificador static.

Uma _definição tentativa_ é uma declaração que pode ou não atuar como uma definição. Se uma definição externa real for encontrada antes ou depois na mesma unidade de tradução, então a definição tentativa atua apenas como uma declaração.
```c
    int i1 = 1;     // definition, external linkage
    int i1;         // tentative definition, acts as declaration because i1 is defined
    extern int i1;  // declaration, refers to the earlier definition
    
    extern int i2 = 3; // definition, external linkage
    int i2;            // tentative definition, acts as declaration because i2 is defined
    extern int i2;     // declaration, refers to the external linkage definition
```
Se não houver definições na mesma unidade de tradução, então a definição tentativa atua como uma definição real que [inicializa com vazio](<#/doc/language/initialization>) o objeto.
```c
    int i3;        // tentative definition, external linkage
    int i3;        // tentative definition, external linkage
    extern int i3; // declaration, external linkage
    // in this translation unit, i3 is defined as if by "int i3 = 0;"
```
Ao contrário das declarações [extern](<#/doc/language/storage_duration>), que não alteram a ligação de um identificador se uma declaração anterior a estabeleceu, as definições tentativas podem discordar na ligação com outra declaração do mesmo identificador. Se duas declarações para o mesmo identificador estiverem no escopo e tiverem ligação diferente, o comportamento é indefinido:
```c
    static int i4 = 2; // definition, internal linkage
    int i4;            // Undefined behavior: linkage disagreement with previous line
    extern int i4;     // declaration, refers to the internal linkage definition
    
    static int i5; // tentative definition, internal linkage
    int i5;        // Undefined behavior: linkage disagreement with previous line
    extern int i5; // refers to previous, whose linkage is internal
```
Uma definição tentativa com ligação interna deve ter tipo completo.
```c
    static int i[]; // Error, incomplete type in a static tentative definition
    int i[]; // OK, equivalent to int i[1] = {0}; unless redeclared later in this file
```
### Regra de uma única definição

Cada unidade de tradução pode ter zero ou uma definição externa de cada identificador com [ligação interna](<#/doc/language/storage_duration>) (uma global estática).

Se um identificador com ligação interna for usado em qualquer expressão que não seja uma não-VLA (desde C99), [`sizeof`](<#/doc/language/sizeof>), [`_Alignof`](<#/doc/language/alignof>) (desde C11) (até C23), [`alignof`](<#/doc/language/alignof>) (desde C23), ou [`typeof`](<#/doc/language/typeof_unqual>) (desde C23), deve haver uma e apenas uma definição externa para esse identificador na unidade de tradução.

O programa inteiro pode ter zero ou uma definição externa de cada identificador com [ligação externa](<#/doc/language/storage_duration>).

Se um identificador com ligação externa for usado em qualquer expressão que não seja uma não-VLA (desde C99), [`sizeof`](<#/doc/language/sizeof>), [`_Alignof`](<#/doc/language/alignof>) (desde C11) (até C23), [`alignof`](<#/doc/language/alignof>) (desde C23), ou [`typeof`](<#/doc/language/typeof_unqual>) (desde C23), deve haver uma e apenas uma definição externa para esse identificador em algum lugar de todo o programa.

### Notas

| Definições inline em diferentes unidades de tradução não são restringidas pela regra de uma única definição. Veja [`inline`](<#/doc/language/inline>) para detalhes sobre as definições de funções inline. | (desde C99) |
|---|---|

Veja [duração de armazenamento e ligação](<#/doc/language/storage_duration>) para o significado da palavra-chave extern com declarações no escopo de arquivo.

Veja [definições](<#/doc/language/declarations>) para a distinção entre declarações e definições.

Definições tentativas foram inventadas para padronizar várias abordagens pré-C89 para declarar antecipadamente identificadores com ligação interna.

### Referências

  * C23 standard (ISO/IEC 9899:2024):

    

  * 6.9 External definitions (p: TBD)

  * C17 standard (ISO/IEC 9899:2018):

    

  * 6.9 External definitions (p: 113-116)

  * C11 standard (ISO/IEC 9899:2011):

    

  * 6.9 External definitions (p: 155-159)

  * C99 standard (ISO/IEC 9899:1999):

    

  * 6.9 External definitions (p: 140-144)

  * C89/C90 standard (ISO/IEC 9899:1990):

    

  * 3.7 EXTERNAL DEFINITIONS