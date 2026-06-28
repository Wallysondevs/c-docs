# Ambiente de ponto flutuante

O ambiente de ponto flutuante é o conjunto de flags de status de ponto flutuante e modos de controle suportados pela implementação. Ele é local à thread; cada thread herda o estado inicial de seu ambiente de ponto flutuante da thread pai. Operações de ponto flutuante modificam as flags de status de ponto flutuante para indicar resultados anormais ou informações auxiliares. O estado dos modos de controle de ponto flutuante afeta os resultados de algumas operações de ponto flutuante.

O acesso e a modificação do ambiente de ponto flutuante são significativos apenas quando [` #pragma STDC FENV_ACCESS`](<#/>) está definido como `ON`. Caso contrário, a implementação é livre para assumir que os modos de controle de ponto flutuante são sempre os padrão e que as flags de status de ponto flutuante nunca são testadas ou modificadas. Na prática, poucos compiladores atuais, como HP aCC, Oracle Studio e IBM XL, suportam o #pragma explicitamente, mas a maioria dos compiladores permite acesso significativo ao ambiente de ponto flutuante de qualquer forma.

### Tipos

Definido no cabeçalho `<fenv.h>`
---
fenv_t | O tipo que representa todo o ambiente de ponto flutuante
fexcept_t | O tipo que representa todas as flags de status de ponto flutuante coletivamente

### Funções

[ feclearexcept](<#/doc/numeric/fenv/feclearexcept>)(desde C99) | limpa as flags de status de ponto flutuante especificadas
(função)
[ fetestexcept](<#/doc/numeric/fenv/fetestexcept>)(desde C99) | determina quais das flags de status de ponto flutuante especificadas estão definidas
(função)
[ feraiseexcept](<#/doc/numeric/fenv/feraiseexcept>)(desde C99) | levanta as exceções de ponto flutuante especificadas
(função)
[ fegetexceptflagfesetexceptflag](<#/doc/numeric/fenv/feexceptflag>)(desde C99)(desde C99) | copia o estado das flags de status de ponto flutuante especificadas do ou para o ambiente de ponto flutuante
(função)
[ fegetroundfesetround](<#/doc/numeric/fenv/feround>)(desde C99)(desde C99) | obtém ou define a direção de arredondamento
(função)
[ fegetenvfesetenv](<#/doc/numeric/fenv/feenv>)(desde C99) | salva ou restaura o ambiente de ponto flutuante atual
(função)
[ feholdexcept](<#/doc/numeric/fenv/feholdexcept>)(desde C99) | salva o ambiente, limpa todas as flags de status e ignora todos os erros futuros
(função)
[ feupdateenv](<#/doc/numeric/fenv/feupdateenv>)(desde C99) | restaura o ambiente de ponto flutuante e levanta as exceções previamente levantadas
(função)

### Macros

[ FE_ALL_EXCEPTFE_DIVBYZEROFE_INEXACTFE_INVALIDFE_OVERFLOWFE_UNDERFLOW](<#/doc/numeric/fenv/FE_exceptions>)(desde C99) | exceções de ponto flutuante
(constante de macro)
[ FE_DOWNWARDFE_TONEARESTFE_TOWARDZEROFE_UPWARD](<#/doc/numeric/fenv/FE_round>)(desde C99) | direção de arredondamento de ponto flutuante
(constante de macro)
[ FE_DFL_ENV](<#/doc/numeric/fenv/FE_DFL_ENV>)(desde C99) | ambiente de ponto flutuante padrão
(constante de macro)

### Referências

* Padrão C23 (ISO/IEC 9899:2024):
  * 7.6 Ambiente de ponto flutuante <fenv.h> (p: TBD)
  * 7.31.4 Ambiente de ponto flutuante <fenv.h> (p: TBD)
* Padrão C17 (ISO/IEC 9899:2018):
  * 7.6 Ambiente de ponto flutuante <fenv.h> (p: 150-156)
  * 7.31.4 Ambiente de ponto flutuante <fenv.h> (p: 332)
* Padrão C11 (ISO/IEC 9899:2011):
  * 7.6 Ambiente de ponto flutuante <fenv.h> (p: 206-215)
  * 7.31.4 Ambiente de ponto flutuante <fenv.h> (p: 455)
* Padrão C99 (ISO/IEC 9899:1999):
  * 7.6 Ambiente de ponto flutuante <fenv.h> (p: 187-196)

### Veja também

[documentação C++](<#/>) para Ambiente de ponto flutuante
---