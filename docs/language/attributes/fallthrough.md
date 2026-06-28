# Atributo C: fallthrough (desde C23)

Indica que o fallthrough do rótulo `case` anterior é intencional e não deve ser diagnosticado por um compilador que avisa sobre fallthrough.

### Sintaxe

---
`[[` `fallthrough` `]]`
`[[` `__fallthrough__` `]]`

### Explicação

Pode ser usado apenas em uma [declaração de atributo](<#/doc/language/declarations>) para criar uma _declaração de fallthrough_ ([[fallthrough]];).

Uma declaração de fallthrough pode ser usada apenas em uma instrução [`switch`](<#/doc/language/switch>), onde o próximo item de bloco (instrução, declaração ou rótulo) a ser encontrado é uma instrução com um rótulo `case` ou `default` para essa instrução switch.

Indica que o fallthrough do rótulo `case` anterior é intencional e não deve ser diagnosticado por um compilador que avisa sobre fallthrough.

### Exemplo

Execute este código
```c
    #include <stdbool.h>
     
    void g(void) {}
    void h(void) {}
    void i(void) {}
     
    void f(int n) {
      switch (n) {
        case 1:
        case 2:
          g();
         [[fallthrough]];
        case 3: // sem aviso sobre fallthrough
          h();
        case 4: // o compilador pode avisar sobre fallthrough
          if(n < 3) {
              i();
              [[fallthrough]]; // OK
          }
          else {
              return;
          }
        case 5:
          while (false) {
            [[fallthrough]]; // malformado: nenhum rótulo case ou default subsequente
          }
        case 6:
          [[fallthrough]]; // malformado: nenhum rótulo case ou default subsequente
      }
    }
     
    int main(void) {}
```

### Veja também

[Documentação C++](<#/>) para fallthrough
---