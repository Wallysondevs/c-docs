# Tempo de Vida

Todo [objeto](<#/doc/language/object>) em C existe, possui um endereço constante, retém seu último valor armazenado (exceto quando o valor é indeterminado) e, para VLAs, retém seu tamanho (desde C99) durante uma porção da execução do programa conhecida como o _tempo de vida_ deste objeto.

Para os objetos que são declarados com duração de armazenamento automática, estática e de thread, o tempo de vida é igual à sua [duração de armazenamento](<#/doc/language/storage_duration>) (observe a diferença entre duração de armazenamento automática para não-VLA e VLA).

Para os objetos com duração de armazenamento alocada, o tempo de vida começa quando a função de alocação retorna (incluindo o retorno de [realloc](<#/doc/memory/realloc>)) e termina quando a função [realloc](<#/doc/memory/realloc>) ou de desalocação é chamada. Observe que, como objetos alocados não possuem [tipo declarado](<#/doc/language/object>), o tipo da expressão lvalue usada pela primeira vez para acessar este objeto torna-se seu [tipo efetivo](<#/doc/language/object>).

Acessar um objeto fora de seu tempo de vida é comportamento indefinido.
```c
    int* foo(void) {
        int a = 17; // a tem duração de armazenamento automática
        return &a;
    }  // tempo de vida de a termina
    int main(void) {
        int* p = foo(); // p aponta para um objeto cujo tempo de vida já terminou ("ponteiro pendente")
        int n = *p; // comportamento indefinido
    }
```

Um ponteiro para um objeto (ou um além do objeto) cujo tempo de vida terminou possui valor indeterminado.

### Tempo de vida temporário

Objetos de struct e union com membros de array (diretos ou membros de membros de struct/union aninhados) que são designados por [expressões não-lvalue](<#/doc/language/value_category>), possuem _tempo de vida temporário_. O tempo de vida temporário começa quando a expressão que se refere a tal objeto é avaliada e termina no próximo [ponto de sequência](<#/doc/language/eval_order>) (ate C11) quando a expressão completa ou o declarador completo contendo-o termina (desde C11).

Qualquer tentativa de modificar um objeto com tempo de vida temporário resulta em comportamento indefinido.
```c
    struct T { double a[4]; };
    struct T f(void) { return (struct T){3.15}; }
    double g1(double* x) { return *x; }
    void g2(double* x) { *x = 1.0; }
    int main(void)
    {
        double d = g1(f().a); // C99: Comportamento Indefinido (UB) acesso a a[0] em g1 cujo tempo de vida terminou
                              //      no ponto de sequência no início de g1
                              // C11: OK, d é 3.15
        g2(f().a); // C99: Comportamento Indefinido (UB) modificação de a[0] cujo tempo de vida terminou no ponto de sequência
                   // C11: Comportamento Indefinido (UB) tentativa de modificar um objeto temporário
    }
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 6.2.4 Duração de armazenamento de objetos (p: 30) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 6.2.4 Duração de armazenamento de objetos (p: 38-39) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 6.2.4 Duração de armazenamento de objetos (p: 32) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 3.1.2.4 Duração de armazenamento de objetos 

### Veja também

[Documentação C++](<#/>) para Tempo de vida de objeto  
---