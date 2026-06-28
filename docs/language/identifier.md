# Identificador

Um _identificador_ é uma sequência arbitrariamente longa de dígitos, sublinhados, letras latinas minúsculas e maiúsculas, e caracteres Unicode especificados usando a notação de [escape](<#/doc/language/escape>) `\u` e `\U` (desde C99), da classe [XID_Continue](<https://www.unicode.org/reports/tr31/#Table_Lexical_Classes_for_Identifiers>)(C23). Um identificador válido deve começar com um caractere não-dígito (letra latina, sublinhado, ou caractere Unicode não-dígito (desde C99)(até C23), ou caractere Unicode da classe [XID_Start](<https://www.unicode.org/reports/tr31/#Table_Lexical_Classes_for_Identifiers>))(C23)). Identificadores diferenciam maiúsculas de minúsculas (letras minúsculas e maiúsculas são distintas). Todo identificador deve estar em conformidade com a [Forma de Normalização C](<https://www.unicode.org/charts/normalization/>).(C23)  
  
É definido pela implementação se caracteres Unicode brutos (não escapados) são permitidos em identificadores: 
```c
    char *\U0001f431 = "cat"; // supported
    char *🐱 = "cat"; // definido pela implementação
                      // (ex: funciona com Clang, mas não com GCC antes da versão 10)
                      // ambos são mal formados em C23. Emojis não são caracteres XID_Start
```

| (desde C99)  
(até C23)  
Caracteres definidos pela implementação cujos pontos de código correspondentes em [ISO/IEC 10646](<https://unicode.org/L2/L2010/10038-fcd10646-main.pdf>) (Unicode) possuem a propriedade XID_Start ou XID_Continue podem aparecer no início ou após o primeiro caractere de um identificador, respectivamente. | (C23)  
  
Identificadores podem denotar os seguintes tipos de entidades: 

  * [objetos](<#/doc/language/object>)
  * [funções](<#/doc/language/functions>)
  * tags ([struct](<#/doc/language/struct>), [union](<#/doc/language/union>), ou [enumerações](<#/doc/language/enum>)) 
  * membros de estrutura ou união 
  * constantes de enumeração 
  * nomes de [typedef](<#/doc/language/typedef>) 
  * nomes de [rótulo](<#/doc/language/statements>) 
  * nomes de [macro](<#/doc/preprocessor/replace>) 
  * nomes de [parâmetro de macro](<#/doc/preprocessor/replace>) 

Todo identificador, exceto nomes de macro ou nomes de parâmetro de macro, possui [escopo](<#/doc/language/scope>), pertence a um [espaço de nomes](<#/doc/language/name_space>), e pode ter [ligação](<#/doc/language/storage_duration>). O mesmo identificador pode denotar entidades diferentes em pontos diferentes do programa, ou pode denotar entidades diferentes no mesmo ponto se as entidades estiverem em espaços de nomes diferentes. 

### Identificadores reservados

Os seguintes identificadores são _reservados_ e não podem ser declarados em um programa (fazer isso invoca comportamento indefinido): 

  1. Os identificadores que são [palavras-chave](<#/doc/keyword>) não podem ser usados para outros propósitos. Em particular, #define ou #undef de um identificador idêntico a uma palavra-chave não é permitido.
  2. Todos os identificadores externos que começam com um sublinhado.
  3. Todos os identificadores que começam com um sublinhado seguido por uma letra maiúscula ou por outro sublinhado (esses identificadores reservados permitem que a biblioteca use inúmeras macros e funções não-externas nos bastidores).
  4. Todos os identificadores externos definidos pela biblioteca padrão (em ambiente hospedado). Isso significa que nenhum nome externo fornecido pelo usuário é permitido corresponder a qualquer nome de biblioteca, nem mesmo se declarar uma função idêntica a uma função de biblioteca.
  5. Identificadores declarados como reservados para a implementação ou uso futuro pela biblioteca padrão (veja abaixo).
  6. Identificadores declarados como potencialmente reservados e fornecidos pela implementação (veja abaixo). (C23)

Todos os outros identificadores estão disponíveis. Identificadores que não são reservados ou potencialmente reservados (C23) podem ser usados sem medo de colisões inesperadas ao mover programas de um compilador e biblioteca para outro. 

Nota: em C++, identificadores com um sublinhado duplo em qualquer lugar são reservados em todos os lugares; em C, apenas aqueles que começam com um sublinhado duplo são reservados. 

#### Identificadores reservados e potencialmente reservados na biblioteca

A biblioteca padrão reserva todo identificador que ela fornece. Identificadores reservados que possuem [ligação externa](<#/doc/language/storage_duration>) (por exemplo, nome de toda função padrão) são reservados independentemente de qual cabeçalho é incluído. Outros identificadores reservados são reservados quando qualquer um de seus cabeçalhos associados é incluído. 

Identificadores potencialmente reservados destinam-se a ser usados pela implementação e por futuras revisões do padrão. Se um identificador potencialmente reservado for fornecido pela implementação, ele se torna reservado. As implementações só podem fornecer [definições externas](<#/doc/language/extern>) de identificadores potencialmente reservados que são reservados como nomes de função. Identificadores potencialmente reservados que não são fornecidos pela implementação não são reservados. Eles podem ser declarados ou definidos pelo usuário sem comportamento indefinido. No entanto, tal uso não é portável. | (C23)  
  
Os seguintes identificadores são reservados ou potencialmente reservados (C23) para a implementação ou uso futuro pela biblioteca padrão. 

  * _nomes de função_ , todos os quais são potencialmente reservados (C23)
    * `cerf`, `cerfc`, `cexp2`, `cexpm1`, `clog10`, `clog1p`, `clog2`, `clgamma`, `ctgamma`, `csinpi`, `ccospi`, `ctanpi`, `casinpi`, `cacospi`, `catanpi`, `ccompoundn`, `cpown`, `cpowr`, `crootn`, `crsqrt`, `cexp10m1`, `cexp10`, `cexp2m1`, `clog10p1`, `clog2p1`, `clogp1`(C23) e suas variantes sufixadas com -f e -l, em [`<complex.h>`](<#/doc/numeric/complex>) (desde C99)
    * começando com `is` ou `to` seguido por uma letra minúscula, em [`<ctype.h>`](<#/doc/string/byte>) e [`<wctype.h>`](<#/doc/string/wide>)(desde C95)
    * começando com `str` ou `wcs`(C23) seguido por uma letra minúscula, em [`<stdlib.h>`](<#/doc/string/byte>) e [`<inttypes.h>`](<#/doc/types/integer>)(C23)
    * começando com `cr_`, em [`<math.h>`](<#/doc/numeric/math>) (C23)
    * começando com `wcs` seguido por uma letra minúscula, em [`<wchar.h>`](<#/doc/string/wide>) (desde C95)
    * começando com `atomic_` seguido por uma letra minúscula, em [`<stdatomic.h>`](<#/doc/thread>) (desde C11)
    * começando com `cnd_`, `mtx_`, `thrd_` ou `tss_` seguido por uma letra minúscula, em [`<threads.h>`](<#/doc/thread>) (desde C11)
  * _nomes de typedef_ , todos os quais são potencialmente reservados (C23)
    * começando com `int` ou `uint` e terminando com `_t`, em [`<stdint.h>`](<#/doc/types/integer>) (desde C99)
    * começando com `atomic_` ou `memory_` seguido por uma letra minúscula, em [`<stdatomic.h>`](<#/doc/thread>) (desde C11)
    * começando com `cnd_`, `mtx_`, `thrd_` ou `tss_` seguido por uma letra minúscula, em [`<threads.h>`](<#/doc/thread>) (desde C11)
  * _nomes de macro_
    * começando com `E` seguido por um dígito ou uma letra maiúscula, em [`<errno.h>`](<#/doc/error/errno_macros>)
    * começando com `FE_` seguido por uma letra maiúscula, em [`<fenv.h>`](<#/doc/numeric/fenv>) (desde C99)
    * começando com `DBL_`, `DEC32_`, `DEC64_`, `DEC128_`, `DEC_`, `FLT_`, ou `LDBL_` seguido por uma letra maiúscula, em [`<float.h>`](<#/doc/types/limits>); esses identificadores são potencialmente reservados (C23)
    * começando com `INT` ou `UINT` e terminando com `_MAX`, `_MIN`, `_WIDTH`(C23), ou `_C`, em [`<stdint.h>`](<#/doc/types/integer>); esses identificadores são potencialmente reservados (C23) (desde C99)
    * começando com `PRI` ou `SCN` seguido por letra minúscula ou a letra `X`, em [`<inttypes.h>`](<#/doc/types/integer>); esses identificadores são potencialmente reservados (C23) (desde C99)
    * começando com `LC_` seguido por uma letra maiúscula, em [`<locale.h>`](<#/doc/locale/LC_categories>)
    * começando com `FP_` seguido por uma letra maiúscula, em [`<math.h>`](<#/doc/numeric/math>) (C23)
    * começando com `MATH_` seguido por uma letra maiúscula, em [`<math.h>`](<#/doc/numeric/math>); esses identificadores são potencialmente reservados (C23)
    * começando com `SIG` ou `SIG_` seguido por uma letra maiúscula, em [`<signal.h>`](<#/doc/program>)
    * começando com `TIME_` seguido por uma letra maiúscula, em [`<time.h>`](<#/doc/chrono/timespec_get>) (desde C11)
    * começando com `ATOMIC_` seguido por uma letra maiúscula, em [`<stdatomic.h>`](<#/doc/thread>); esses identificadores são potencialmente reservados (C23) (desde C11)
  * _constantes de enumeração_ , todas as quais são potencialmente reservadas (C23)
    * começando com `memory_order_` seguido por uma letra minúscula, em [`<stdatomic.h>`](<#/doc/thread>) (desde C11)
    * começando com `cnd_`, `mtx_`, `thrd_` ou `tss_` seguido por uma letra minúscula, em [`<threads.h>`](<#/doc/thread>) (desde C11)

Recomenda-se que as implementações emitam um aviso na declaração ou definição de identificadores potencialmente reservados, exceto quando 

  * a declaração é uma declaração não-definição de um identificador com ligação externa fornecido pela implementação, e 
  * o tipo usado na declaração é [compatível](<#/doc/language/types>) com o usado na definição. 

| (C23)  
  
### Limites de tradução

Embora não haja um limite específico para o comprimento dos identificadores, compiladores antigos tinham limites no número de caracteres iniciais significativos em identificadores e os linkers impunham limites mais rigorosos nos nomes com [ligação externa](<#/doc/language/storage_duration>). C exige que pelo menos os seguintes limites sejam suportados por qualquer implementação em conformidade com o padrão: 

  * 31 caracteres iniciais significativos em um identificador interno ou um nome de macro 
  * 6 caracteres iniciais significativos em um identificador externo 
  * 511 identificadores externos em uma unidade de tradução 
  * 127 identificadores com escopo de bloco declarados em um bloco 
  * 1024 identificadores de macro definidos simultaneamente em uma unidade de tradução de pré-processamento 

| (até C99)  
  
  * 63 caracteres iniciais significativos em um identificador interno ou um nome de macro 
  * 31 caracteres iniciais significativos em um identificador externo 
  * 4095 identificadores externos em uma unidade de tradução 
  * 511 identificadores com escopo de bloco declarados em um bloco 
  * 4095 identificadores de macro definidos simultaneamente em uma unidade de tradução de pré-processamento 

| (desde C99)  
  
### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 5.2.5.2 Limites de tradução (p: TBD) 

    

  * 6.4.2 Identificadores (p: TBD) 

    

  * 6.10.10 Nomes de macro predefinidos (p: TBD) 

    

  * 6.11.7 Nomes de macro predefinidos (p: TBD) 

    

  * 7.33 Direções futuras da biblioteca (p: TBD) 

    

  * K.3.1.2 Identificadores reservados (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 5.2.4.1 Limites de tradução (p: 19-20) 

    

  * 6.4.2 Identificadores (p: 43) 

    

  * 6.10.8 Nomes de macro predefinidos (p: 127-129) 

    

  * 6.11.9 Nomes de macro predefinidos (p: 130) 

    

  * 7.31 Direções futuras da biblioteca (p: 332-333) 

    

  * K.3.1.2 Identificadores reservados (p: 425) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 5.2.4.1 Limites de tradução (p: 25-26) 

    

  * 6.4.2 Identificadores (p: 59-60) 

    

  * 6.10.8 Nomes de macro predefinidos (p: 175-176) 

    

  * 6.11.9 Nomes de macro predefinidos (p: 179) 

    

  * 7.31 Direções futuras da biblioteca (p: 455-457) 

    

  * K.3.1.2 Identificadores reservados (p: 584) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 5.2.4.1 Limites de tradução (p: 20-21) 

    

  * 6.4.2 Identificadores (p: 51-52) 

    

  * 6.10.8 Nomes de macro predefinidos (p: 160-161) 

    

  * 6.11.9 Nomes de macro predefinidos (p: 163) 

    

  * 7.26 Direções futuras da biblioteca (p: 401-402) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 2.2.4.1 Limites de tradução 

    

  * 3.1.2 Identificadores 

    

  * 3.8.8 Nomes de macro predefinidos 

### Veja também

[Documentação C++](<#/>) para Identificadores  
---