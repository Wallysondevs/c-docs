# Objetos e alinhamento

Programas C criam, destroem, acessam e manipulam objetos.

Um objeto em C é uma região de [armazenamento de dados](<#/doc/language/memory_model>) no ambiente de execução, cujo conteúdo pode representar _valores_ (um valor é o significado do conteúdo de um objeto, quando interpretado como tendo um [tipo](<#/doc/language/compatible_type>) específico).

Todo objeto possui

*   tamanho (pode ser determinado com [`sizeof`](<#/doc/language/sizeof>))
*   requisito de alinhamento (pode ser determinado por [`_Alignof`](<#/doc/language/alignof>)(até C23)[`alignof`](<#/doc/language/alignof>)(desde C23))(desde C11)
*   [duração de armazenamento](<#/doc/language/storage_duration>) (automática, estática, alocada, thread-local)
*   [tempo de vida](<#/doc/language/lifetime>) (igual à duração de armazenamento ou temporário)
*   tipo efetivo (veja abaixo)
*   valor (que pode ser indeterminado)
*   opcionalmente, um [identificador](<#/doc/language/identifier>) que denota este objeto.

Objetos são criados por [declarações](<#/doc/language/declarations>), [funções de alocação](<#/doc/memory>), [literais de string](<#/doc/language/string_literal>), [literais compostos](<#/doc/language/compound_literal>), e por expressões não-lvalue que retornam [estruturas ou uniões com membros de array](<#/doc/language/lifetime>).

### Representação de objeto

Exceto por [campos de bits](<#/doc/language/bit_field>), objetos são compostos por sequências contíguas de um ou mais bytes, cada um consistindo de [CHAR_BIT](<#/doc/types/limits>) bits, e podem ser copiados com [memcpy](<#/doc/string/byte/memcpy>) para um objeto do tipo unsigned char[n], onde `n` é o tamanho do objeto. O conteúdo do array resultante é conhecido como _representação de objeto_.

Se dois objetos têm a mesma representação de objeto, eles se comparam como iguais (exceto se forem NaNs de ponto flutuante). O inverso não é verdadeiro: dois objetos que se comparam como iguais podem ter representações de objeto diferentes porque nem todo bit da representação de objeto precisa participar do valor. Tais bits podem ser usados para preenchimento para satisfazer o requisito de alinhamento, para verificações de paridade, para indicar representações de armadilha (trap representations), etc.

Se uma representação de objeto não representa nenhum valor do tipo de objeto, ela é conhecida como _representação de armadilha_ (trap representation). Acessar uma representação de armadilha de qualquer forma que não seja lendo-a através de uma expressão lvalue de tipo caractere é comportamento indefinido. O valor de uma estrutura ou união nunca é uma representação de armadilha, mesmo que qualquer membro particular seja uma.

Para objetos do tipo char, signed char e unsigned char, cada bit da representação de objeto é exigido para participar da representação de valor e cada padrão de bits possível representa um valor distinto (nenhum preenchimento, bits de armadilha ou múltiplas representações permitidos).

Quando objetos de [tipos inteiros](<#/doc/language/arithmetic_types>) (short, int, long, long long) ocupam múltiplos bytes, o uso desses bytes é definido pela implementação, mas as duas implementações dominantes são _big-endian_ (POWER, Sparc, Itanium) e _little-endian_ (x86, x86_64): uma plataforma big-endian armazena o byte mais significativo no endereço mais baixo da região de armazenamento ocupada pelo inteiro, uma plataforma little-endian armazena o byte menos significativo no endereço mais baixo. Veja [Endianness](<https://en.wikipedia.org/wiki/Endianness> "enwiki:Endianness") para detalhes. Veja também o exemplo abaixo.

Embora a maioria das implementações não permita representações de armadilha, bits de preenchimento ou múltiplas representações para tipos inteiros, existem exceções; por exemplo, um valor de um tipo inteiro em Itanium [pode ser uma representação de armadilha](<https://web.archive.org/web/20170830125905/https://blogs.msdn.microsoft.com/oldnewthing/20040119-00/?p=41003>).

### Tipo efetivo

Todo objeto tem um _tipo efetivo_, que determina quais acessos [lvalue](<#/doc/language/value_category>) são válidos e quais violam as regras de aliasing estrito.

Se o objeto foi criado por uma [declaração](<#/doc/language/declarations>), o tipo declarado desse objeto é o _tipo efetivo_ do objeto.

Se o objeto foi criado por uma [função de alocação](<#/doc/memory>) (incluindo [realloc](<#/doc/memory/realloc>)), ele não tem tipo declarado. Tal objeto adquire um tipo efetivo da seguinte forma:

*   A primeira escrita nesse objeto através de um lvalue que tem um tipo diferente de tipo caractere, momento em que o tipo desse lvalue se torna o _tipo efetivo_ deste objeto para essa escrita e todas as leituras subsequentes.
*   [memcpy](<#/doc/string/byte/memcpy>) ou [memmove](<#/doc/string/byte/memmove>) copiam outro objeto para esse objeto, ou copiam outro objeto para esse objeto como um array de tipo caractere, momento em que o tipo efetivo do objeto de origem (se ele tivesse um) se torna o tipo efetivo deste objeto para essa escrita e todas as leituras subsequentes.
*   Qualquer outro acesso ao objeto sem tipo declarado, o tipo efetivo é o tipo do lvalue usado para o acesso.

### Aliasing estrito

Dado um objeto com _tipo efetivo_ T1, usar uma expressão lvalue (tipicamente, desreferenciar um ponteiro) de um tipo diferente T2 é comportamento indefinido, a menos que:

*   T2 e T1 são [tipos compatíveis](<#/doc/language/compatible_type>).
*   T2 é uma versão cvr-qualified de um tipo que é [compatível](<#/doc/language/compatible_type>) com T1.
*   T2 é uma versão signed ou unsigned de um tipo que é [compatível](<#/doc/language/compatible_type>) com T1.
*   T2 é um tipo agregado ou tipo união que inclui um dos tipos mencionados entre seus membros (incluindo, recursivamente, um membro de um subagregado ou união contida).
*   T2 é um tipo caractere (char, signed char, ou unsigned char).

```c
    int i = 7;
    char* pc = (char*)(&i);
    
    if (pc[0] == '\x7') // aliasing through char is OK
        puts("This system is little-endian");
    else
        puts("This system is big-endian");
    
    float* pf = (float*)(&i);
    float d = *pf; // UB: float lvalue *p cannot be used to access int
```

Essas regras controlam se, ao compilar uma função que recebe dois ponteiros, o compilador deve emitir código que releia um após escrever através do outro:
```c
    // int* and double* cannot alias
    void f1(int* pi, double* pd, double d)
    {
        // the read from *pi can be done only once, before the loop
        for (int i = 0; i < *pi; i++)
            *pd++ = d;
    }
```
```c
    struct S { int a, b; };
    
    // int* and struct S* may alias because S is an aggregate type with a member of type int
    void f2(int* pi, struct S* ps, struct S s)
    {
        // read from *pi must take place after every write through *ps
        for (int i = 0; i < *pi; i++)
            *ps++ = s;
    }
```

Note que o [qualificador restrict](<#/doc/language/restrict>) pode ser usado para indicar que dois ponteiros não fazem aliasing mesmo que as regras acima permitam que o façam.

Note que o type-punning também pode ser realizado através do membro inativo de uma [union](<#/doc/language/union>).

### Alinhamento

Todo [tipo de objeto](<#/doc/language/types>) completo possui uma propriedade chamada _requisito de alinhamento_, que é um valor inteiro do tipo [size_t](<#/doc/types/size_t>) representando o número de bytes entre endereços sucessivos nos quais objetos deste tipo podem ser alocados. Os valores de alinhamento válidos são potências integrais não negativas de dois.

O requisito de alinhamento de um tipo pode ser consultado com [`_Alignof`](<#/doc/language/alignof>)(até C23)[`alignof`](<#/doc/language/alignof>)(desde C23). | (desde C11)

A fim de satisfazer os requisitos de alinhamento de todos os membros de uma struct, preenchimento (padding) pode ser inserido após alguns de seus membros.

Execute este código
```c
    #include <stdalign.h>
    #include <stdio.h>
    
    // objects of struct S can be allocated at any address
    // because both S.a and S.b can be allocated at any address
    struct S
    {
        char a; // size: 1, alignment: 1
        char b; // size: 1, alignment: 1
    }; // size: 2, alignment: 1
    
    // objects of struct X must be allocated at 4-byte boundaries
    // because X.n must be allocated at 4-byte boundaries
    // because int's alignment requirement is (usually) 4
    struct X
    {
        int n;  // size: 4, alignment: 4
        char c; // size: 1, alignment: 1
        // three bytes padding
    }; // size: 8, alignment: 4
    
    int main(void)
    {
        printf("sizeof(struct S) = %zu\n", sizeof(struct S));
        printf("alignof(struct S) = %zu\n", alignof(struct S));
        printf("sizeof(struct X) = %zu\n", sizeof(struct X));
        printf("alignof(struct X) = %zu\n", alignof(struct X));
    }
```

Saída possível:
```c
    sizeof(struct S) = 2
    alignof(struct S) = 1
    sizeof(struct X) = 8
    alignof(struct X) = 4
```

Cada tipo de objeto impõe seu requisito de alinhamento a todo objeto desse tipo. O alinhamento mais fraco (menor) é o alinhamento dos tipos char, signed char e unsigned char, e é igual a 1. O _alinhamento fundamental_ mais estrito (maior) de qualquer tipo é definido pela implementação e igual ao alinhamento de [max_align_t](<#/doc/types/max_align_t>)(desde C11).

Alinhamentos fundamentais são suportados para objetos de todos os tipos de durações de armazenamento.

Se o alinhamento de um objeto é tornado mais estrito (maior) do que [max_align_t](<#/doc/types/max_align_t>) usando [`_Alignof`](<#/doc/language/alignof>)(até C23)[`alignof`](<#/doc/language/alignof>)(desde C23), ele tem um _requisito de alinhamento estendido_. Um tipo struct ou union cujo membro tem alinhamento estendido é um _tipo super-alinhado_ (over-aligned type). É definido pela implementação se tipos super-alinhados são suportados, e seu suporte pode ser diferente em cada tipo de [duração de armazenamento](<#/doc/language/storage_duration>). Se um tipo struct ou union `S` não tem nenhum membro de um tipo super-alinhado ou declarado com um especificador de alinhamento que especifica um alinhamento estendido, `S` tem um alinhamento fundamental. A versão [atomic](<#/doc/language/atomic>) de todo tipo [aritmético](<#/doc/language/arithmetic_types>) ou [ponteiro](<#/doc/language/pointer>) tem um alinhamento fundamental. | (desde C11)

### Relatórios de defeitos

Os seguintes relatórios de defeitos que alteram o comportamento foram aplicados retroativamente a padrões C publicados anteriormente.

DR | Aplicado a | Comportamento conforme publicado | Comportamento correto
[DR 445](<https://www.open-std.org/jtc1/sc22/wg14/www/docs/n2396.htm#dr_445>) | C11 | um tipo poderia ter alinhamento estendido sem _Alignas envolvido | ele deve ter alinhamento fundamental

### Referências

*   Padrão C17 (ISO/IEC 9899:2018):
    *   3.15 objeto (p: 5)
    *   6.2.6 Representações de tipos (p: 33-35)
    *   6.2.8 Alinhamento de objetos (p: 36-37)
    *   6.5/6-7 Expressões (p: 55-56)
*   Padrão C11 (ISO/IEC 9899:2011):
    *   3.15 objeto (p: 6)
    *   6.2.6 Representações de tipos (p: 44-46)
    *   6.2.8 Alinhamento de objetos (p: 48-49)
    *   6.5/6-7 Expressões (p: 77)
*   Padrão C99 (ISO/IEC 9899:1999):
    *   3.2 alinhamento (p: 3)
    *   3.14 objeto (p: 5)
    *   6.2.6 Representações de tipos (p: 37-39)
    *   6.5/6-7 Expressões (p: 67-68)
*   Padrão C89/C90 (ISO/IEC 9899:1990):
    *   1.6 Definições de termos

### Veja também

[Documentação C++](<#/>) para Objeto