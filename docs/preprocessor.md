# Pré-processador

O pré-processador é executado na [fase de tradução 4](<#/doc/language/translation_phases>), antes da compilação. O resultado do pré-processamento é um único arquivo que é então passado para o compilador real.

### Diretivas

As diretivas de pré-processamento controlam o comportamento do pré-processador. Cada diretiva ocupa uma linha e tem o seguinte formato:

  * caractere `#`
  * instrução de pré-processamento (uma de `define`, `undef`, `include`, `if`, `ifdef`, `ifndef`, `else`, `elif`, `elifdef`, `elifndef`(desde C23), `endif`, `line`, `embed`(desde C23), `error`, `warning`(desde C23), `pragma`) [1](<#/doc/preprocessor>)
  * argumentos (depende da instrução)
  * quebra de linha.

A diretiva nula (`#` seguida por uma quebra de linha) é permitida e não tem efeito.

### Capacidades

O pré-processador possui as seguintes capacidades de tradução de arquivos-fonte:

  * **[compilar condicionalmente](<#/doc/preprocessor/conditional>)** partes do arquivo-fonte (controlado pelas diretivas `#if`, `#ifdef`, `#ifndef`, `#else`, `#elif`, `#elifdef`, `#elifndef`(desde C23) e `#endif`).
  * **[substituir](<#/doc/preprocessor/replace>)** macros de texto, possivelmente concatenando ou colocando identificadores entre aspas (controlado pelas diretivas `#define` e `#undef`, e pelos operadores `#` e `##`)
  * **[incluir](<#/doc/preprocessor/include>)** outros arquivos (controlado pela diretiva `#include` e verificado com `__has_include`(desde C23))
  * causar um **[erro](<#/doc/preprocessor/error>)** ou **[aviso](<#/doc/preprocessor/error>)**(desde C23) (controlado pela diretiva `#error` ou `#warning` respectivamente(desde C23))

Os seguintes aspectos do pré-processador podem ser controlados:

  * comportamento **[definido pela implementação](<#/doc/preprocessor/impl>)** (controlado pela diretiva `#pragma` e pelo operador `_Pragma`(desde C99))
  * **[nome do arquivo e informações de linha](<#/doc/preprocessor/line>)** disponíveis para o pré-processador (controlado pelas diretivas `#line`)

### Notas de Rodapé

  1. [↑](<#/doc/preprocessor>) Estas são as diretivas definidas pelo padrão. O padrão não define o comportamento para outras diretivas: elas podem ser ignoradas, ter algum significado útil ou tornar o programa malformado. Mesmo que ignoradas, elas são removidas do código-fonte quando o pré-processador termina. Uma extensão não padronizada comum é a diretiva [#warning](<#/doc/preprocessor/error>) que emite uma mensagem definida pelo usuário durante a compilação.(até C23)

### Exemplo

| Esta seção está incompleta
Razão: sem exemplo

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 6.10 Diretivas de pré-processamento (p: A definir)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 6.10 Diretivas de pré-processamento (p: 117-129)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 6.10 Diretivas de pré-processamento (p: 160-178)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 6.10 Diretivas de pré-processamento (p: 145-162)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 3.8 Diretivas de pré-processamento

### Veja também

[Documentação C](<#/doc/preprocessor/replace>) para Símbolos de Macro Predefinidos
---
[Documentação C](<#/>) para Índice de Símbolos de Macro
[Documentação C++](<#/>) para Pré-processador