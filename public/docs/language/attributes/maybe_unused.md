# Atributo C: maybe_unused (desde C23)

Suprime avisos sobre entidades não utilizadas.

### Sintaxe

---
`[[` `maybe_unused` `]]`
`[[` `__maybe_unused__` `]]`
---

### Explicação

Este atributo pode aparecer na declaração das seguintes entidades:

  * [struct](<#/doc/language/struct>)/[union](<#/doc/language/union>): struct [[maybe_unused]] S;,
  * [nome de typedef](<#/doc/language/typedef>): [[maybe_unused]] typedef S* PS;,
  * objeto: [[maybe_unused]] int x;,
  * membro de struct/union: union U { [[maybe_unused]] int n; };,
  * [função](<#/doc/language/function_definition>): [[maybe_unused]] void f(void);,
  * [enumeração](<#/doc/language/enum>): enum [[maybe_unused]] E {};,
  * enumerador: enum { A [[maybe_unused]], B [[maybe_unused]] = 42 };.

Se o compilador emitir avisos sobre entidades não utilizadas, esse aviso é suprimido para qualquer entidade declarada `maybe_unused`.

### Exemplo

Execute este código
```
    #include <assert.h>
    
    [[maybe_unused]] void f([[maybe_unused]] _Bool cond1, [[maybe_unused]] _Bool cond2)
    {
       [[maybe_unused]] _Bool b = cond1 && cond2;
       assert(b); // no modo de lançamento, assert é removido na compilação, e b não é utilizado
                  // nenhum aviso porque é declarado [[maybe_unused]]
    } // os parâmetros cond1 e cond2 não são utilizados, nenhum aviso
    
    int main(void)
    {
        f(1, 1);
    }
```

### Veja também

[documentação C++](<#/>) para maybe_unused
---