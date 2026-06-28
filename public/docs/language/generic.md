# Seleção genérica (desde C11)

Fornece uma maneira de escolher uma das várias expressões em tempo de compilação, com base no tipo de uma expressão controladora
  
### Sintaxe
  
---  
`_Generic` `(` controlling-expression `,` association-list `)` | | (desde C11)  
  
onde association-list é uma lista de associações separadas por vírgulas, cada uma das quais tem a sintaxe
  
---  
type-name `:` expression
`default` `:` expression
  
onde 

- **type-name** — qualquer [tipo de objeto](<#/doc/language/compatible_type>) completo que não seja de modificação variável (ou seja, não VLA ou ponteiro para VLA).
- **controlling-expression** — qualquer expressão (exceto para o [operador vírgula](<#/doc/language/operator_other>)) cujo tipo deve ser compatível com um dos type-names se a associação default não for usada
- **expression** — qualquer expressão (exceto para o [operador vírgula](<#/doc/language/operator_other>)) de qualquer tipo e categoria de valor
  
Nenhum dos dois type-names na association-list pode especificar [tipos compatíveis](<#/doc/language/compatible_type>). Pode haver apenas uma associação que usa a palavra-chave default. Se default não for usado e nenhum dos type-names for compatível com o tipo da expressão controladora, o programa não será compilado.

### Explicação

Primeiro, o tipo da controlling-expression passa por [conversões lvalue](<#/doc/language/conversion>). A conversão é realizada apenas no domínio do tipo: ela descarta os qualificadores cvr de nível superior e a atomicidade e aplica transformações de array-para-ponteiro/função-para-ponteiro ao tipo da expressão controladora, sem iniciar quaisquer efeitos colaterais ou calcular quaisquer valores.

O tipo após a conversão é comparado com os type-names da lista de associações.

Se o tipo for [compatível](<#/doc/language/compatible_type>) com o type-name de uma das associações, então o tipo, valor e [categoria de valor](<#/doc/language/value_category>) da seleção genérica são o tipo, valor e categoria de valor da expressão que aparece após os dois pontos para aquele type-name.

Se nenhum dos type-names for compatível com o tipo da controlling-expression, e a associação default for fornecida, então o tipo, valor e categoria de valor da seleção genérica são o tipo, valor e categoria de valor da expressão após o rótulo `default :`.

### Notas

A controlling-expression e as expressões das seleções que não são escolhidas nunca são avaliadas.

Devido às conversões lvalue, "abc" corresponde a char* e não a char[4] e (int const){0} corresponde a int, e não a const int.

Todas as [categorias de valor](<#/doc/language/value_category>), incluindo designadores de função e expressões void, são permitidas como expressões em uma seleção genérica, e se selecionada, a própria seleção genérica tem a mesma categoria de valor.

As [macros matemáticas genéricas por tipo](<#/doc/numeric/tgmath>) de [`<tgmath.h>`](<#/doc/numeric/tgmath>), introduzidas em C99, foram implementadas de maneira específica do compilador. As seleções genéricas, introduzidas em C11, deram aos programadores a capacidade de escrever código similar dependente de tipo.

A seleção genérica é semelhante à sobrecarga em C++ (onde uma das várias funções é escolhida em tempo de compilação com base nos tipos dos argumentos), exceto que ela faz a seleção entre expressões arbitrárias.

### Palavras-chave

[`_Generic`](<#/doc/keyword/_Generic>), [`default`](<#/doc/keyword/default>)

### Exemplo

Execute este código
```c
    #include <math.h>
    #include <stdio.h>
    
    // Possível implementação da macro cbrt de tgmath.h
    #define cbrt(X) _Generic((X),     \
                  long double: cbrtl, \
                      default: cbrt,  \
                        float: cbrtf  \
                  )(X)
    
    int main(void)
    {
        double x = 8.0;
        const float y = 3.375;
        printf("cbrt(8.0) = %f\n", cbrt(x));    // seleciona o cbrt padrão
        printf("cbrtf(3.375) = %f\n", cbrt(y)); // converte const float para float,
                                                // então seleciona cbrtf
    }
```

Output: 
```
    cbrt(8.0) = 2.000000
    cbrtf(3.375) = 1.500000
```

### Relatórios de defeito

Os seguintes relatórios de defeito que alteram o comportamento foram aplicados retroativamente a padrões C publicados anteriormente.

DR | Aplicado a | Comportamento conforme publicado | Comportamento correto   
[DR 481](<https://www.open-std.org/jtc1/sc22/wg14/www/docs/n2396.htm#dr_481>) | C11 | era subespecificado se a expressão controladora passava por conversões lvalue | ela passa   
  
### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 6.5.1.1 Seleção genérica (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 6.5.1.1 Seleção genérica (p: 56-57) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 6.5.1.1 Seleção genérica (p: 78-79) 

### Veja também

[Documentação C++](<#/>) para Templates  
---