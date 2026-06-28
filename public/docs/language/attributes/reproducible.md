# Atributo C: unsequenced, reproducible (desde C23)

Fornece ao compilador informações sobre o acesso de objetos por uma função, de modo que certas propriedades de chamadas de função possam ser deduzidas.

### Sintaxe

---
`[[` `unsequenced` `]]`
`[[` `__unsequenced__` `]]` | (1) |
`[[` `reproducible` `]]`
`[[` `__reproducible__` `]]` | (2) |

1) Indica que uma função é [sem efeito](<#/doc/language/attributes/reproducible>), [idempotente](<#/doc/language/attributes/reproducible>), [sem estado](<#/doc/language/attributes/reproducible>) e [independente](<#/doc/language/attributes/reproducible>).

2) Indica que uma função é sem efeito e idempotente.

### Explicação

Esses atributos se aplicam a um declarador de função ou a um especificador de tipo que possui um tipo de função. O atributo correspondente é uma propriedade do tipo de função.

#### Sem Efeito

Uma avaliação de uma chamada de função é sem efeito se qualquer operação de armazenamento que é sequenciada durante a chamada for a modificação de um objeto que se sincroniza com a chamada; se adicionalmente a operação for observável, todo acesso ao objeto deve ser baseado em um parâmetro ponteiro único da função.

#### Idempotente

Uma avaliação E é idempotente se uma segunda avaliação de E puder ser sequenciada imediatamente após a original sem alterar o valor resultante, se houver, ou o estado observável da execução.

#### Sem Estado

Uma função F é sem estado se qualquer definição de um objeto com [duração de armazenamento](<#/doc/language/storage_duration>) estática ou de thread em F ou em uma função que é chamada por F for qualificada como const, mas não como volatile.

#### Independente

Uma função F é independente se, para qualquer objeto X que é observado por uma chamada a F através de um lvalue que não é baseado em um parâmetro da chamada, todos os acessos a X em todas as chamadas a F durante a mesma execução do programa observarem o mesmo valor; caso contrário, se o acesso for baseado em um parâmetro ponteiro, deverá haver um único parâmetro ponteiro P tal que qualquer acesso a X seja para um lvalue baseado em P.

Um objeto X é observado por uma chamada de função se ambos se sincronizam, se X não é local à chamada, se X tem um tempo de vida que começa antes da chamada de função, e se um acesso a X é sequenciado durante a chamada; o último valor de X, se houver, que é armazenado antes da chamada é dito ser o valor de X que é observado pela chamada.

### Notas

Esses atributos existem para fins de otimização do compilador.

Se uma função é reproducible, múltiplas chamadas subsequentes podem ser tratadas como uma única chamada.

Se uma função é unsequenced, múltiplas chamadas subsequentes podem ser tratadas como uma única chamada, e as chamadas podem ser paralelizadas e reordenadas arbitrariamente.