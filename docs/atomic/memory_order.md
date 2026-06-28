# memory_order

Definido no cabeçalho [`<stdatomic.h>`](<#/doc/thread>)

```c
enum memory_order
{
memory_order_relaxed,
memory_order_consume,
memory_order_acquire,
memory_order_release,
memory_order_acq_rel,
memory_order_seq_cst
};  // desde C11
```

`memory_order` especifica como os acessos à memória, incluindo acessos à memória regulares e não atômicos, devem ser ordenados em torno de uma operação atômica. Na ausência de quaisquer restrições em um sistema multi-core, quando múltiplas threads simultaneamente leem e escrevem em várias variáveis, uma thread pode observar os valores mudarem em uma ordem diferente da ordem em que outra thread os escreveu. De fato, a ordem aparente das mudanças pode até diferir entre múltiplas threads leitoras. Alguns efeitos semelhantes podem ocorrer mesmo em sistemas uniprocessadores devido a transformações do compilador permitidas pelo modelo de memória.

O comportamento padrão de todas as operações atômicas na [linguagem](<#/doc/language/atomic>) e na biblioteca prevê _ordenação sequencialmente consistente_ (veja a discussão abaixo). Esse padrão pode prejudicar o desempenho, mas as operações atômicas da biblioteca podem receber um argumento `memory_order` adicional para especificar as restrições exatas, além da atomicidade, que o compilador e o processador devem impor para essa operação.

### Constantes

Definido no cabeçalho `[`<stdatomic.h>`](<#/doc/thread>)`
---
Valor | Explicação
`memory_order_relaxed` | Operação relaxada: não há restrições de sincronização ou ordenação impostas a outras leituras ou escritas, apenas a atomicidade desta operação é garantida (veja [Ordenação Relaxada](<#/doc/atomic/memory_order>) abaixo).
`memory_order_consume` | Uma operação de carregamento com esta ordem de memória executa uma _operação de consumo_ no local de memória afetado: nenhuma leitura ou escrita na thread atual dependente do valor atualmente carregado pode ser reordenada antes deste carregamento. Escritas em variáveis dependentes de dados em outras threads que liberam a mesma variável atômica são visíveis na thread atual. Na maioria das plataformas, isso afeta apenas as otimizações do compilador (veja [Ordenação Release-Consume](<#/doc/atomic/memory_order>) abaixo).
`memory_order_acquire` | Uma operação de carregamento com esta ordem de memória executa a _operação de aquisição_ no local de memória afetado: nenhuma leitura ou escrita na thread atual pode ser reordenada antes deste carregamento. Todas as escritas em outras threads que liberam a mesma variável atômica são visíveis na thread atual (veja [Ordenação Release-Acquire](<#/doc/atomic/memory_order>) abaixo).
`memory_order_release` | Uma operação de armazenamento com esta ordem de memória executa a _operação de liberação_: nenhuma leitura ou escrita na thread atual pode ser reordenada após este armazenamento. Todas as escritas na thread atual são visíveis em outras threads que adquirem a mesma variável atômica (veja [Ordenação Release-Acquire](<#/doc/atomic/memory_order>) abaixo) e as escritas que _carregam uma dependência_ na variável atômica tornam-se visíveis em outras threads que consomem a mesma atômica (veja [Ordenação Release-Consume](<#/doc/atomic/memory_order>) abaixo).
`memory_order_acq_rel` | Uma operação de leitura-modificação-escrita com esta ordem de memória é tanto uma _operação de aquisição_ quanto uma _operação de liberação_. Nenhuma leitura ou escrita de memória na thread atual pode ser reordenada antes do carregamento, nem depois do armazenamento. Todas as escritas em outras threads que liberam a mesma variável atômica são visíveis antes da modificação e a modificação é visível em outras threads que adquirem a mesma variável atômica.
`memory_order_seq_cst` | Uma operação de carregamento com esta ordem de memória executa uma _operação de aquisição_, um armazenamento executa uma _operação de liberação_, e uma leitura-modificação-escrita executa tanto uma _operação de aquisição_ quanto uma _operação de liberação_, além de existir uma _única ordem total_ na qual todas as threads observam todas as modificações na mesma ordem (veja [Ordenação Sequencialmente Consistente](<#/doc/atomic/memory_order>) abaixo).
| Esta seção está incompleta
Razão: happens-before e outros conceitos, como em C++, mas manter as ordens de modificação e as quatro consistências em [c/language/atomic](<#/doc/language/atomic>)
| Esta seção está incompleta
Razão: ao fazer o acima, não esquecer que, embora happens-before não fosse acíclico em C11 conforme publicado, isso foi atualizado para corresponder ao C++11 via DR 401

#### Ordenação Relaxada

Operações atômicas marcadas com `memory_order_relaxed` não são operações de sincronização; elas não impõem uma ordem entre acessos concorrentes à memória. Elas apenas garantem atomicidade e consistência da ordem de modificação.

Por exemplo, com x e y inicialmente zero,

```c
// Thread 1:
r1 = atomic_load_explicit(y, memory_order_relaxed); // A
atomic_store_explicit(x, r1, memory_order_relaxed); // B
// Thread 2:
r2 = atomic_load_explicit(x, memory_order_relaxed); // C
atomic_store_explicit(y, 42, memory_order_relaxed); // D
```
é permitido produzir `r1 == r2 == 42` porque, embora A seja _sequenciado antes_ de B dentro da thread 1 e C seja _sequenciado antes_ de D dentro da thread 2, nada impede que D apareça antes de A na ordem de modificação de y, e B de aparecer antes de C na ordem de modificação de x. O efeito colateral de D em y poderia ser visível para o carregamento A na thread 1, enquanto o efeito colateral de B em x poderia ser visível para o carregamento C na thread 2. Em particular, isso pode ocorrer se D for concluído antes de C na thread 2, seja devido a reordenação do compilador ou em tempo de execução.

O uso típico para ordenação de memória relaxada é o incremento de contadores, como os contadores de referência, já que isso requer apenas atomicidade, mas não ordenação ou sincronização.

#### Ordenação Release-Consume

Se um armazenamento atômico na thread A for marcado com `memory_order_release`, um carregamento atômico na thread B da mesma variável for marcado com `memory_order_consume`, e o carregamento na thread B ler um valor escrito pelo armazenamento na thread A, então o armazenamento na thread A é _ordenado por dependência antes_ do carregamento na thread B.

Todas as escritas de memória (não atômicas e atômicas relaxadas) que _aconteceram antes_ do armazenamento atômico do ponto de vista da thread A, tornam-se _efeitos colaterais visíveis_ dentro daquelas operações na thread B para as quais a operação de carregamento _carrega dependência_, ou seja, uma vez que o carregamento atômico é concluído, os operadores e funções na thread B que usam o valor obtido do carregamento têm a garantia de ver o que a thread A escreveu na memória.

A sincronização é estabelecida apenas entre as threads que _liberam_ e _consumem_ a mesma variável atômica. Outras threads podem ver uma ordem de acessos à memória diferente de uma ou de ambas as threads sincronizadas.

Em todas as CPUs mainstream, exceto DEC Alpha, a ordenação por dependência é automática, nenhuma instrução de CPU adicional é emitida para este modo de sincronização, apenas certas otimizações do compilador são afetadas (por exemplo, o compilador é proibido de realizar carregamentos especulativos nos objetos que estão envolvidos na cadeia de dependência).

Casos de uso típicos para esta ordenação envolvem acesso de leitura a estruturas de dados concorrentes raramente escritas (tabelas de roteamento, configuração, políticas de segurança, regras de firewall, etc.) e situações de publicador-assinante com publicação mediada por ponteiro, ou seja, quando o produtor publica um ponteiro através do qual o consumidor pode acessar informações: não há necessidade de tornar todo o resto que o produtor escreveu na memória visível para o consumidor (o que pode ser uma operação cara em arquiteturas fracamente ordenadas). Um exemplo de tal cenário é [`rcu_dereference`](<https://en.wikipedia.org/wiki/Read-copy-update> "enwiki:Read-copy-update").

Note que atualmente (2/2015) nenhum compilador de produção conhecido rastreia cadeias de dependência: operações de consumo são elevadas a operações de aquisição.

#### Sequência de Liberação

Se algum atômico for armazenado-liberado e várias outras threads realizarem operações de leitura-modificação-escrita nesse atômico, uma "sequência de liberação" é formada: todas as threads que realizam as leituras-modificações-escritas no mesmo atômico sincronizam com a primeira thread e entre si, mesmo que não tenham semântica `memory_order_release`. Isso torna possíveis situações de um único produtor - múltiplos consumidores sem impor sincronização desnecessária entre threads consumidoras individuais.

#### Ordenação Release-Acquire

Se um armazenamento atômico na thread A for marcado com `memory_order_release`, um carregamento atômico na thread B da mesma variável for marcado com `memory_order_acquire`, e o carregamento na thread B ler um valor escrito pelo armazenamento na thread A, então o armazenamento na thread A _sincroniza-se com_ o carregamento na thread B.

Todas as escritas de memória (incluindo não atômicas e atômicas relaxadas) que _aconteceram antes_ do armazenamento atômico do ponto de vista da thread A, tornam-se _efeitos colaterais visíveis_ na thread B. Ou seja, uma vez que o carregamento atômico é concluído, a thread B tem a garantia de ver tudo o que a thread A escreveu na memória. Esta promessa só é válida se B realmente retornar o valor que A armazenou, ou um valor posterior na sequência de liberação.

A sincronização é estabelecida apenas entre as threads que _liberam_ e _adquirem_ a mesma variável atômica. Outras threads podem ver uma ordem de acessos à memória diferente de uma ou de ambas as threads sincronizadas.

Em sistemas fortemente ordenados — x86, SPARC TSO, IBM mainframe, etc. — a ordenação release-acquire é automática para a maioria das operações. Nenhuma instrução de CPU adicional é emitida para este modo de sincronização; apenas certas otimizações do compilador são afetadas (por exemplo, o compilador é proibido de mover armazenamentos não atômicos para além do armazenamento-liberação atômico ou de realizar carregamentos não atômicos antes do carregamento-aquisição atômico). Em sistemas fracamente ordenados (ARM, Itanium, PowerPC), instruções especiais de carregamento de CPU ou de barreira de memória são usadas.

Bloqueios de exclusão mútua, como [mutexes](<#/doc/thread>) ou [spinlocks atômicos](<#/doc/atomic/atomic_flag_test_and_set>), são um exemplo de sincronização release-acquire: quando o bloqueio é liberado pela thread A e adquirido pela thread B, tudo o que ocorreu na seção crítica (antes da liberação) no contexto da thread A deve ser visível para a thread B (após a aquisição) que está executando a mesma seção crítica.

#### Ordenação Sequencialmente Consistente

Operações atômicas marcadas com `memory_order_seq_cst` não apenas ordenam a memória da mesma forma que a ordenação release/acquire (tudo o que _aconteceu antes_ de um armazenamento em uma thread torna-se um _efeito colateral visível_ na thread que realizou um carregamento), mas também estabelecem uma _única ordem total de modificação_ de todas as operações atômicas assim marcadas.

Formalmente,

cada operação `memory_order_seq_cst` B que carrega da variável atômica M, observa um dos seguintes:

  * o resultado da última operação A que modificou M, que aparece antes de B na única ordem total,
  * OU, se houve tal A, B pode observar o resultado de alguma modificação em M que não é `memory_order_seq_cst` e não _acontece antes_ de A,
  * OU, se não houve tal A, B pode observar o resultado de alguma modificação não relacionada de M que não é `memory_order_seq_cst`.

Se houve uma operação `memory_order_seq_cst` [atomic_thread_fence](<#/doc/atomic/atomic_thread_fence>) X _sequenciada antes_ de B, então B observa um dos seguintes:

  * a última modificação `memory_order_seq_cst` de M que aparece antes de X na única ordem total,
  * alguma modificação não relacionada de M que aparece mais tarde na ordem de modificação de M.

Para um par de operações atômicas em M chamadas A e B, onde A escreve e B lê o valor de M, se houver duas [atomic_thread_fence](<#/doc/atomic/atomic_thread_fence>)s `memory_order_seq_cst` X e Y, e se A é _sequenciado antes_ de X, Y é _sequenciado antes_ de B, e X aparece antes de Y na Ordem Total Única, então B observa um dos seguintes:

  * o efeito de A,
  * alguma modificação não relacionada de M que aparece depois de A na ordem de modificação de M.

Para um par de modificações atômicas de M chamadas A e B, B ocorre depois de A na ordem de modificação de M se

  * existe uma [atomic_thread_fence](<#/doc/atomic/atomic_thread_fence>) `memory_order_seq_cst` X tal que A é _sequenciado antes_ de X e X aparece antes de B na Ordem Total Única,
  * ou, existe uma [atomic_thread_fence](<#/doc/atomic/atomic_thread_fence>) `memory_order_seq_cst` Y tal que Y é _sequenciado antes_ de B e A aparece antes de Y na Ordem Total Única,
  * ou, existem [atomic_thread_fence](<#/doc/atomic/atomic_thread_fence>)s `memory_order_seq_cst` X e Y tais que A é _sequenciado antes_ de X, Y é _sequenciado antes_ de B, e X aparece antes de Y na Ordem Total Única.

Note que isso significa que:

1) assim que operações atômicas que não são marcadas com `memory_order_seq_cst` entram em cena, a consistência sequencial é perdida,

2) as barreiras sequencialmente consistentes estão apenas estabelecendo uma ordenação total para as próprias barreiras, não para as operações atômicas no caso geral (_sequenced-before_ não é uma relação entre threads, ao contrário de _happens-before_).

A ordenação sequencial pode ser necessária para situações de múltiplos produtores-múltiplos consumidores onde todos os consumidores devem observar as ações de todos os produtores ocorrendo na mesma ordem.

A ordenação sequencial total requer uma instrução de barreira de memória completa da CPU em todos os sistemas multi-core. Isso pode se tornar um gargalo de desempenho, pois força os acessos à memória afetados a se propagarem para cada núcleo.

### Relação com volatile

Dentro de uma thread de execução, acessos (leituras e escritas) através de [lvalues volatile](<#/doc/language/volatile>) não podem ser reordenados para além de efeitos colaterais observáveis (incluindo outros acessos volatile) que são separados por um ponto de sequência dentro da mesma thread, mas esta ordem não é garantida para ser observada por outra thread, uma vez que o acesso volatile não estabelece sincronização entre threads.

Além disso, acessos volatile não são atômicos (leitura e escrita concorrentes são uma [condição de corrida de dados](<#/doc/language/memory_model>)) e não ordenam a memória (acessos à memória não-volatile podem ser livremente reordenados em torno do acesso volatile).

Uma exceção notável é o Visual Studio, onde, com as configurações padrão, cada escrita volatile tem semântica de liberação e cada leitura volatile tem semântica de aquisição ([Microsoft Docs](<https://learn.microsoft.com/en-us/cpp/cpp/volatile-cpp>)), e assim volatiles podem ser usados para sincronização entre threads. A semântica volatile padrão não é aplicável à programação multi-threaded, embora seja suficiente, por exemplo, para comunicação com um manipulador de [sinal](<#/doc/program/signal>) que executa na mesma thread quando aplicada a variáveis [sig_atomic_t](<#/doc/program/sig_atomic_t>).

### Exemplos

| Esta seção está incompleta
Razão: nenhum exemplo

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.17.1/4 memory_order (p: TBD)

    

  * 7.17.3 Ordem e consistência (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.17.1/4 memory_order (p: 200)

    

  * 7.17.3 Ordem e consistência (p: 201-203)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.17.1/4 memory_order (p: 273)

    

  * 7.17.3 Ordem e consistência (p: 275-277)

### Veja também

[Documentação C++](<#/>) para ordem de memória
---

### Links externos

1\. | [Protocolo MOESI](<https://en.wikipedia.org/wiki/MOESI_protocol> "enwiki:MOESI protocol")
2\. | [x86-TSO: Um Modelo de Programador Rigoroso e Utilizável para Multiprocessadores x86](<https://www.cl.cam.ac.uk/~pes20/weakmemory/cacm.pdf>) P. Sewell et. al., 2010
3\. | [Uma Introdução Tutorial aos Modelos de Memória Relaxada ARM e POWER](<https://www.cl.cam.ac.uk/~pes20/ppc-supplemental/test7.pdf>) P. Sewell et al, 2012
4\. | [MESIF: Um Protocolo de Coerência de Cache de Dois Saltos para Interconexões Ponto a Ponto](<https://researchspace.auckland.ac.nz/bitstream/handle/2292/11594/MESIF-2009.pdf?sequence=6>) J.R. Goodman, H.H.J. Hum, 2009
5\. | [Modelos de Memória](<https://research.swtch.com/mm>) Russ Cox, 2021
| Esta seção está incompleta
Razão: Vamos encontrar boas referências sobre QPI, MOESI e talvez Dragon.