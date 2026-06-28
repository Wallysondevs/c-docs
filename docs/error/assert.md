# assert

Definido no cabeçalho [`<assert.h>`](<#/doc/error>)

```c
#ifdef NDEBUG
#define assert(condition) ((void)0)
#else
#define assert(condition) /*implementation defined*/
#endif  // até C23
#ifdef NDEBUG
#define assert(...) ((void)0)
#else
#define assert(...) /*implementation defined*/
#endif  // desde C23
```

  
A definição da macro `assert` depende de outra macro, NDEBUG, que não é definida pela biblioteca padrão.

Se NDEBUG for definida como um nome de macro no ponto do código-fonte onde [`<assert.h>`](<#/doc/error>) é incluído, então `assert` não faz nada.

Se NDEBUG não for definida, então `assert` verifica se seu argumento(até C23)a expressão sintetizada de __VA_ARGS__(desde C23) (que deve ter tipo escalar, caso contrário, o comportamento é indefinido) compara igual a zero. Se for o caso, `assert` exibe informações de diagnóstico específicas da implementação na saída de erro padrão e chama [abort](<#/doc/program/abort>)(). As informações de diagnóstico devem incluir o texto da `expression`, bem como os valores da [variável predefinida](<#/doc/language/function_definition>) __func__ e(desde C99) das [macros predefinidas](<#/doc/preprocessor/replace>) __FILE__ e __LINE__.

### Parâmetros

condition  |  \-  |  expressão de tipo escalar   
  
### Valor de retorno

(nenhum)

### Notas

Não há uma interface padronizada para adicionar uma mensagem adicional aos erros de `assert`. Uma maneira portátil de incluir uma é usar um [operador vírgula](<#/doc/language/operator_other>), ou usar && com um literal de string:
```c
    assert(("There are five lights", 2 + 2 == 5));
    assert(2 + 2 == 5 && "There are five lights");
```

A implementação de `assert` no [Microsoft CRT](<https://learn.microsoft.com/en-us/cpp/c-runtime-library/reference/assert-macro-assert-wassert>) não está em conformidade com C99 e revisões posteriores, porque sua função subjacente (`_wassert`) não aceita nem __func__ nem um substituto equivalente.

Embora a mudança de `assert` em C23 ([N2829](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2829.htm>)) não seja um relatório formal de defeito, o comitê C [recomenda](<https://www.open-std.org/jtc1/sc22/wg14/www/previous.html>) que as implementações retroportem a mudança para modos antigos.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    // uncomment to disable assert()
    // #define NDEBUG
    #include <assert.h>
    #include <math.h>
     
    #define TEST(...) __VA_ARGS__
     
    int main(void)
    {
        double x = -1.0;
        assert(x >= 0.0);
        printf("sqrt(x) = %f\n", sqrt(x));
     
        assert(TEST(x >= 0.0));
     
        return 0;
    }
```

Saída possível:
```
    --- Output with NDEBUG not defined: ---
    a.out: main.cpp:10: main: Assertion `x >= 0.0' failed.
     
    --- Output with NDEBUG defined: ---
    sqrt(x) = -nan
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.2.2.1 A macro assert (p: 196) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.2.1.1 A macro assert (p: 135) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.2.1.1 A macro assert (p: 186-187) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.2.1.1 A macro assert (p: 169) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.2.1.1 A macro assert 

### Veja também

[ abort](<#/doc/program/abort>) |  causa a terminação anormal do programa (sem limpeza)   
(função)  
[Documentação C++](<#/>) para assert