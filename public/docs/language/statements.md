# Instruções

Instruções são fragmentos do programa C que são executados em sequência. O corpo de qualquer função é uma instrução composta, que, por sua vez, é uma sequência de instruções e declarações:
```c
    int main(void)
    { // início de uma instrução composta
        int n = 1; // declaração (não é uma instrução)
        n = n+1; // instrução de expressão
        printf("n = %d\n", n); // instrução de expressão
        return 0; // instrução de retorno
    } // fim da instrução composta, fim do corpo da função
```

Existem cinco tipos de instruções:

1) [instruções compostas](<#/doc/language/statements>)

2) [instruções de expressão](<#/doc/language/statements>)

3) [instruções de seleção](<#/doc/language/statements>)

4) [instruções de iteração](<#/doc/language/statements>)

5) [instruções de salto](<#/doc/language/statements>)

Uma [sequência de especificadores de atributo](<#/doc/language/attributes>) (attr-spec-seq) pode ser aplicada a uma instrução sem rótulo, caso em que (exceto para uma instrução de expressão) os atributos são aplicados à instrução respectiva. | (desde C23)

### Rótulos

Qualquer instrução pode ser _rotulada_, fornecendo um nome seguido por dois pontos antes da própria instrução.

---
attr-spec-seq(optional)(desde C23) identifier `:` | (1) |
attr-spec-seq(optional)(desde C23) `case` constant-expression `:` | (2) |
attr-spec-seq(optional)(desde C23) `default` `:` | (3) |

1) Alvo para [goto](<#/doc/language/goto>).

2) Rótulo de caso em uma instrução [switch](<#/doc/language/switch>).

3) Rótulo padrão em uma instrução [switch](<#/doc/language/switch>).

Qualquer instrução (mas não uma declaração) pode ser precedida por qualquer número de _rótulos_, cada um dos quais declara identifier como um nome de rótulo, que deve ser único dentro da função envolvente (em outras palavras, nomes de rótulos têm [escopo de função](<#/doc/language/scope>)).

A declaração de rótulo não tem efeito por si só, não altera o fluxo de controle, nem modifica o comportamento da instrução que a segue de forma alguma.

Um rótulo deve ser seguido por uma instrução. | (até C23)
Um rótulo pode aparecer sem sua instrução seguinte. Se um rótulo aparece sozinho em um bloco, ele se comporta como se fosse seguido por uma [instrução nula](<#/doc/language/statements>). A [attr-spec-seq](<#/doc/language/attributes>) opcional é aplicada ao rótulo. | (desde C23)

### Instruções compostas

Uma instrução composta, ou _bloco_, é uma sequência de instruções e declarações delimitada por chaves.

---
`{` statement `|` declaration...(optional) `}` | | (até C23)
attr-spec-seq(optional) `{` unlabeled-statement `|` label `|` declaration...(optional) `}` | | (desde C23)

A instrução composta permite que um conjunto de declarações e instruções seja agrupado em uma única unidade que pode ser usada em qualquer lugar onde uma única instrução é esperada (por exemplo, em uma instrução [if](<#/doc/language/if>) ou uma instrução de iteração):
```c
    if (expr) // início da instrução if
    { // início do bloco
      int n = 1; // declaração
      printf("%d\n", n); // instrução de expressão
    } // fim do bloco, fim da instrução if
```

Cada instrução composta introduz seu próprio [escopo de bloco](<#/doc/language/scope>).

Os inicializadores das variáveis com [duração de armazenamento](<#/doc/language/storage_duration>) automática declaradas dentro de um bloco e os declaradores VLA são executados quando o fluxo de controle passa por essas declarações em ordem, como se fossem instruções:
```c
    int main(void)
    { // início do bloco
      { // início do bloco
           puts("hello"); // instrução de expressão
           int n = printf("abc\n"); // declaração, imprime "abc", armazena 4 em n
           int an*[printf("1\n")]; // declaração, imprime "1", aloca 8*sizeof(int)
           printf("%zu\n", sizeof(a)); // instrução de expressão
      } // fim do bloco, escopo de n e a termina
      int n = 7; // n pode ser reutilizado
    }
```

### Instruções de expressão

Uma expressão seguida por um ponto e vírgula é uma instrução.

---
expression(optional) `;` | (1) |
attr-spec-seq expression `;` | (2) | (desde C23)

A maioria das instruções em um programa C típico são instruções de expressão, como atribuições ou chamadas de função.

Uma instrução de expressão sem uma expressão é chamada de _instrução nula_. Ela é frequentemente usada para fornecer um corpo vazio a um loop [for](<#/doc/language/for>) ou [while](<#/doc/language/while>). Também pode ser usada para carregar um rótulo no final de uma instrução composta ou antes de uma declaração:
```c
    puts("hello"); // instrução de expressão
    char *s;
    while (*s++ != '\0')
        ; // instrução nula
```

A [attr-spec-seq](<#/doc/language/attributes>) opcional é aplicada à expressão. Uma attr-spec-seq seguida por `;` não forma uma instrução de expressão. Em vez disso, forma uma [declaração de atributo](<#/doc/language/declarations>). | (desde C23)

### Instruções de seleção

As instruções de seleção escolhem entre uma de várias instruções dependendo do valor de uma expressão.

---
attr-spec-seq(optional)(desde C23) `if` `(` expression `)` statement | (1) |
attr-spec-seq(optional)(desde C23) `if` `(` expression `)` statement `else` statement | (2) |
attr-spec-seq(optional)(desde C23) `switch` `(` expression `)` statement | (3) |

1) Instrução [if](<#/doc/language/if>)

2) Instrução [if](<#/doc/language/if>) com uma cláusula else

3) Instrução [switch](<#/doc/language/switch>)

### Instruções de iteração

As instruções de iteração executam repetidamente uma instrução.

---
attr-spec-seq(optional)(desde C23) `while` `(` expression `)` statement | (1) |
attr-spec-seq(optional)(desde C23) `do` statement `while` `(` expression `)` `;` | (2) |
attr-spec-seq(optional)(desde C23) `for` `(` init-clause `;` expression(optional) `;` expression(optional) `)` statement | (3) |

1) Loop [while](<#/doc/language/while>)

2) Loop [do-while](<#/doc/language/do>)

3) Loop [for](<#/doc/language/for>)

### Instruções de salto

As instruções de salto transferem incondicionalmente o controle de fluxo.

---
attr-spec-seq(optional)(desde C23) `break` `;` | (1) |
attr-spec-seq(optional)(desde C23) `continue` `;` | (2) |
attr-spec-seq(optional)(desde C23) `return` expression(optional) `;` | (3) |
attr-spec-seq(optional)(desde C23) `goto` identifier `;` | (4) |

1) Instrução [break](<#/doc/language/break>)

2) Instrução [continue](<#/doc/language/continue>)

3) Instrução [return](<#/doc/language/return>) com uma expressão opcional

4) Instrução [goto](<#/doc/language/goto>)

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 6.8 Instruções e blocos (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 6.8 Instruções e blocos (p: 106-112)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 6.8 Instruções e blocos (p: 146-154)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 6.8 Instruções e blocos (p: 131-139)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 3.6 INSTRUÇÕES

### Veja também

[documentação C++](<#/>) para Instruções
---