# Conceitos básicos

Esta seção fornece definições para a terminologia específica e os conceitos usados ao descrever a linguagem de programação C.

Um programa C é uma sequência de arquivos de texto (tipicamente arquivos de cabeçalho e de código-fonte) que contêm [declarações](<#/doc/language/declarations>). Eles passam por [tradução](<#/doc/language/translation_phases>) para se tornarem um programa executável, que é executado quando o SO chama sua [função main](<#/doc/language/main_function>) (a menos que seja o próprio SO ou outro programa _freestanding_, nesse caso, o ponto de entrada é definido pela implementação).

Certas palavras em um programa C têm significado especial, elas são [palavras-chave](<#/doc/keyword>). Outras podem ser usadas como [identificadores](<#/doc/language/identifier>), que podem ser usados para identificar [objetos](<#/doc/language/object>), [funções](<#/doc/language/functions>), tags de [struct](<#/doc/language/struct>), [union](<#/doc/language/union>), ou [enumeração](<#/doc/language/enum>), seus membros, nomes de [typedef](<#/doc/language/typedef>), [rótulos](<#/doc/language/statements>), ou [macros](<#/doc/preprocessor/replace>).

Cada identificador (exceto macro) é válido apenas dentro de uma parte do programa chamada seu [escopo](<#/doc/language/scope>) e pertence a um dos quatro tipos de [espaços de nomes](<#/doc/language/name_space>). Alguns identificadores têm [ligação](<#/doc/language/storage_duration>) o que os faz referir-se às mesmas entidades quando aparecem em diferentes escopos ou unidades de tradução.

Definições de funções incluem sequências de [instruções](<#/doc/language/statements>) e [declarações](<#/doc/language/declarations>), algumas das quais incluem [expressões](<#/doc/language/expressions>), que especificam os cálculos a serem realizados pelo programa.

[Declarações](<#/doc/language/declarations>) e [expressões](<#/doc/language/expressions>) criam, destroem, acessam e manipulam [objetos](<#/doc/language/object>). Cada [objeto](<#/doc/language/object>), [função](<#/doc/language/functions>) e [expressão](<#/doc/language/expressions>) em C está associado a um [tipo](<#/doc/language/compatible_type>).

### Veja também

[documentação C++](<#/>) para Conceitos básicos
---