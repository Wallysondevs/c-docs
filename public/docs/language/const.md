# qualificador de tipo const

Cada tipo individual no [sistema de tipos](<#/doc/language/compatible_type>) do C possui várias versões _qualificadas_ desse tipo, correspondendo a um, dois ou todos os três qualificadores: `const`, [`volatile`](<#/doc/language/volatile>) e, para ponteiros para tipos de objeto, [`restrict`](<#/doc/language/restrict>). Esta página descreve os efeitos do qualificador `const`.

Objetos [declarados](<#/doc/language/declarations>) com tipos qualificados com `const` podem ser colocados em memória somente leitura pelo compilador, e se o endereço de um objeto `const` nunca for obtido em um programa, ele pode nem ser armazenado.

Qualquer tentativa de modificar um objeto cujo tipo é qualificado com `const` resulta em comportamento indefinido.
```c
    const int n = 1; // objeto de tipo qualificado com const
    int* p = (int*)&n;
    *p = 2; // comportamento indefinido
```

A semântica de `const` se aplica apenas a expressões [lvalue](<#/doc/language/value_category>); sempre que uma expressão lvalue `const` é usada em um contexto que não requer um lvalue, seu qualificador `const` é perdido (note que o qualificador `volatile`, se presente, não é perdido).

As expressões lvalue que designam objetos de tipo qualificado com `const` e as expressões lvalue que designam objetos de tipo `struct` ou `union` com pelo menos um membro de tipo qualificado com `const` (incluindo membros de agregados ou uniões contidos recursivamente), não são _lvalues modificáveis_. Em particular, eles não são atribuíveis:
```c
    const int n = 1; // objeto de tipo const
    n = 2; // erro: o tipo de n é qualificado com const
    
    int x = 2; // objeto de tipo não qualificado
    const int* p = &x;
    *p = 3; // erro: o tipo do lvalue *p é qualificado com const
    
    struct {int a; const int b; } s1 = {.b=1}, s2 = {.b=2};
    s1 = s2; // erro: o tipo de s1 não é qualificado, mas possui um membro const
```

Um membro de um tipo `struct` ou `union` qualificado com `const` adquire a qualificação do tipo ao qual pertence (tanto quando acessado usando o operador `.` quanto o operador `- >`).
```c
    struct s { int i; const int ci; } s;
    // o tipo de s.i é int, o tipo de s.ci é const int
    const struct s cs;
    // os tipos de cs.i e cs.ci são ambos const int
```

| Se um tipo de array é declarado com o qualificador de tipo `const` (através do uso de [typedef](<#/doc/language/typedef>)), o tipo de array não é qualificado com `const`, mas seu tipo de elemento é. | (até C23) |
|---|---|
| Um tipo de array e seu tipo de elemento são sempre considerados identicamente qualificados com `const`. | (desde C23) |
```c
    typedef int A[2][3];
    const A a = {{4, 5, 6}, {7, 8, 9}}; // array de array de const int
    int* pi = a[0]; // Erro: a[0] tem tipo const int*
    void *unqual_ptr = a; // OK até C23; erro desde C23
    // Notas: o clang aplica a regra em C++/C23 mesmo nos modos C89-C17
```

Se um tipo de função é declarado com o qualificador de tipo `const` (através do uso de [typedef](<#/doc/language/typedef>)), o comportamento é indefinido.

Em uma declaração de função, a palavra-chave `const` pode aparecer dentro dos colchetes usados para declarar um tipo de array de um parâmetro de função. Ela qualifica o tipo de ponteiro para o qual o tipo de array é transformado. As duas declarações a seguir declaram a mesma função:
```c
    void f(double x[const], const double y[const]);
    void f(double * const x, const double * const y);
```

| (desde C99) |
|---|
| Literais compostos qualificados com `const` não designam necessariamente objetos distintos; eles podem compartilhar armazenamento com outros literais compostos e com literais de string que por acaso têm a mesma representação ou representação sobreposta. |
```c
    const int* p1 = (const int[]){1, 2, 3};
    const int* p2 = (const int[]){2, 3, 4}; // o valor de p2 pode ser igual a p1+1
    _Bool b = "foobar" + 3 == (const char[]){"bar"}; // o valor de b pode ser 1
```

| (desde C99) |
|---|

Um ponteiro para um tipo não `const` pode ser implicitamente convertido para um ponteiro para a versão qualificada com `const` do mesmo tipo ou de um tipo [compatível](<#/doc/language/compatible_type>). A conversão inversa requer uma expressão de cast.
```c
    int* p = 0;
    const int* cp = p; // OK: adiciona qualificadores (int para const int)
    p = cp; // Erro: descarta qualificadores (const int para int)
    p = (int*)cp; // OK: cast
```

Note que ponteiro para ponteiro para `T` não é conversível para ponteiro para ponteiro para `const T`; para que dois tipos sejam compatíveis, suas qualificações devem ser idênticas.
```c
    char *p = 0;
    const char **cpp = &p; // Erro: char* e const char* não são tipos compatíveis
    char * const *pcp = &p; // OK, adiciona qualificadores (char* para char*const)
```

### Palavras-chave

[`const`](<#/>)

### Notas

O C adotou o qualificador _const_ do C++, mas, diferentemente do C++, expressões de tipo qualificado com `const` em C não são [expressões constantes](<#/doc/language/constant_expression>); elas não podem ser usadas como rótulos de [case](<#/doc/language/switch>) ou para inicializar objetos com duração de armazenamento [static](<#/doc/language/static_storage_duration>) e [thread](<#/doc/language/thread_storage_duration>), [enumeradores](<#/doc/language/enum>) ou tamanhos de [bit-field](<#/doc/language/bit_field>). Quando são usadas como tamanhos de [array](<#/doc/language/array>), os arrays resultantes são VLAs.

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 6.7.3 Qualificadores de tipo (p: 87-90)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 6.7.3 Qualificadores de tipo (p: 121-123)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 6.7.3 Qualificadores de tipo (p: 108-110)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 6.5.3 Qualificadores de tipo

### Veja também

[Documentação C++](<#/>) para qualificadores de tipo cv (`const` e `volatile`)
---