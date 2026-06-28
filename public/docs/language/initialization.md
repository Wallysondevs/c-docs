# Inicialização

Uma [declaração](<#/doc/language/declarations>) de um objeto pode fornecer seu valor inicial através do processo conhecido como _inicialização_.

Para cada [declarador](<#/doc/language/declarations>), o inicializador, se não for omitido, pode ser um dos seguintes:

---
`=` expression | (1) |
`=` `{` initializer-list `}` | (2) |
`=` `{` `}` | (3) | (desde C23)

onde initializer-list é uma lista não vazia de inicializadores separados por vírgulas (com uma vírgula final opcional), onde cada inicializador tem uma das três formas possíveis:

---
expression | (1) |
`{` initializer-list `}` | (2) |
`{` `}` | (3) | (desde C23)
designator-list `=` initializer | (4) | (desde C99)
onde designator-list é uma lista de designadores de array na forma `[` constant-expression `]` ou designadores de membro de struct/union na forma `.` identifier; veja [inicialização de array](<#/doc/language/array_initialization>) e [inicialização de struct](<#/doc/language/struct_initialization>). Nota: além dos inicializadores, initializer-list entre chaves pode aparecer em [literais compostos](<#/doc/language/compound_literal>), que são expressões da forma: |
---
`(` type `)` `{` initializer-list `}`
`(` type `)` `{` `}` | | (desde C23)
(desde C99)

### Explicação

O inicializador especifica o valor inicial armazenado em um objeto.

#### Inicialização explícita

Se um inicializador for fornecido, veja

  * [inicialização escalar](<#/doc/language/scalar_initialization>) para a inicialização de tipos escalares
  * [inicialização de array](<#/doc/language/array_initialization>) para a inicialização de tipos de array
  * [inicialização de struct](<#/doc/language/struct_initialization>) para a inicialização de tipos struct e union.

#### Inicialização implícita

Se um inicializador não for fornecido:

  * objetos com [duração de armazenamento](<#/doc/language/storage_duration>) automática são inicializados com valores indeterminados (que podem ser [representações de armadilha](<#/doc/language/object>))
  * objetos com [duração de armazenamento](<#/doc/language/storage_duration>) estática e thread-local são inicializados vazios

#### Inicialização vazia

Um objeto é inicializado vazio se for explicitamente inicializado a partir do inicializador = {}. | (desde C23)

Em alguns casos, um objeto é inicializado vazio se não for inicializado explicitamente, ou seja:

  * ponteiros são inicializados com valores de ponteiro nulo de seus tipos
  * objetos de tipos integrais são inicializados com zero sem sinal
  * objetos de tipos de ponto flutuante são inicializados com zero positivo
  * todos os elementos de arrays, todos os membros de structs e os primeiros membros de unions são inicializados vazios, recursivamente, e todos os bits de preenchimento são inicializados com zero

    (em plataformas onde valores de ponteiro nulo e zeros de ponto flutuante têm representações de todos os bits zero, esta forma de inicialização para estáticos é normalmente implementada alocando-os na seção .bss da imagem do programa)

### Notas

Ao inicializar um objeto com [duração de armazenamento](<#/doc/language/storage_duration>) estática ou thread-local, cada expressão no inicializador deve ser uma [expressão constante](<#/doc/language/constant_expression>) ou um [literal de string](<#/doc/language/string_literal>).

Inicializadores não podem ser usados em declarações de objetos de tipo incompleto, VLAs e objetos com escopo de bloco com ligação.

Os valores iniciais dos parâmetros de função são estabelecidos como se por atribuição dos argumentos de uma [chamada de função](<#/doc/language/operator_other>), em vez de por inicialização.

Se um valor indeterminado for usado como argumento para qualquer chamada da biblioteca padrão, o comportamento é indefinido. Caso contrário, o resultado de qualquer expressão envolvendo valores indeterminados é um valor indeterminado (por exemplo, int n;, n pode não ser igual a si mesmo e pode parecer mudar seu valor em leituras subsequentes)

Não há uma construção especial em C correspondente à [inicialização por valor](<#/>) em C++; no entanto, = {0} (ou (T){0} em literais compostos)(desde C99) pode ser usado em vez disso, pois o padrão C não permite structs vazias, unions vazias ou arrays de comprimento zero. | (até C23)
O inicializador vazio = {} (ou (T){} em literais compostos) pode ser usado para alcançar a mesma semântica que a [inicialização por valor](<#/>) em C++. | (desde C23)

### Exemplo

Execute este código
```c
    #include <stdlib.h>
    int a[2]; // inicializa a para {0, 0}
    int main(void)
    {
        int i;          // inicializa i para um valor indeterminado
        static int j;   // inicializa j para 0
        int k = 1;      // inicializa k para 1
    
        // inicializa int x[3] para 1,3,5
        // inicializa int* p para &x[0]
        int x[] = { 1, 3, 5 }, *p = x;
    
        // inicializa w (um array de duas structs) para
        // { { {1,0,0}, 0}, { {2,0,0}, 0} }
        struct {int a[3], b;} w[] = {[0].a = {1}, [1].a[0] = 2};
    
        // expressão de chamada de função pode ser usada para uma variável local
        char* ptr = malloc(10);
        free(ptr);
    
    //  Erro: objetos com duração de armazenamento estática requerem inicializadores constantes
    //  static char* ptr = malloc(10);
    
    //  Erro: VLA não pode ser inicializado
    //  int vla[n] = {0};
    }
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 6.7.9 Inicialização (p: 100-105)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 6.7.9 Inicialização (p: 139-144)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 6.7.8 Inicialização (p: 125-130)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 6.5.7 Inicialização

### Veja também

[documentação C++](<#/>) para Inicialização
---