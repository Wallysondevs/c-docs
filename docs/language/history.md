# Histórico do C

## C Primitivo
  
  * 1969: B criado, baseado em BCPL, para substituir o assembler do PDP-7 como linguagem de programação de sistema para Unix 

    

  * adicionou os operadores ++, --, atribuição composta, permaneceu uma linguagem sem tipos como BCPL 

  * 1971: NB ("new B") criado ao portar B para PDP-11 

    

  * tipos (int, char, arrays e ponteiros), conversão de array para ponteiro, compilação para código de máquina 

  * 1972: Linguagem renomeada para C 

    

  * struct, operadores && e ||, pré-processador, I/O portátil 

  * 1973: Unix reescrito em C 

    

  * unsigned, long, union, enumerações, segurança de tipo aumentada 

  * 1978: The C Programming Language, 1ª edição 

## C Padrão

  * 1983: ANSI estabeleceu o comitê X3J11 
  * 1988: The C Programming Language, 2ª edição 
  * 1989: **C89** , o padrão ANSI C publicado 

  1. codificou práticas existentes 
  2. novas funcionalidades: volatile, enum, signed, void, locales 
  3. Do C++: const, protótipos de função 

  * 1990: **C90** , o padrão ANSI C aceito como ISO/IEC 9899:1990 
  * 1994: Corrigendum Técnico 1 (ISO/IEC 9899:1990/Cor.1:1994) 

    

  * [44 pequenas alterações](<https://open-std.org/JTC1/SC22/WG14/www/docs/tc1.htm>)

  * 1995: **C95** (ISO/IEC 9899:1990/Amd.1:1995) ([loja online](<https://infostore.saiglobal.com/store/Details.aspx?DocN=isoc000767513>)) 

  1. suporte amplamente expandido para caracteres largos e multibyte ([`<wctype.h>`](<#/doc/string/wide>), [`<wchar.h>`](<#/doc/string/wide>), adições e alterações ao I/O de stream, etc) 
  2. dígrafos, [`<iso646.h>`](<#/doc/language/operator_alternative>), 

  * 1996: Corrigendum Técnico 2 (ISO/IEC 9899:1990/Cor.2:1996) 

    

  * [24 pequenas alterações](<https://open-std.org/JTC1/SC22/WG14/www/docs/tc2.htm>)

  * 1999: **C99** (ISO/IEC 9899:1999) 

  1. novas funcionalidades: bool, long long, [`<stdint.h>`](<#/doc/types/integer>), [`<inttypes.h>`](<#/doc/types/integer>), restrict, literais compostos, arrays de tamanho variável, membros de array flexíveis, inicializadores designados, [`<fenv.h>`](<#/doc/numeric/fenv>), macros variádicas, números complexos, __func__, formato hexadecimal de ponto flutuante (%a), formatação monetária em [lconv](<#/doc/locale/lconv>), [isblank](<#/doc/string/byte/isblank>), concatenação de literais de string estreitos e largos, vírgula final em enumerações, argumentos vazios em macros tipo função, pragmas STDC_*, va_copy, retorno nulo de [tmpnam](<#/doc/io/tmpnam>), ponteiro nulo em [setvbuf](<#/doc/io/setvbuf>), especificadores de comprimento `hh` e `ll` em [printf](<#/doc/io/fprintf>), [snprintf](<#/doc/io/fprintf>), [_Exit](<#/doc/program/_Exit>), [`<tgmath.h>`](<#/doc/numeric/tgmath>), especificadores [strftime](<#/doc/chrono/strftime>) tipo POSIX 
  2. do C++: inline, mistura de declarações e código, declarações na cláusula init do loop for, comentários //, nomes de caracteres universais no código fonte 
  3. removeu funções implícitas e int implícito

  * 2001: Corrigendum Técnico 1 (ISO/IEC 9899:1999/Cor.1:2001) 

    

  * [11 defeitos corrigidos](<https://open-std.org/JTC1/SC22/WG14/www/docs/9899tc1/.>)

  * 2004: Corrigendum Técnico 2 (ISO/IEC 9899:1999/Cor.2:2004) 
  * 2004: TR Unicode (ISO/IEC TR 19769:2004) ([loja ISO](<https://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=33907>)) ([N1040](<https://open-std.org/JTC1/SC22/WG14/www/docs/n1040.pdf>) rascunho de 7 de novembro de 2003) 
  * 2007: Corrigendum Técnico 3 (ISO/IEC 9899:1999/Cor.3:2007) ([N1256](<https://open-std.org/JTC1/SC22/WG14/www/docs/n1256.pdf>) rascunho de 7 de setembro de 2007) 

    

  * [gets](<#/doc/io/gets>) obsoleto

  * 2007: TR de interfaces de verificação de limites (ISO/IEC TR 24731-1:2007) ([loja ISO](<https://www.iso.org/iso/catalogue_detail.htm?csnumber=38841>)) ([N1225](<https://open-std.org/JTC1/SC22/WG14/www/docs/n1225.pdf>) rascunho de 28 de março de 2007) 
  * 2008: TR Embarcado (ISO/IEC TR 18037:2008) ([loja ISO](<https://www.iso.org/iso/catalogue_detail.htm?csnumber=51126>)) ([N1021](<https://open-std.org/JTC1/SC22/WG14/www/docs/n1021.pdf>) rascunho de 24 de setembro de 2003) 
  * 2009: TR de ponto flutuante decimal (ISO/IEC TR 24732:2009) ([loja ISO](<https://www.iso.org/iso/catalogue_detail.htm?csnumber=38842>)) ([N1241](<https://open-std.org/JTC1/SC22/WG14/www/docs/n1241.pdf>) rascunho de 5 de julho de 2007) 
  * 2009: TR de funções matemáticas especiais (ISO/IEC TR 24747:2009) ([loja ISO](<https://www.iso.org/iso/catalogue_detail.htm?csnumber=38857>)) ([N1182](<https://open-std.org/JTC1/SC22/WG14/www/docs/n1182.pdf>) rascunho de 2 de agosto de 2006) 
  * 2010: TR de funções de alocação dinâmica (ISO/IEC TR 24731-2:2010) ([loja ISO](<https://www.iso.org/iso/catalogue_detail.htm?csnumber=51678>)) ([N1388](<https://open-std.org/JTC1/SC22/WG14/www/docs/n1388.pdf>) rascunho de 1º de junho de 2009) 
  * 2011: **C11** (ISO/IEC 9899:2011) ([loja ISO](<https://www.iso.org/iso/home/store/catalogue_tc/catalogue_detail.htm?csnumber=57853>)) ([loja ANSI](<https://webstore.ansi.org/RecordDetail.aspx?sku=INCITS%2fISO%2fIEC+9899-2012#.UGCvLIHyaHM>)) ([N1570](<https://open-std.org/JTC1/SC22/WG14/www/docs/n1570.pdf>) rascunho de 12 de abril de 2011) 

  1. modelo de memória ciente de threads, [`<stdatomic.h>`](<#/doc/thread>), [`<threads.h>`](<#/doc/thread>), funções genéricas por tipo, alignas/alignof, noreturn, static_assert, extensões de analisabilidade, extensões para tipos complexos e imaginários, structs e unions anônimas, modo de abertura de arquivo exclusivo, [quick_exit](<#/doc/program/quick_exit>)
  2. removeu [gets](<#/doc/io/gets>)
  3. do TR de interfaces de verificação de limites: interfaces de verificação de limites, 
  4. do TR Unicode: char16_t, char32_t, e [`<uchar.h>`](<#/doc/string/multibyte>)

  * 2012: Corrigendum Técnico 1 (ISO/IEC 9899:2011/Cor 1:2012) ([loja ISO](<https://www.iso.org/iso/home/store/catalogue_tc/catalogue_detail.htm?csnumber=61717>)) 

    

  * Corrige [DR 411](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2244.htm#dr_411>)

  * 2013: TS de Regras de Codificação Segura (ISO/IEC TS 17961:2013) ([loja ISO](<https://www.iso.org/iso/catalogue_detail.htm?csnumber=61134>)) ([N1718](<https://open-std.org/JTC1/SC22/WG14/www/docs/n1718.pdf>) 30 de maio de 2013) 
  * 2014: TS FP parte 1: Aritmética de ponto flutuante binário (ISO/IEC TS 18661-1:2014) ([loja ISO](<https://www.iso.org/iso/catalogue_detail.htm?csnumber=63146>)) ([N1778](<https://open-std.org/JTC1/SC22/WG14/www/docs/n1778.pdf>) rascunho de 2013) 

  1. fornece alterações ao C11 (principalmente ao Anexo F) que cobrem todos os requisitos básicos e algumas recomendações da IEC 60559:2011 (C11 foi construído sobre a IEC 60559:1989) 

  * 2015: TS FP parte 2: Aritmética de ponto flutuante decimal (ISO/IEC TS 18661-2:2015) ([loja ISO](<https://www.iso.org/iso/home/store/catalogue_ics/catalogue_detail_ics.htm?csnumber=68882>)) ([N1912](<https://open-std.org/JTC1/SC22/WG14/www/docs/n1912.pdf>) rascunho de 2015) 

  1. fornece alterações ao C11 para suportar todos os requisitos, além de algumas recomendações básicas, da IEC 60559:2011 para aritmética de ponto flutuante decimal. Isso substitui ISO/IEC TR 24732:2009. 

  * 2015: TS FP parte 3: Tipos de intercâmbio e estendidos (ISO/IEC TS 18661-3:2015) ([loja ISO](<https://www.iso.org/iso/home/store/catalogue_tc/catalogue_detail.htm?csnumber=65615>)) ([N1945](<https://open-std.org/JTC1/SC22/WG14/www/docs/n1945.pdf>) rascunho de 2015) 

  1. fornece alterações ao C11 para suportar as recomendações da IEC 60559:2011 para formatos de ponto flutuante estendidos e os formatos de intercâmbio, tanto aritméticos quanto não aritméticos. 

  * 2015: TS FP parte 4: Funções suplementares (ISO/IEC TS 18661-4:2015) ([loja ISO](<https://www.iso.org/iso/home/store/catalogue_tc/catalogue_detail.htm?csnumber=65616>)) ([N1950](<https://open-std.org/JTC1/SC22/WG14/www/docs/n1950.pdf>) rascunho de 2015) 

  1. fornece alterações ao C11 para suportar todas as operações matemáticas recomendadas pela IEC 60559:2011, incluindo trigonometria em unidades de π, raiz quadrada inversa, juros compostos, etc. 

  * 2016: TS FP parte 5: Atributos suplementares (ISO/IEC TS 18661-5:2016) ([loja ISO](<https://www.iso.org/iso/home/store/catalogue_tc/catalogue_detail.htm?csnumber=65617>)) ([N2004](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2004.pdf>) rascunho de 2016) 

  1. fornece alterações ao C11 para suportar todos os atributos suplementares (modelo de avaliação, tratamento de exceções, reprodutibilidade, etc) recomendados pela IEC 60559:2011 

  * 2018: **C17** (ISO/IEC 9899:2018) ([Loja ISO](<https://www.iso.org/standard/74528.html>)) ([Rascunho final](<https://files.lhmouse.com/standards/ISO%20C%20N2176.pdf>)) 

    [Artigo Principal: C17](<#/doc/17>)

Relatórios de Defeitos corrigidos no C17 (54 defeitos)  
---  
  
  * [DR 400](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_400>)
  * [DR 401](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_401>)
  * [DR 402](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_402>)
  * [DR 403](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_403>)
  * [DR 404](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_404>)
  * [DR 405](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_405>)
  * [DR 406](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_406>)
  * [DR 407](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_407>)
  * [DR 410](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_410>)
  * [DR 412](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_412>)
  * [DR 414](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_414>)
  * [DR 415](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_415>)
  * [DR 416](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_416>)
  * [DR 417](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_417>)
  * [DR 419](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_419>)
  * [DR 423](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_423>)
  * [DR 426](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_426>)
  * [DR 428](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_428>)
  * [DR 429](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_429>)
  * [DR 430](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_430>)
  * [DR 431](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_431>)
  * [DR 433](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_433>)
  * [DR 434](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_434>)
  * [DR 436](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_436>)
  * [DR 437](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_437>)
  * [DR 438](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_438>)
  * [DR 439](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_439>)
  * [DR 441](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_441>)
  * [DR 444](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_444>)
  * [DR 445](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_445>)
  * [DR 447](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_447>)
  * [DR 448](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_448>)
  * [DR 450](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_450>)
  * [DR 452](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_452>)
  * [DR 453](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_453>)
  * [DR 457](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_457>)
  * [DR 458](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_458>)
  * [DR 459](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_459>)
  * [DR 460](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_460>)
  * [DR 462](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_462>)
  * [DR 464](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_464>)
  * [DR 465](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_465>)
  * [DR 468](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_468>)
  * [DR 470](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_470>)
  * [DR 471](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_471>)
  * [DR 472](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_472>)
  * [DR 473](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_473>)
  * [DR 475](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_475>)
  * [DR 477](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_477>)
  * [DR 480](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_480>)
  * [DR 481](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_481>)
  * [DR 485](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_485>)
  * [DR 487](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_487>)
  * [DR 491](<http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2244.htm#dr_491>)

  
  
  * 2023 **C23** (ISO/IEC 9899:2024). C23 é a revisão atual do padrão C. 

    [Artigo Principal: C23](<#/doc/23>)

Relatórios de Defeitos corrigidos no C23 (? defeitos)  
---  
  
  * [DR 440](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2379.htm>)
  * [DR 432](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2326.htm>)
  * [DR 467](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2326.htm>)
  * [DR 476](<https://www.open-std.org/jtc1/sc22/wg14/www/docs/n2396.htm#dr_476>)
  * [DR 482](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2324.htm>)
  * [DR 488](<https://www.open-std.org/jtc1/sc22/wg14/www/docs/n2396.htm#dr_488>)
  * [DR 489](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2713.htm>)
  * [DR 494](<https://www.open-std.org/jtc1/sc22/wg14/www/docs/n2396.htm#dr_494>)
  * [DR 496](<https://www.open-std.org/jtc1/sc22/wg14/www/docs/n2396.htm#dr_496>)
  * [DR 497](<https://www.open-std.org/jtc1/sc22/wg14/www/docs/n2396.htm#dr_497>)
  * [DR 499](<https://www.open-std.org/jtc1/sc22/wg14/www/docs/n2396.htm#dr_499>)
  * [DR 500](<https://www.open-std.org/jtc1/sc22/wg14/www/docs/n2396.htm#dr_500>)
  * [DR 501](<https://www.open-std.org/jtc1/sc22/wg14/www/docs/n2396.htm#dr_501>)

  
  
### Desenvolvimento futuro

  * TS de Paralelismo (Rascunho [N2017](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2017.pdf>) 2016-03-10) 
  * TS de Memória Transacional (Rascunho [N1961](<https://open-std.org/JTC1/SC22/WG14/www/docs/n1961.pdf>) 2015-09-23) 
  * **C** (Último rascunho [n3435](<https://open-std.org/JTC1/SC22/WG14/www/docs/n3435.pdf>) 2025-01-03) 

  1. Lista de problemas que não receberam status de DR: ([N2556](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2556.pdf>) 2020-08-02) 

    [Artigo Principal: C29](<https://en.cppreference.com/mwiki/index.php?title=c/29&action=edit&redlink=1> "c/29 \(page does not exist\)") ? 
    Próxima revisão principal do padrão da linguagem C 

### Veja também

[documentação C++](<#/>) para Histórico do C++  
---  
  
### Links externos

1.  | [O Desenvolvimento da Linguagem C](<https://www.bell-labs.com/usr/dmr/www/chist.html>) por Dennis M. Ritchie   
2.  | [Justificativa para o padrão C99](<https://www.open-std.org/jtc1/sc22/wg14/www/C99RationaleV5.10.pdf>)