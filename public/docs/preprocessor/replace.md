# Substituindo macros de texto

O pré-processador suporta substituição de macros de texto e substituição de macros de texto tipo função.

### Sintaxe

---
`#define` identifier replacement-list ﻿(opcional) | (1) |
`#define` identifier ﻿`(` parameters `)` replacement-list | (2) |
`#define` identifier ﻿`(` parameters`, ... )` replacement-list | (3) | (desde C99)
`#define` identifier ﻿`( ... )` replacement-list | (4) | (desde C99)
`#undef` identifier | (5) |
---

### Explicação

#### Diretivas #define

As diretivas `#define` definem o identificador como uma macro, ou seja, elas instruem o compilador a substituir todas as ocorrências sucessivas do identificador pela `replacement-list`, que pode ser opcionalmente processada adicionalmente. Se o identificador já estiver definido como qualquer tipo de macro, o programa é malformado, a menos que as definições sejam idênticas.

##### Macros tipo objeto

Macros tipo objeto substituem cada ocorrência de um identificador definido pela `replacement-list`. A versão (1) da diretiva `#define` se comporta exatamente assim.

##### Macros tipo função

Macros tipo função substituem cada ocorrência de um identificador definido pela `replacement-list`, adicionalmente aceitando um número de argumentos, que então substituem as ocorrências correspondentes de quaisquer dos parâmetros na `replacement-list`.

A sintaxe de uma invocação de macro tipo função é similar à sintaxe de uma chamada de função: cada instância do nome da macro seguida por um `(` como o próximo token de pré-processamento introduz a sequência de tokens que é substituída pela `replacement-list`. A sequência é terminada pelo token `)` correspondente, ignorando pares correspondentes de parênteses esquerdo e direito intervenientes.

O número de argumentos deve ser o mesmo que o número de argumentos na definição da macro (`parameters`) ou o programa é malformado. Se o identificador não estiver em notação funcional, ou seja, não tiver parênteses após si, ele não é substituído de forma alguma.

A versão (2) da diretiva `#define` define uma macro tipo função simples.

A versão (3) da diretiva `#define` define uma macro tipo função com número variável de argumentos. Os argumentos adicionais podem ser acessados usando o identificador `__VA_ARGS__`, que é então substituído pelos argumentos fornecidos com o identificador a ser substituído.

A versão (4) da diretiva `#define` define uma macro tipo função com número variável de argumentos, mas sem argumentos regulares. Os argumentos podem ser acessados apenas com o identificador `__VA_ARGS__`, que é então substituído pelos argumentos fornecidos com o identificador a ser substituído.

Para as versões (3,4), a `replacement-list` pode conter a sequência de tokens `__VA_OPT__ (` content `)`, que é substituída por `content` se `__VA_ARGS__` não for vazio, e expande para nada caso contrário.
```c
    #define F(...) f(0 __VA_OPT__(,) __VA_ARGS__)
    F(a, b, c) // replaced by f(0, a, b, c)
    F()        // replaced by f(0)
    
    #define G(X, ...) f(0, X __VA_OPT__(,) __VA_ARGS__)
    G(a, b, c) // replaced by f(0, a, b, c)
    G(a, )     // replaced by f(0, a)
    G(a)       // replaced by f(0, a)
    
    #define SDEF(sname, ...) S sname __VA_OPT__(= { __VA_ARGS__ })
    SDEF(foo);       // replaced by S foo;
    SDEF(bar, 1, 2); // replaced by S bar = { 1, 2 };
```

| (desde C23)

Nota: se um argumento de uma macro tipo função incluir vírgulas que não são protegidas por pares correspondentes de parênteses esquerdo e direito (como `macro(array[x = y, x + 1])` ou `[atomic_store](<#/doc/atomic/atomic_store>) (p, (struct S){ a, b });`), a vírgula é interpretada como separador de argumento da macro, causando uma falha de compilação devido à incompatibilidade na contagem de argumentos.

#### Operadores # e ##

Em macros tipo função, um operador `#` antes de um identificador na `replacement-list` executa a substituição de parâmetros no identificador e envolve o resultado em aspas, criando efetivamente um literal de string. Além disso, o pré-processador adiciona barras invertidas para escapar as aspas que cercam literais de string embutidos, se houver, e duplica as barras invertidas dentro da string conforme necessário. Todo o espaço em branco inicial e final é removido, e qualquer sequência de espaço em branco no meio do texto (mas não dentro de literais de string embutidos) é colapsada para um único espaço. Esta operação é chamada de "stringificação". Se o resultado da stringificação não for um literal de string válido, o comportamento é indefinido.

