# Analisabilidade

Esta extensão opcional à linguagem C limita os resultados potenciais da execução de algumas formas de comportamento indefinido, o que melhora a eficácia da análise estática de tais programas. A analisabilidade só é garantida como habilitada se a [constante de macro predefinida](<#/doc/preprocessor/replace>) __STDC_ANALYZABLE__(C11) for definida pelo compilador.

Se o compilador suportar analisabilidade, qualquer construção de linguagem ou biblioteca cujo comportamento seja indefinido é ainda classificada entre comportamento indefinido _crítico_ e _limitado_, e o comportamento de todos os casos de UB limitado é restrito conforme especificado abaixo.

### Comportamento indefinido crítico

UB crítico é um comportamento indefinido que pode realizar uma escrita de memória ou uma leitura de memória volátil fora dos limites de qualquer objeto. Um programa que possui comportamento indefinido crítico pode ser suscetível a explorações de segurança.

Apenas os seguintes comportamentos indefinidos são críticos:

  * acesso a um objeto fora de seu [tempo de vida](<#/doc/language/lifetime>) (ex: através de um ponteiro pendente)
  * escrita em um objeto cujas declarações não são [compatíveis](<#/doc/language/compatible_type>)
  * chamada de função através de um ponteiro de função cujo tipo não é [compatível](<#/doc/language/compatible_type>) com o tipo da função para a qual ele aponta
  * expressão [lvalue](<#/doc/language/value_category>) é avaliada, mas não designa um objeto
  * tentativa de modificação de um [literal de string](<#/doc/language/string_literal>)
  * [desreferenciação](<#/doc/language/operator_member_access>) de um ponteiro inválido (nulo, indeterminado, etc) ou [além-do-fim](<#/doc/language/operator_arithmetic>)
  * modificação de um [objeto const](<#/doc/language/const>) através de um ponteiro não-const
  * chamada a uma função ou macro da biblioteca padrão com um argumento inválido
  * chamada a uma função variádica da biblioteca padrão com tipo de argumento inesperado (ex: chamada a [printf](<#/doc/io/fprintf>) com um argumento de um tipo que não corresponde ao seu especificador de conversão)
  * [longjmp](<#/doc/program/longjmp>) onde não há [setjmp](<#/doc/program/setjmp>) no escopo de chamada, entre threads, ou de dentro do escopo de um tipo VM.
  * qualquer uso do ponteiro que foi desalocado por [free](<#/doc/memory/free>) ou [realloc](<#/doc/memory/realloc>)
  * qualquer função da biblioteca de [string](<#/doc/string/byte>) ou [wide string](<#/doc/string/wide>) acessa um array fora dos limites

### Comportamento indefinido limitado

UB limitado é um comportamento indefinido que não pode realizar uma escrita de memória ilegal, embora possa causar uma armadilha (trap) e possa produzir ou armazenar valores indeterminados.

  * Todo comportamento indefinido não listado como crítico é limitado, incluindo

    

  * condições de corrida de dados multithread
  * uso de [valores indeterminados](<#/doc/language/initialization>) com duração de armazenamento automática
  * violações de [aliasing estrito](<#/doc/language/object>)
  * acesso a objeto [desalinhado](<#/doc/language/object>)
  * overflow de inteiro com sinal
  * [efeitos colaterais não sequenciados](<#/doc/language/eval_order>) modificam o mesmo escalar ou modificam e leem o mesmo escalar
  * overflow de [conversão](<#/doc/language/conversion>) de ponto flutuante para inteiro ou de ponteiro para inteiro
  * [deslocamento bit a bit](<#/doc/language/operator_arithmetic>) por uma contagem de bits negativa ou muito grande
  * [divisão inteira](<#/doc/language/operator_arithmetic>) por zero
  * uso de uma expressão void
  * [atribuição](<#/doc/language/operator_assignment>) direta ou [memcpy](<#/doc/string/byte/memcpy>) de objetos sobrepostos de forma inexata
  * violações de [restrict](<#/doc/language/restrict>)
  * etc... TODO comportamento indefinido que não está na lista crítica.

### Notas

O comportamento indefinido limitado desabilita certas otimizações: a compilação com analisabilidade habilitada preserva a causalidade do código-fonte, que [pode ser violada](<#/doc/language/as_if>) pelo comportamento indefinido de outra forma.

A extensão de analisabilidade permite, como uma forma de comportamento definido pela implementação, que o [manipulador de restrição em tempo de execução](<#/doc/error/set_constraint_handler_s>) seja invocado quando uma armadilha (trap) ocorre.

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 6.10.8.3/1 Macros de recurso condicional (p: 177)

    

  * Anexo L Analisabilidade (p: 652-653)