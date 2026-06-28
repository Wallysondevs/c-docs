# Busca e espaços de nomes

Quando um [identificador](<#/doc/language/identifier>) é encontrado em um programa C, uma busca é realizada para localizar a [declaração](<#/doc/language/declarations>) que introduziu esse identificador e que está atualmente [em escopo](<#/doc/language/scope>). C permite que mais de uma declaração para o mesmo identificador esteja em escopo simultaneamente se esses identificadores pertencerem a diferentes categorias, chamadas _espaços de nomes_ :

1) Espaço de nomes de rótulos: todos os identificadores declarados como [rótulos](<#/doc/language/statements>).

2) Nomes de tags: todos os identificadores declarados como nomes de [structs](<#/doc/language/struct>), [unions](<#/doc/language/union>) e [tipos enumerados](<#/doc/language/enum>). Note que todos os três tipos de tags compartilham um único espaço de nomes.

3) Nomes de membros: todos os identificadores declarados como membros de qualquer [struct](<#/doc/language/struct>) ou [union](<#/doc/language/union>). Cada struct e union introduz seu próprio espaço de nomes desse tipo.

4) Espaço de nomes de atributos globais: [tokens de atributo](<#/doc/language/attributes>) definidos pelo padrão ou prefixos de atributo definidos pela implementação. 5) Nomes de atributos não-padrão: nomes de atributos que seguem prefixos de atributo. Cada prefixo de atributo possui um espaço de nomes separado para os atributos definidos pela implementação que ele introduz. | (desde C23)

6) Todos os outros identificadores, chamados _identificadores comuns_ para distingui-los de (1-5) (nomes de funções, nomes de objetos, nomes de typedef, constantes de enumeração).

No ponto da busca, o espaço de nomes de um identificador é determinado pela maneira como ele é usado:

1) um identificador que aparece como operando de uma [instrução goto](<#/doc/language/goto>) é buscado no espaço de nomes de rótulos.

2) um identificador que segue a palavra-chave struct, union, ou enum é buscado no espaço de nomes de tags.

3) um identificador que segue o operador de [acesso a membro](<#/doc/language/operator_member_access>) ou acesso a membro através de ponteiro é buscado no espaço de nomes de membros do tipo determinado pelo operando esquerdo do operador de acesso a membro.

4) um identificador que aparece diretamente em um especificador de atributo ([[...]]) é buscado no espaço de nomes de atributos globais. 5) um identificador que segue o token :: após um prefixo de atributo é buscado no espaço de nomes introduzido pelo prefixo de atributo. | (desde C23)

6) todos os outros identificadores são buscados no espaço de nomes de identificadores comuns.

### Notas

Os nomes de [macros](<#/doc/preprocessor/replace>) não fazem parte de nenhum espaço de nomes porque são substituídos pelo pré-processador antes da análise semântica.

É prática comum injetar nomes de struct/union/enum no espaço de nomes dos identificadores comuns usando uma declaração [typedef](<#/doc/language/typedef>):
```c
    struct A { };       // introduces the name A in tag name space
    typedef struct A A; // first, lookup for A after "struct" finds one in tag name space
                        // then introduces the name A in the ordinary name space
    struct A* p;        // OK, this A is looked up in the tag name space
    A* q;               // OK, this A is looked up in the ordinary name space
```

Um exemplo bem conhecido do mesmo identificador sendo usado em dois espaços de nomes é o identificador stat do cabeçalho POSIX `sys/stat.h`. Ele [nomeia uma função](<http://pubs.opengroup.org/onlinepubs/9699919799/>) quando usado como um identificador comum e [indica uma struct](<http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/sys_stat.h.html>) quando usado como uma tag.

Ao contrário do C++, as constantes de enumeração não são membros de struct, e seu espaço de nomes é o espaço de nomes dos identificadores comuns, e como não há escopo de struct em C, seu escopo é o escopo no qual a declaração da struct aparece:
```c
    struct tagged_union {
       enum {INT, FLOAT, STRING} type;
       union {
          int integer;
          float floating_point;
          char *string;
       };
    } tu;
     
    tu.type = INT; // OK in C, error in C++
```

Se um atributo padrão, um prefixo de atributo ou um nome de atributo não-padrão não for suportado, o atributo inválido em si é ignorado sem causar um erro. | (desde C23)

### Exemplo

Execute este código
```c
    void foo (void) { return; } // ordinary name space, file scope
    struct foo {      // tag name space, file scope
        int foo;      // member name space for this struct foo, file scope
        enum bar {    // tag name space, file scope
            RED       // ordinary name space, file scope
        } bar;        // member name space for this struct foo, file scope
        struct foo* p; // OK: uses tag/file scope name "foo"
    };
    enum bar x; // OK: uses tag/file-scope bar
    // int foo; // Error: ordinary name space foo already in scope 
    //union foo { int a, b; }; // Error: tag name space foo in scope
     
    int main(void)
    {
        goto foo; // OK uses "foo" from label name space/function scope
     
        struct foo { // tag name space, block scope (hides file scope)
           enum bar x; // OK, uses "bar" from tag name space/file scope
        };
        typedef struct foo foo; // OK: uses foo from tag name space/block scope
                                // defines block-scope ordinary foo (hides file scope)
        (foo){.x=RED}; // uses ordinary/block-scope foo and ordinary/file-scope RED
     
    foo:; // label name space, function scope
    }
```

### Referências

* Padrão C17 (ISO/IEC 9899:2018):

  

* 6.2.3 Espaços de nomes de identificadores (p: 29-30)

* Padrão C11 (ISO/IEC 9899:2011):

  

* 6.2.3 Espaços de nomes de identificadores (p: 37)

* Padrão C99 (ISO/IEC 9899:1999):

  

* 6.2.3 Espaços de nomes de identificadores (p: 31)

* Padrão C89/C90 (ISO/IEC 9899:1990):

  

* 3.1.2.3 Espaços de nomes de identificadores

### Veja também

[Documentação C++](<#/>) para Busca de nomes
---