Quando `#` aparece antes de `__VA_ARGS__`, todo o `__VA_ARGS__` expandido é envolvido em aspas:
```c
    #define showlist(...) puts(#__VA_ARGS__)
    showlist();            // expands to puts("")
    showlist(1, "x", int); // expands to puts("1, \"x\", int")
```

| (desde C99)

Um operador `##` entre quaisquer dois identificadores sucessivos na `replacement-list` executa a substituição de parâmetros nos dois identificadores e então concatena o resultado. Esta operação é chamada de "concatenação" ou "colagem de tokens". Apenas tokens que formam um token válido juntos podem ser colados: identificadores que formam um identificador mais longo, dígitos que formam um número, ou operadores `+` e `=` que formam um `+=`. Um comentário não pode ser criado colando `/` e `*` porque os comentários são removidos do texto antes que a substituição de macro seja considerada. Se o resultado da concatenação não for um token válido, o comportamento é indefinido.

Nota: Alguns compiladores oferecem uma extensão que permite que `##` apareça após uma vírgula e antes de `__VA_ARGS__`, caso em que `##` não faz nada quando `__VA_ARGS__` não é vazio, mas remove a vírgula quando `__VA_ARGS__` é vazio: isso torna possível definir macros como `[fprintf](<#/doc/io/fprintf>) ([stderr](<#/doc/io/std_streams>), format, ##__VA_ARGS__)`.

A ordem de avaliação dos operadores `#` e `##` é não especificada.

#### Diretiva #undef

A diretiva `#undef` desdefine o identificador, ou seja, ela cancela a definição anterior do identificador pela diretiva `#define`. Se o identificador não tiver uma macro associada, a diretiva é ignorada.

### Macros predefinidas

Os seguintes nomes de macro são predefinidos em qualquer unidade de tradução:

__STDC__ | expande para a constante inteira 1. Esta macro destina-se a indicar uma implementação conforme
(constante de macro)
__STDC_VERSION__(C95) | expande para uma constante inteira do tipo `long` cujo valor aumenta a cada versão do padrão C:

  * 199409L (C95)
  * 199901L (C99)
  * 201112L (C11)
  * 201710L (C17)
  * 202311L (C23)
(constante de macro)

__STDC_HOSTED__(C99) | expande para a constante inteira 1 se a implementação for hospedada (executa sob um SO), ​0​ se for autônoma (executa sem um SO)
(constante de macro)
__FILE__ | expande para o nome do arquivo atual, como um literal de string de caractere, pode ser alterado pela diretiva `[#line](<#/doc/preprocessor/line>)`
(constante de macro)
__LINE__ | expande para o número da linha do arquivo fonte, uma constante inteira, pode ser alterado pela diretiva `[#line](<#/doc/preprocessor/line>)`
(constante de macro)
__DATE__ | expande para a data de tradução, um literal de string de caractere no formato "Mmm dd yyyy". O nome do mês é como se gerado por `[asctime](<#/doc/chrono/asctime>)` e o primeiro caractere de "dd" é um espaço se o dia do mês for menor que 10
(constante de macro)
__TIME__ | expande para a hora da tradução, um literal de string de caractere no formato "hh:mm:ss", como na hora gerada por `[asctime](<#/doc/chrono/asctime>)()`
(constante de macro)
__STDC_UTF_16__(C23) | expande para 1 para indicar que `char16_t` usa codificação UTF-16
(constante de macro)
__STDC_UTF_32__(C23) | expande para 1 para indicar que `char32_t` usa codificação UTF-32
(constante de macro)
__STDC_EMBED_NOT_FOUND____STDC_EMBED_FOUND____STDC_EMBED_EMPTY__(C23) | expande para ​0​, 1 e 2, respectivamente
(constante de macro)

Os seguintes nomes de macro adicionais podem ser predefinidos por uma implementação:

