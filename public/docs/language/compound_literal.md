# Literais compostos (desde C99)

Constrói um objeto sem nome do tipo especificado (que pode ser um tipo struct, union ou até mesmo array) no local.

### Sintaxe

---
`(` storage-class-specifiers (opcional)(desde C23) type `)` `{` initializer-list `}` | | (desde C99)
`(` storage-class-specifiers (opcional)(desde C23) type `)` `{` initializer-list `,` `}` | | (desde C99)
`(` storage-class-specifiers (opcional) type `)` `{` `}` | | (desde C23)

onde

- **storage-class-specifiers** — (desde C23) Uma lista de [especificadores de classe de armazenamento](<#/doc/language/storage_duration>) que pode conter apenas constexpr, static, register, ou [thread_local](<#/doc/thread/thread_local>)
- **type** — um [nome de tipo](<#/doc/language/compatible_type>) especificando qualquer tipo de objeto completo ou um array de tamanho desconhecido, mas não um VLA
- **initializer-list** — lista de inicializadores adequados para [inicialização](<#/doc/language/initialization>) de um objeto do tipo

### Explicação

A expressão de literal composto constrói um objeto sem nome do tipo especificado por type e o inicializa conforme especificado por initializer-list. [Inicializadores designados](<#/doc/language/initialization>) são aceitos.

O tipo do literal composto é type (exceto quando type é um array de tamanho desconhecido; seu tamanho é deduzido da initializer-list como na [inicialização de array](<#/doc/language/array_initialization>)).

A categoria de valor de um literal composto é [lvalue](<#/doc/language/value_category>) (seu endereço pode ser obtido).

O objeto sem nome ao qual o literal composto avalia tem [duração de armazenamento](<#/doc/language/storage_duration>) estática se o literal composto ocorrer no escopo de arquivo e [duração de armazenamento](<#/doc/language/storage_duration>) automática se o literal composto ocorrer no escopo de bloco (nesse caso, a [vida útil](<#/doc/language/lifetime>) do objeto termina no final do bloco envolvente). | (até C23)
Se o literal composto for avaliado fora do corpo de uma função e fora de qualquer lista de parâmetros, ele é associado ao escopo de arquivo; caso contrário, ele é associado ao bloco envolvente. Dependendo dessa associação, os especificadores de classe de armazenamento (possivelmente vazios), o nome do tipo e a lista de inicializadores, se houver, devem ser tais que sejam especificadores válidos para uma definição de objeto no escopo de arquivo ou escopo de bloco, respectivamente, da seguinte forma,
```c
       storage-class-specifiers typeof(type) ID = { initializer-list };
```

onde ID é um identificador que é único para todo o programa. Um literal composto fornece um objeto sem nome cujo valor, tipo, duração de armazenamento e outras propriedades são como se dados pela sintaxe de definição acima; se a duração de armazenamento for automática, a vida útil da instância do objeto sem nome é a execução atual do bloco envolvente. Se os especificadores de classe de armazenamento contiverem outros especificadores além de constexpr, static, register, ou [thread_local](<#/doc/thread/thread_local>), o comportamento é indefinido. | (desde C23)

### Notas

Literais compostos de tipos de array de caracteres ou caracteres largos qualificados com const podem compartilhar armazenamento com [literais de string](<#/doc/language/string_literal>).
```c
    (const char []){"abc"} == "abc" // pode ser 1 ou 0, não especificado
```

Cada literal composto cria apenas um único objeto em seu escopo:
```c
    int f (void)
    {
        struct s {int i;} *p = 0, *q;
        int j = 0;
    again:
        q = p, p = &((struct s){ j++ });
        if (j < 2) goto again; // nota; se um loop fosse usado, ele terminaria o escopo aqui,
                               // o que encerraria a vida útil do literal composto
                               // deixando p como um ponteiro pendente
        return p == q && q->i == 1; // sempre retorna 1
    }
```

Como os literais compostos não têm nome, um literal composto não pode referenciar a si mesmo (uma struct nomeada pode incluir um ponteiro para si mesma)

Embora a sintaxe de um literal composto seja semelhante a um [cast](<#/doc/language/cast>), a distinção importante é que um cast é uma expressão não-lvalue, enquanto um literal composto é um lvalue.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    
    int *p = (int[]){2, 4}; // cria um array estático sem nome do tipo int[2]
                            // inicializa o array com os valores {2, 4}
                            // cria o ponteiro p para apontar para o primeiro elemento do
                            // array
    const float *pc = (const float []){1e0, 1e1, 1e2}; // literal composto somente leitura
    
    struct point {double x,y;};
    
    int main(void)
    {
        int n = 2, *p = &n;
        p = (int [2]){*p}; // cria um array automático sem nome do tipo int[2]
                           // inicializa o primeiro elemento com o valor anteriormente
                           // contido em *p
                           // inicializa o segundo elemento com zero
                           // armazena o endereço do primeiro elemento em p
    
        void drawline1(struct point from, struct point to);
        void drawline2(struct point *from, struct point *to);
        drawline1(
            (struct point){.x=1, .y=1},  // cria duas structs com escopo de bloco e
            (struct point){.x=3, .y=4}); // chama drawline1, passando-as por valor
        drawline2(
            &(struct point){.x=1, .y=1},  // cria duas structs com escopo de bloco e
            &(struct point){.x=3, .y=4}); // chama drawline2, passando seus endereços
    }
    
    void drawline1(struct point from, struct point to)
    {
        printf("drawline1: `from` @ %p {%.2f, %.2f}, `to` @ %p {%.2f, %.2f}\n",
            (void*)&from, from.x, from.y, (void*)&to, to.x, to.y);
    }
    
    void drawline2(struct point *from, struct point *to)
    {
        printf("drawline2: `from` @ %p {%.2f, %.2f}, `to` @ %p {%.2f, %.2f}\n",
            (void*)from, from->x, from->y, (void*)to, to->x, to->y);
    }
```

Saída possível:
```
    drawline1: `from` @ 0x7ffd24facea0 {1.00, 1.00}, `to` @ 0x7ffd24face90 {3.00, 4.00}
    drawline2: `from` @ 0x7ffd24facec0 {1.00, 1.00}, `to` @ 0x7ffd24faced0 {3.00, 4.00}
```

### Referências

* Padrão C23 (ISO/IEC 9899:2024):

  * 6.5.2.5 Literais compostos (p: A definir)

* Padrão C17 (ISO/IEC 9899:2018):

  * 6.5.2.5 Literais compostos (p: 61-63)

* Padrão C11 (ISO/IEC 9899:2011):

  * 6.5.2.5 Literais compostos (p: 85-87)

* Padrão C99 (ISO/IEC 9899:1999):

  * 6.5.2.5 Literais compostos (p: 75-77)