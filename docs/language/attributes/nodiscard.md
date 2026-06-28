# Atributo C: nodiscard (desde C23)

Se uma função declarada `nodiscard` ou uma função que retorna uma struct/union/enum declarada `nodiscard` por valor for chamada a partir de uma [expressão de valor descartado](<#/doc/language/expressions>) que não seja uma conversão para void, o compilador é encorajado a emitir um aviso.

### Sintaxe

---
`[[` `nodiscard` `]]`
`[[` `__nodiscard__` `]]` | (1) |
`[[` `nodiscard` `(` string-literal `)` `]]`
`[[` `__nodiscard__` `(` string-literal `)` `]]` | (2) |
- **literal de string** — texto que pode ser usado para explicar a justificativa pela qual o resultado não deve ser descartado

### Explicação

Aparece em uma declaração de função, declaração de enumeração ou declaração de struct/union.

Se, a partir de uma [expressão de valor descartado](<#/doc/language/expressions>) que não seja uma conversão para void,

  * uma função declarada `nodiscard` for chamada, ou
  * uma função que retorna uma struct/union/enum declarada `nodiscard` for chamada,

o compilador é encorajado a emitir um aviso.

O literal de string, se especificado, é geralmente incluído nos avisos.

### Exemplo

Execute este código
```c
    struct [[nodiscard]] error_info { int status; /*...*/ };
    struct error_info enable_missile_safety_mode() { /*...*/ return (struct error_info){0}; }
    void launch_missiles() { /*...*/ }
    void test_missiles() {
       enable_missile_safety_mode(); // compiler may warn on discarding a nodiscard value
       launch_missiles();
    }
    struct error_info* foo() { static struct error_info e; /*...*/ return &e; }
    void f1() {
        foo(); // nodiscard type itself is not returned, no warning
    }
    // nodiscard( string-literal ):
    [[nodiscard("PURE FUN")]] int strategic_value(int x, int y) { return x ^ y; }
    
    int main()
    {
        strategic_value(4,2); // compiler may warn on discarding a nodiscard value
        int z = strategic_value(0,0); // OK: return value is not discarded
        return z;
    }
```

Saída possível:
```
    game.cpp:5:4: warning: ignoring return value of function declared with 'nodiscard' attribute
    game.cpp:17:5: warning: ignoring return value of function declared with 'nodiscard' attribute: PURE FUN
```

### Veja também

[Documentação C++](<#/>) para nodiscard
---