# FLT_EVAL_METHOD

Definido no cabeçalho [`<float.h>`](<#/doc/types/limits>)

```c
#define FLT_EVAL_METHOD /* implementation-defined */  // desde C99
```

Especifica o intervalo e a precisão dos valores de ponto flutuante obtidos de constantes de ponto flutuante e de todas as operações (operadores, conversões implícitas de operandos), exceto atribuição, conversão de tipo (cast) e chamadas de funções de biblioteca.

Valor | Explicação
valores negativos, exceto -1 | comportamento definido pela implementação
-1 | a precisão padrão não é conhecida
​0​ | todas as operações e constantes são avaliadas no intervalo e precisão do tipo usado. Além disso, float_t e double_t são equivalentes a float e double, respectivamente
1 | todas as operações e constantes são avaliadas no intervalo e precisão de double. Além disso, tanto float_t quanto double_t são equivalentes a double
2 | todas as operações e constantes são avaliadas no intervalo e precisão de long double. Além disso, tanto float_t quanto double_t são equivalentes a long double

### Notas

Independentemente do valor de FLT_EVAL_METHOD, qualquer expressão de ponto flutuante pode ser _contraída_, ou seja, calculada como se todos os resultados intermediários tivessem intervalo e precisão infinitos (a menos que [` #pragma`](<#/doc/preprocessor/impl>)` STDC FP_CONTRACT esteja desativado).

A conversão de tipo (cast) e a atribuição removem qualquer intervalo e precisão supérfluos: isso modela a ação de armazenar um valor de um registrador FPU de precisão estendida em um local de memória de tamanho padrão.

### Veja também

[ float_t](<#/doc/numeric/math/float_t>)(C99) | tipo de ponto flutuante mais eficiente, pelo menos tão largo quanto float
(typedef)
[ double_t](<#/doc/numeric/math/float_t>)(C99) | tipo de ponto flutuante mais eficiente, pelo menos tão largo quanto double
[documentação C++](<#/>) para FLT_EVAL_METHOD