# especificador constexpr (desde C23)

Um objeto escalar declarado com o especificador de classe de armazenamento `constexpr` é uma [constante](<#/doc/language/constant_expression>). Ele deve ser totalmente e explicitamente inicializado de acordo com as regras de inicialização estática. Ele ainda possui ligação apropriada à sua declaração e existe em tempo de execução para que seu endereço possa ser obtido; ele simplesmente não pode ser modificado em tempo de execução de forma alguma, ou seja, o compilador pode usar seu conhecimento do valor fixo do objeto em qualquer outra [expressão constante](<#/doc/language/constant_expression>).

Além disso, a expressão constante que é usada para o inicializador de tal constante é verificada em tempo de compilação.

Um inicializador de tipo de ponto flutuante deve ser avaliado com o ambiente de ponto flutuante em tempo de tradução.

Existem algumas restrições sobre o tipo de um objeto que pode ser declarado com `constexpr`. Ou seja, as seguintes construções não são permitidas para serem `constexpr`:

  * [Ponteiros](<#/doc/language/pointer>) (exceto que ponteiros nulos podem ser `constexpr`),
  * Tipos modificados variavelmente,
  * [Tipos atômicos](<#/doc/language/atomic>),
  * Tipos [`volatile`](<#/doc/language/volatile>),
  * Ponteiros [`restrict`](<#/doc/language/restrict>).

### Palavras-chave

[`constexpr`](<#/doc/keyword/constexpr>)

### Notas

### Exemplo

Execute este código
```c
    #include <fenv.h>
    #include <stdio.h>
    
    int main(void)
    {
        constexpr float f = 23.0f;
        constexpr float g = 33.0f;
        fesetround(FE_TOWARDZERO);
        constexpr float h = f / g; // não é afetado por fesetround() acima
        printf("%f\n", h);
    }
```

Saída:
```
    0.696969
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * TBD TBD (p: TBD)

### Veja também

[Documentação C++](<#/>) para o especificador de tipo `constexpr`