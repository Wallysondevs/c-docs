# Conformidade

_Conformidade_ possui uma definição tripla:

  * _programa estritamente conforme_ - usa apenas construções de linguagem bem definidas, ou seja, construções com um único comportamento. Exclui comportamento não especificado, indefinido ou definido pela implementação, e não excede nenhum limite mínimo de implementação.
  * _programa conforme_ - aceitável para uma implementação conforme.
  * _implementação conforme_ -
    * Uma implementação hospedada conforme deve aceitar qualquer programa estritamente conforme.
    * Uma implementação autônoma conforme deve aceitar qualquer programa estritamente conforme no qual o uso dos recursos especificados na cláusula da biblioteca (cláusula 7) esteja restrito ao conteúdo dos cabeçalhos da biblioteca padrão autônoma (veja abaixo).
    * Uma implementação conforme pode ter extensões (incluindo funções de biblioteca adicionais), desde que não alterem o comportamento de nenhum programa estritamente conforme.

### Explicação

O padrão não define nenhum limite mínimo de implementação para unidades de tradução. Um ambiente hospedado possui um sistema operacional; um ambiente autônomo não. Um programa executado em um ambiente hospedado pode usar todos os recursos descritos na cláusula da biblioteca (cláusula 7); um programa executado em um ambiente autônomo pode usar um subconjunto de recursos da biblioteca exigidos pela cláusula 4.

#### Cabeçalhos da biblioteca padrão autônoma

Todos os recursos da biblioteca padrão em cada cabeçalho totalmente autônomo devem ser fornecidos por uma implementação autônoma.

Alguns cabeçalhos da biblioteca padrão são condicionalmente autônomos.

  * Se a implementação predefinir a macro `__STDC_IEC_60559_BFP__` ou `__STDC_IEC_60559_DFP__`, então [`<math.h>`](<#/doc/numeric/math>) e [`<fenv.h>`](<#/doc/numeric/fenv>) são cabeçalhos totalmente autônomos. No entanto, o comportamento das funções nesses cabeçalhos é exigido como bem definido em um ambiente autônomo apenas se um programa não definir o estado do pragma [`FENV_ACCESS`](<#/doc/preprocessor/impl>) para `ON`.

Alguns cabeçalhos da biblioteca padrão são parcialmente autônomos.

  * Em [`<stdlib.h>`](<#/doc/program>), [`memalignment`](<#/doc/program/memalignment>) é autônomo. Além disso, quando `__STDC_IEC_60559_BFP__` ou `__STDC_IEC_60559_DFP__` são predefinidos, as funções de conversão numérica (`ato _X_`, `strto _X_` e `strfrom _X_`) também são autônomas, enquanto seu comportamento é exigido como bem definido em um ambiente autônomo apenas se um programa não definir o estado do pragma [`FENV_ACCESS`](<#/doc/preprocessor/impl>) para `ON`. Nenhum outro componente em [`<stdlib.h>`](<#/doc/program>) é exigido para ser fornecido por uma implementação autônoma.
  * Em [`<string.h>`](<#/doc/string/byte>), [`strdup`](<#/doc/string/byte/strdup>), [`strndup`](<#/doc/string/byte/strndup>), [strcoll](<#/doc/string/byte/strcoll>), [strxfrm](<#/doc/string/byte/strxfrm>), [strtok](<#/doc/string/byte/strtok>) e [strerror](<#/doc/string/byte/strerror>) não são exigidos para serem fornecidos por uma implementação autônoma.

| (desde C23)
##### Cabeçalhos da biblioteca padrão totalmente autônomos

---
[`<float.h>`](<#/doc/types/limits>) | [Limites de tipos de ponto flutuante](<#/doc/types/limits>)
[`<iso646.h>`](<#/doc/language/operator_alternative>) (desde C95) | [Grafias alternativas de operadores](<#/doc/language/operator_alternative>)
[`<limits.h>`](<#/doc/types/limits>) | [Intervalos de tipos inteiros](<#/doc/types/limits>)
[`<stdalign.h>`](<#/doc/types>) (desde C11) | Macros de conveniência [`alignas` e `alignof`](<#/doc/types>)
[`<stdarg.h>`](<#/doc/variadic>) | [Argumentos variáveis](<#/doc/variadic>)
[`<stdbool.h>`](<#/doc/types>) (desde C99) | [Macros para tipo booleano](<#/doc/types>)
[`<stddef.h>`](<#/doc/types>) | [Definições de macro comuns](<#/doc/types>)
[`<stdint.h>`](<#/doc/types/integer>) (desde C99) | [Tipos inteiros de largura fixa](<#/doc/types/integer>)
[`<stdnoreturn.h>`](<#/doc/language/_Noreturn>) (desde C11) | Macro de conveniência [`noreturn`](<#/doc/types>)
[`<stdbit.h>`](<#/doc/numeric>) (desde C23) | Macros para trabalhar com as representações de byte e bit de tipos

##### Cabeçalhos da biblioteca padrão condicionalmente totalmente autônomos

[`<fenv.h>`](<#/doc/numeric/fenv>) (desde C23) | [Ambiente de ponto flutuante](<#/doc/numeric/fenv>)
[`<math.h>`](<#/doc/numeric/math>) (desde C23) | [Funções matemáticas comuns](<#/doc/numeric/math>)

##### Cabeçalhos da biblioteca padrão parcialmente autônomos

[`<stdlib.h>`](<#/doc/program>) (desde C23) | Utilitários gerais: [gerenciamento de memória](<#/doc/memory>), [utilitários de programa](<#/doc/program>), [conversões de string](<#/doc/string>), [números aleatórios](<#/doc/numeric/random>), [algoritmos](<#/doc/algorithm>)
[`<string.h>`](<#/doc/string/byte>) (desde C23) | [Manipulação de strings](<#/doc/string/byte>)

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 4 Conformidade (p: 9-10)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 4 Conformidade (p: 4)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 4 Conformidade (p: 8-9)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 4 Conformidade (p: 7-8)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 1.7 Conformidade

### Veja também

[Documentação C++](<#/>) para implementação autônoma e hospedada
---