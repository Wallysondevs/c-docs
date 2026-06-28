# Regra as-if

Permite todas e quaisquer transformações de código que não alterem o comportamento observável do programa.

### Explicação

O compilador C tem permissão para realizar quaisquer alterações no programa, desde que o seguinte permaneça verdadeiro:

1) Em cada [ponto de sequência](<#/doc/language/eval_order>), os valores de todos os objetos [volatile](<#/doc/language/volatile>) são estáveis (avaliações anteriores estão completas, novas avaliações não iniciadas). | (ate C11)
1) Acessos (leituras e escritas) a objetos [volatile](<#/doc/language/volatile>) ocorrem estritamente de acordo com a semântica das expressões nas quais eles ocorrem. Em particular, eles [não são reordenados](<#/doc/atomic/memory_order>) em relação a outros acessos volatile na mesma thread. | (desde C11)

2) Na terminação do programa, os dados escritos em arquivos são exatamente como se o programa tivesse sido executado conforme escrito.

3) O texto de solicitação que é enviado para dispositivos interativos será exibido antes que o programa aguarde por entrada.

4) Se o pragma [` #pragma STDC FENV_ACCESS`](<#/doc/preprocessor/impl>) for suportado e estiver definido como `ON`, as alterações no [ambiente de ponto flutuante](<#/doc/numeric/fenv>) (exceções de ponto flutuante e modos de arredondamento) são garantidas de serem observadas pelos operadores aritméticos de ponto flutuante e chamadas de função como se executadas conforme escrito, exceto que

  * o resultado de qualquer expressão de ponto flutuante, exceto conversão de tipo (cast) e atribuição, pode ter um intervalo e precisão de um tipo de ponto flutuante diferente do tipo da expressão (veja [FLT_EVAL_METHOD](<#/doc/types/limits/FLT_EVAL_METHOD>)),
  * não obstante o acima, resultados intermediários de qualquer expressão de ponto flutuante podem ser calculados como se tivessem intervalo e precisão infinitos (a menos que [` #pragma STDC FP_CONTRACT`](<#/doc/preprocessor/impl>) esteja `OFF`).

| (desde C99)

### Notas

| Esta seção está incompleta
Razão: preencher de forma similar a [cpp/language/as_if](<#/>)

### Veja também

  * [Ordem de avaliação](<#/doc/language/eval_order>)

[Documentação C++](<#/>) para a regra as-if
---