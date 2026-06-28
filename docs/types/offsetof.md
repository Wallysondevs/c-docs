# offsetof

Definido no cabeçalho [`<stddef.h>`](<#/doc/types>)

```c
#define offsetof(type, member) /*implementation-defined*/
```

A macro **offsetof** expande para uma [expressão constante inteira](<#/doc/language/constant_expression>) do tipo [size_t](<#/doc/types/size_t>), cujo valor é o deslocamento, em bytes, do início de um objeto do tipo especificado para seu subobjeto especificado, incluindo preenchimento (padding), se houver.

Dado um objeto `o` do tipo `type` com duração de armazenamento estática, &(o.member) deve ser uma expressão constante de endereço e apontar para um subobjeto de `o`. Caso contrário, o comportamento é indefinido.

Se o nome do tipo especificado em `type` contiver uma vírgula que não esteja entre parênteses correspondentes, o comportamento é indefinido. | (desde C23)

### Notas

Se `offsetof` for aplicado a um membro bit-field, o comportamento é indefinido, porque o endereço de um bit-field não pode ser obtido.

`member` não se restringe a um membro direto. Ele pode denotar um subobjeto de um determinado membro, como um elemento de um membro array.

Embora seja especificado em C23 que especificar um novo tipo contendo uma vírgula não entre parênteses em `offsetof` é comportamento indefinido, tal uso geralmente não é suportado mesmo em modos anteriores: offsetof(struct Foo { int a, b; }, a) geralmente falha na compilação.

`typeof` pode ser usado para evitar o efeito negativo de vírgulas na definição de um novo tipo, por exemplo, offsetof(typeof(struct { int i, j; }), i) é bem definido. | (desde C23)

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <stddef.h>
    
    struct S {
        char c;
        double d;
    };
    
    int main(void)
    {
        printf("the first element is at offset %zu\n", offsetof(struct S, c));
        printf("the double is at offset %zu\n", offsetof(struct S, d));
    }
```

Saída possível:
```
    the first element is at offset 0
    the double is at offset 8
```

### Relatórios de defeito

Os seguintes relatórios de defeito que alteram o comportamento foram aplicados retroativamente a padrões C publicados anteriormente.

DR | Aplicado a | Comportamento publicado | Comportamento correto
[DR 496](<https://www.open-std.org/jtc1/sc22/wg14/www/docs/n2396.htm#dr_496>) | C89 | apenas structs e membros de struct eram mencionados | unions e outros subobjetos também são suportados

### Veja também

[ size_t](<#/doc/types/size_t>) | tipo inteiro sem sinal retornado pelo operador [`sizeof`](<#/doc/language/sizeof>)
(typedef)
[Documentação C++](<#/>) para offsetof