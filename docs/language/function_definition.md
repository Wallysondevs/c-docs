# Definições de função

Uma definição de função associa o corpo da função (uma sequência de declarações e instruções) ao nome da função e à lista de parâmetros. Ao contrário da [declaração de função](<#/doc/language/function_declaration>), as definições de função são permitidas apenas no escopo de arquivo (não há funções aninhadas).

C suporta duas formas diferentes de definições de função:

---
attr-spec-seq(opcional) specifiers-and-qualifiers parameter-list-declarator function-body | (1) |
specifiers-and-qualifiers identifier-list-declarator declaration-list function-body | (2) | (até C23)

onde

- **attr-spec-seq** — (C23) uma lista opcional de [atributos](<#/doc/language/attributes>), aplicada à função
- **specifiers-and-qualifiers** — uma combinação de
* [especificadores de tipo](<#/doc/language/declarations>) que, possivelmente modificados pelo declarador, formam o _tipo de retorno_
* [especificadores de classe de armazenamento](<#/doc/language/storage_duration>), que determinam a ligação do identificador (`static`, `extern`, ou nenhum)
* especificadores de função [`inline`](<#/doc/language/inline>), [`_Noreturn`](<#/doc/language/_Noreturn>), ou nenhum
- **parameter-list-declarator** — um declarador para um tipo de função que usa uma [lista de parâmetros](<#/doc/language/function_declaration>) para designar parâmetros de função
- **identifier-list-declarator** — um declarador para um tipo de função que usa uma [lista de identificadores](<#/doc/language/function_declaration>) para designar parâmetros de função
- **declaration-list** — sequência de declarações que declaram cada identificador em identifier-list-declarator. Essas declarações não podem usar inicializadores e o único [especificador de classe de armazenamento](<#/doc/language/storage_duration>) permitido é register.
- **function-body** — uma [instrução composta](<#/doc/language/statements>), que é uma sequência de declarações e instruções entre chaves, que é executada sempre que esta função é chamada

1) Definição de função estilo novo (C89). Esta definição tanto introduz a própria função quanto serve como um protótipo de função para quaisquer futuras [expressões de chamada de função](<#/doc/language/operator_other>), forçando conversões de expressões de argumento para os tipos de parâmetro declarados.
```c
    int max(int a, int b)
    {
        return a>b?a:b;
    }
    
    double g(void)
    {
        return 0.1;
    }
```

2) (até C23) Definição de função estilo antigo (K&R). Esta definição não se comporta como um protótipo e quaisquer futuras [expressões de chamada de função](<#/doc/language/operator_other>) realizarão promoções de argumento padrão.
```c
    int max(a, b)
    int a, b;
    {
        return a>b?a:b;
    }
    double g()
    {
        return 0.1;
    }
```

### Explicação

Assim como nas [declarações de função](<#/doc/language/function_declaration>), o tipo de retorno da função, determinado pelo especificador de tipo em specifiers-and-qualifiers e possivelmente modificado pelo declarador como de costume em [declarações](<#/doc/language/declarations>), deve ser um tipo de objeto completo não-array ou o tipo void. Se o tipo de retorno fosse cvr-qualificado, ele é ajustado para sua versão não qualificada para o propósito de construir o tipo de função.
```c
    void f(char *s) { puts(s); } // return type is void
    int sum(int a, int b) { return a+b; } // return type is int
    int (*foo(const void *p))[3] { // return type is pointer to array of 3 int
        return malloc(sizeof(int[3]));
    }
```

Assim como nas [declarações de função](<#/doc/language/function_declaration>), os tipos dos parâmetros são ajustados de funções para ponteiros e de arrays para ponteiros para o propósito de construir o tipo de função e os qualificadores cvr de nível superior de todos os tipos de parâmetro são ignorados para o propósito de determinar [tipo de função compatível](<#/doc/language/compatible_type>).

Ao contrário das [declarações de função](<#/doc/language/function_declaration>), parâmetros formais sem nome não são permitidos (caso contrário, haveria conflitos em definições de função estilo antigo (K&R)), eles devem ser nomeados mesmo que não sejam usados dentro da função. A única exceção é a lista de parâmetros especial (void). | (até C23)
Parâmetros formais podem ser sem nome em definições de função, porque as definições de função estilo antigo (K&R) foram removidas. Parâmetros sem nome são inacessíveis por nome dentro do corpo da função. | (desde C23)
```c
    int f(int, int); // declaration
    // int f(int, int) { return 7; } // Error until C23, OK since C23
    int f(int a, int b) { return 7; } // definition
    int g(void) { return 8; } // OK: void doesn't declare a parameter
```

Dentro do corpo da função, cada parâmetro nomeado é uma expressão [lvalue](<#/doc/language/value_category>), eles têm [duração de armazenamento](<#/doc/language/storage_duration>) automática e [escopo de bloco](<#/doc/language/scope>). O layout dos parâmetros na memória (ou se eles são armazenados na memória) é não especificado: faz parte da [convenção de chamada](<https://en.wikipedia.org/wiki/Calling_convention> "enwiki:Calling convention").
```c
    int main(int ac, char **av)
    {
        ac = 2; // parameters are lvalues
        av = (char *[]){"abc", "def", NULL};
        f(ac, av);
    }
```

Veja [operador de chamada de função](<#/doc/language/operator_other>) para outros detalhes sobre a mecânica de uma chamada de função e [return](<#/doc/language/return>) para retornar de funções.

### __func__

Dentro de cada corpo de função, a variável predefinida especial __func__ com escopo de bloco e duração de armazenamento estática está disponível, como se definida imediatamente após a chave de abertura por
```c
    static const char __func__[] = "function name";
```

Este identificador especial é às vezes usado em combinação com as [constantes de macro predefinidas](<#/doc/preprocessor/replace>) __FILE__ e __LINE__, por exemplo, por [assert](<#/doc/error/assert>). | (desde C99)

### Notas

A lista de argumentos deve estar explicitamente presente no declarador, ela não pode ser herdada de um typedef
```c
    typedef int p(int q, int r); // p is a function type int(int, int)
    p f { return q + r; } // Error
```

Em C89, specifiers-and-qualifiers era opcional, e se omitido, o tipo de retorno da função assumia int por padrão (possivelmente alterado pelo declarador). Além disso, a definição estilo antigo não exigia uma declaração para cada parâmetro em declaration-list. Qualquer parâmetro cuja declaração estivesse faltando tinha o tipo int
```c
    max(a, b) // a and b have type int, return type is int
    {
        return a>b?a:b;
    }
```
| (até C99)

### Relatórios de defeito

Os seguintes relatórios de defeito que alteram o comportamento foram aplicados retroativamente a padrões C publicados anteriormente.

DR | Aplicado a | Comportamento conforme publicado | Comportamento correto
[DR 423](<https://www.open-std.org/jtc1/sc22/wg14/www/docs/n2396.htm#dr_423>) | C89 | o tipo de retorno pode ser qualificado | o tipo de retorno é implicitamente desqualificado

### Referências

* Padrão C17 (ISO/IEC 9899:2018):
* 6.9.1 Definições de função (p: 113-115)
* Padrão C11 (ISO/IEC 9899:2011):
* 6.9.1 Definições de função (p: 156-158)
* Padrão C99 (ISO/IEC 9899:1999):
* 6.9.1 Definições de função (p: 141-143)
* Padrão C89/C90 (ISO/IEC 9899:1990):
* 3.7.1 Definições de função

### Ver também

[Documentação C++](<#/>) para Definição de função
---