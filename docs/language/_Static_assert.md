# Asserção estática (desde C11)

### Sintaxe  
  
---  
`_Static_assert` `(` expression `,` message `)` |  |  (desde C11)(obsoleto em C23)  
`static_assert` `(` expression `,` message `)` |  |  (desde C23)  
`_Static_assert` `(` expression `)` |  |  (desde C23)(obsoleto em C23)  
`static_assert` `(` expression `)` |  |  (desde C23)  
expression |  \-  |  qualquer [expressão constante inteira](<#/doc/language/constant_expression>)  
message |  \-  |  qualquer [literal de string](<#/doc/language/string_literal>)  
Esta palavra-chave também está disponível como uma macro de conveniência [`static_assert`](<#/doc/error/static_assert>), disponível no cabeçalho [`<assert.h>`](<#/doc/error>).  | (ate C23)  
Ambos `static_assert` e `_Static_assert` têm os mesmos efeitos. `_Static_assert` é uma grafia obsoleta que é mantida para compatibilidade. Uma implementação também pode definir `static_assert` e/ou `_Static_assert` como macros predefinidas, e `static_assert` não é mais fornecido por [`<assert.h>`](<#/doc/error>).  | (desde C23)  
  
### Explicação

A expressão constante é avaliada em tempo de compilação e comparada a zero. Se for igual a zero, ocorre um erro em tempo de compilação e o compilador deve exibir a mensagem como parte da mensagem de erro (exceto que caracteres que não estão no [conjunto de caracteres básico](<#/doc/language/charset>) não são obrigados a serem exibidos)(ate C23)deve exibir a mensagem (se fornecida) como parte da mensagem de erro(desde C23). 

Caso contrário, se a expressão não for igual a zero, nada acontece; nenhum código é emitido. 

### Palavras-chave

[`_Static_assert`](<#/doc/keyword/_Static_assert>), [`static_assert`](<#/doc/keyword/static_assert>)

### Exemplo

Execute este código
```c
    #include <assert.h> // não é mais necessário desde C23
     
    int main(void)
    {
        // Testa se a matemática funciona, C23:
        static_assert((2 + 2) % 3 == 1, "Whoa dude, you knew!");
        // Alternativa pré-C23:
        _Static_assert(2 + 2 * 2 == 6, "Lucky guess!?");
     
        // Isso produzirá um erro em tempo de compilação.
        // static_assert(sizeof(int) < sizeof(char), "Unmet condition!");
     
        constexpr int _42 = 2 * 3 * 2 * 3 + 2 * 3;
        static_assert(_42 == 42); // a string da mensagem pode ser omitida.
     
        // const int _13 = 13;
        // Erro em tempo de compilação - não é uma expressão constante inteira:
        // static_assert(_13 == 13);
    }
```

### Referências

  * C23 standard (ISO/IEC 9899:2024): 

    

  * 6.7.11 Asserções estáticas (p: TBD) 

  * C17 standard (ISO/IEC 9899:2018): 

    

  * 6.7.10 Asserções estáticas (p: 105) 

    

  * 7.2 Diagnósticos <assert.h> (p: 135) 

  * C11 standard (ISO/IEC 9899:2011): 

    

  * 6.7.10 Asserções estáticas (p: 145) 

    

  * 7.2 Diagnósticos <assert.h> (p: 186-187) 

### Veja também

[ assert](<#/doc/error/assert>) |  aborta o programa se a condição especificada pelo usuário não for verdadeira. Pode ser desabilitado para compilações de lançamento   
(macro de função)  
[C++ documentation](<#/>) para a declaração de `static_assert`