__STDC_ISO_10646__(C99) | expande para uma constante inteira no formato `yyyymmL`, se `wchar_t` usar Unicode; a data indica a revisão mais recente do Unicode suportada
(constante de macro)
__STDC_IEC_559__(C99) | expande para 1 se IEC 60559 for suportado (obsoleto)(desde C23)
(constante de macro)
__STDC_IEC_559_COMPLEX__(C99) | expande para 1 se aritmética complexa IEC 60559 for suportada (obsoleto)(desde C23)
(constante de macro)
__STDC_UTF_16__(C11) | expande para 1 se `char16_t` usar codificação UTF-16
(constante de macro)
__STDC_UTF_32__(C11) | expande para 1 se `char32_t` usar codificação UTF-32
(constante de macro)
__STDC_MB_MIGHT_NEQ_WC__(C99) | expande para 1 se 'x' == L'x' puder ser falso para um membro do conjunto de caracteres básico, como em sistemas baseados em EBCDIC que usam Unicode para `wchar_t`
(constante de macro)
__STDC_ANALYZABLE__(C11) | expande para 1 se [analisabilidade](<#/doc/language/analyzability>) for suportada
(constante de macro)
__STDC_LIB_EXT1__(C11) | expande para uma constante inteira 201112L se [interfaces de verificação de limites](<#/doc/error>) forem suportadas
(constante de macro)
__STDC_NO_ATOMICS__(C11) | expande para 1 se tipos [atômicos](<#/doc/language/atomic>) e [biblioteca de operações atômicas](<#/doc/thread>) não forem suportados
(constante de macro)
__STDC_NO_COMPLEX__(C11) | expande para 1 se [tipos complexos](<#/doc/language/arithmetic_types>) e [biblioteca matemática complexa](<#/doc/numeric/complex>) não forem suportados
(constante de macro)
__STDC_NO_THREADS__(C11) | expande para 1 se [multithreading](<#/doc/thread>) não for suportado
(constante de macro)
__STDC_NO_VLA__(C11) | expande para 1 se [arrays de tamanho variável](<#/doc/language/array>) e tipos modificados variavelmente (até C23) de duração de armazenamento automática (desde C23) não forem suportados
(constante de macro)
__STDC_IEC_60559_BFP__(C23) | expande para 202311L se aritmética de ponto flutuante binário IEC 60559 for suportada
(constante de macro)
__STDC_IEC_60559_DFP__(C23) | expande para 202311L se aritmética de ponto flutuante decimal IEC 60559 for suportada
(constante de macro)
__STDC_IEC_60559_COMPLEX__(C23) | expande para 202311L se aritmética complexa IEC 60559 for suportada
(constante de macro)
__STDC_IEC_60559_TYPES__(C23) | expande para 202311L se tipos de intercâmbio e estendidos IEC 60559 forem suportados
(constante de macro)

Os valores dessas macros (exceto para `__FILE__` e `__LINE__`) permanecem constantes ao longo da unidade de tradução. Tentativas de redefinir ou desdefinir essas macros resultam em comportamento indefinido.

A variável predefinida `__func__` (veja [definição de função](<#/doc/language/function_definition>) para detalhes) não é uma macro de pré-processador, embora às vezes seja usada junto com `__FILE__` e `__LINE__`, por exemplo, por `[assert](<#/doc/error/assert>)`. | (desde C99)

### Exemplo

Execute este código
```c
    #include <stdio.h>
    
    // make function factory and use it
    #define FUNCTION(name, a) int fun_##name(int x) { return (a) * x; }
    
    FUNCTION(quadruple, 4)
    FUNCTION(double, 2)
    
    #undef FUNCTION
    #define FUNCTION 34
    #define OUTPUT(a) puts( #a )
    
    int main(void)
    {
        printf("quadruple(13): %d\n", fun_quadruple(13) );
        printf("double(21): %d\n", fun_double(21) );
        printf("%d\n", FUNCTION);
        OUTPUT(billion);               // note the lack of quotes
    }
```

Saída:
```
    quadruple(13): 52
    double(21): 42
    34
    billion
```

### Relatórios de defeito

Os seguintes relatórios de defeito que alteram o comportamento foram aplicados retroativamente a padrões C publicados anteriormente.

DR | Aplicado a | Comportamento conforme publicado | Comportamento correto
[DR 321](<https://www.open-std.org/jtc1/sc22/wg14/www/docs/dr_321.htm>) | C99 | não estava claro se L'x' == 'x' sempre se mantém
entre o conjunto de caracteres básico | `__STDC_MB_MIGHT_NEQ_WC__` adicionado para o propósito

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 6.10.4 Substituição de macro (p: 187-184)

    

  * 6.10.9 Nomes de macro predefinidos (p: 186-188)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 6.10.3 Substituição de macro (p: 121-126)

    

  * 6.10.8 Nomes de macro predefinidos (p: 127-129)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 6.10.3 Substituição de macro (p: 166-173)

    

  * 6.10.8 Nomes de macro predefinidos (p: 175-176)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 6.10.3 Substituição de macro (p: 151-158)

    

  * 6.10.8 Nomes de macro predefinidos (p: 160-161)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 3.8.3 Substituição de macro

    

  * 3.8.8 Nomes de macro predefinidos

### Veja também

[documentação C++](<#/>) para Substituindo macros de texto
---