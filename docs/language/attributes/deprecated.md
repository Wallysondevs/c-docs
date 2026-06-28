# Atributo C: deprecated (desde C23)

Indica que o nome ou entidade declarada com este atributo está [obsoleta](<https://en.wikipedia.org/wiki/Deprecation> "enwiki:Deprecation"), ou seja, o uso é permitido, mas desencorajado por alguma razão.

### Sintaxe

---
`[[` `deprecated` `]]`
`[[` `__deprecated__` `]]` | (1) |
`[[` `deprecated` `(` string-literal `)` `]]`
`[[` `__deprecated__` `(` string-literal `)` `]]` | (2) |
- **string-literal** — texto que pode ser usado para explicar a razão da obsolescência e/ou para sugerir uma entidade substituta

### Explicação

Indica que o uso do nome ou entidade declarada com este atributo é permitido, mas desencorajado por alguma razão. Compiladores tipicamente emitem avisos sobre tais usos. O string-literal, se especificado, é geralmente incluído nos avisos.

Este atributo é permitido em declarações dos seguintes nomes ou entidades:

*   [struct](<#/doc/language/struct>)/[union](<#/doc/language/union>): struct [[deprecated]] S;,
*   [typedef-name](<#/doc/language/typedef>): [[deprecated]] typedef S* PS;,
*   objetos: [[deprecated]] int x;,
*   membro de struct/union: union U { [[deprecated]] int n; };,
*   [função](<#/doc/language/function_definition>): [[deprecated]] void f(void);,
*   [enumeração](<#/doc/language/enum>): enum [[deprecated]] E {};,
*   enumerador: enum { A [[deprecated]], B [[deprecated]] = 42 };.

Um nome declarado não obsoleto pode ser redeclarado como obsoleto. Um nome declarado obsoleto não pode ser "des-obsoletado" redeclarando-o sem este atributo.

### Exemplo

Execute este código
```c
    #include <stdio.h>
     
    [[deprecated]]
    void TriassicPeriod(void)
    {
        puts("Triassic Period: [251.9 - 208.5] million years ago.");
    }
     
    [[deprecated("Use NeogenePeriod() instead.")]]
    void JurassicPeriod(void)
    {
        puts("Jurassic Period: [201.3 - 152.1] million years ago.");
    }
     
    [[deprecated("Use calcSomethingDifferently(int).")]]
    int calcSomething(int x)
    {
        return x * 2;
    }
     
    int main(void)
    {
        TriassicPeriod();
        JurassicPeriod();
    }
```

Saída possível:
```
    Triassic Period: [251.9 - 208.5] million years ago.
    Jurassic Period: [201.3 - 152.1] million years ago.
     
    prog.c:23:5: warning: 'TriassicPeriod' is deprecated [-Wdeprecated-declarations]
        TriassicPeriod();
        ^
    prog.c:3:3: note: 'TriassicPeriod' has been explicitly marked deprecated here
    [[deprecated]]
      ^
    prog.c:24:5: warning: 'JurassicPeriod' is deprecated: Use NeogenePeriod() instead. [-Wdeprecated-declarations]
        JurassicPeriod();
        ^
    prog.c:9:3: note: 'JurassicPeriod' has been explicitly marked deprecated here
    [[deprecated("Use NeogenePeriod() instead.")]]
      ^
    2 warnings generated.
```

### Veja também

[Documentação C++](<#/>) para deprecated
---