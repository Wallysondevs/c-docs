# FLT_ROUNDS

Definido no cabeçalho [`<float.h>`](<#/doc/types/limits>)

```c
#define FLT_ROUNDS /* implementation defined */
```

Retorna a direção de arredondamento atual das operações aritméticas de ponto flutuante.

Valor | Explicação
`-1` | a direção de arredondamento padrão é desconhecida
`0` | em direção a zero; mesmo significado que [FE_TOWARDZERO](<#/doc/numeric/fenv/FE_round>)
`1` | para o mais próximo; mesmo significado que [FE_TONEAREST](<#/doc/numeric/fenv/FE_round>)
`2` | em direção ao infinito positivo; mesmo significado que [FE_UPWARD](<#/doc/numeric/fenv/FE_round>)
`3` | em direção ao infinito negativo; mesmo significado que [FE_DOWNWARD](<#/doc/numeric/fenv/FE_round>)
outros valores | comportamento definido pela implementação

### Notas

O modo de arredondamento pode ser alterado com [fesetround](<#/doc/numeric/fenv/feround>) e **FLT_ROUNDS** reflete essa mudança.

### Veja também

[ fegetroundfesetround](<#/doc/numeric/fenv/feround>)(C99)(C99) | obtém ou define a direção de arredondamento
(função)
[ FE_DOWNWARDFE_TONEARESTFE_TOWARDZEROFE_UPWARD](<#/doc/numeric/fenv/FE_round>)(C99) | direção de arredondamento de ponto flutuante
(constante de macro)
[Documentação C++](<#/>) para FLT_ROUNDS