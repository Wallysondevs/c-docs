# Cabeçalhos da Biblioteca Padrão C

A interface da biblioteca padrão C é definida pela seguinte coleção de cabeçalhos.

[`<assert.h>`](<#/doc/error>) | [Macro compilada condicionalmente que compara seu argumento a zero](<#/doc/error>)
[`<complex.h>`](<#/doc/numeric/complex>) (desde C99) | [Aritmética de números complexos](<#/doc/numeric/complex>)
[`<ctype.h>`](<#/doc/string/byte>) | [Funções para determinar o tipo contido em dados de caractere](<#/doc/string/byte>)
[`<errno.h>`](<#/doc/error>) | [Macros que reportam condições de erro](<#/doc/error>)
[`<fenv.h>`](<#/doc/numeric/fenv>) (desde C99) | [Ambiente de ponto flutuante](<#/doc/numeric/fenv>)
[`<float.h>`](<#/doc/types/limits>) | [Limites de tipos de ponto flutuante](<#/doc/types/limits>)
[`<inttypes.h>`](<#/doc/types/integer>) (desde C99) | [Conversão de formato de tipos inteiros](<#/doc/types/integer>)
[`<iso646.h>`](<#/doc/language/operator_alternative>) (desde C95) | [Grafias alternativas de operadores](<#/doc/language/operator_alternative>)
[`<limits.h>`](<#/doc/types/limits>) | [Intervalos de tipos inteiros](<#/doc/types/limits>)
[`<locale.h>`](<#/doc/locale>) | [Utilitários de localização](<#/doc/locale>)
[`<math.h>`](<#/doc/numeric/math>) | [Funções matemáticas comuns](<#/doc/numeric/math>)
[`<setjmp.h>`](<#/doc/program>) | [Saltos não locais](<#/doc/program>)
[`<signal.h>`](<#/doc/program>) | [Tratamento de sinais](<#/doc/program>)
[`<stdalign.h>`](<#/doc/types>) (desde C11)(obsoleto em C23) | Macros de conveniência [`alignas` e `alignof`](<#/doc/types>)
[`<stdarg.h>`](<#/doc/variadic>) | [Argumentos variáveis](<#/doc/variadic>)
[`<stdatomic.h>`](<#/doc/thread>) (desde C11) | [Operações atômicas](<#/doc/thread>)
[`<stdbit.h>`](<#/doc/numeric>) (desde C23) | [Macros para trabalhar com as representações de byte e bit de tipos](<#/doc/numeric>)
[`<stdbool.h>`](<#/doc/types>) (desde C99)(obsoleto em C23) | [Macros para tipo booleano](<#/doc/types>)
[`<stdckdint.h>`](<#/doc/numeric>) (desde C23) | [Macros para realizar aritmética inteira verificada](<#/doc/numeric>)
[`<stddef.h>`](<#/doc/types>) | [Definições de macro comuns](<#/doc/types>)
[`<stdint.h>`](<#/doc/types/integer>) (desde C99) | [Tipos inteiros de largura fixa](<#/doc/types/integer>)
[`<stdio.h>`](<#/doc/io>) | [Entrada/saída](<#/doc/io>)
[`<stdlib.h>`](<#/doc/program>) | Utilitários gerais: [gerenciamento de memória](<#/doc/memory>), [utilitários de programa](<#/doc/program>), [conversões de string](<#/doc/string>), [números aleatórios](<#/doc/numeric/random>), [algoritmos](<#/doc/algorithm>)
`<stdmchar.h>` (desde C29) | Transcodificação de texto
[`<stdnoreturn.h>`](<#/doc/language/_Noreturn>) (desde C11)(obsoleto em C23) | Macro de conveniência [`noreturn`](<#/doc/language/_Noreturn>)
[`<string.h>`](<#/doc/string/byte>) | [Manipulação de strings](<#/doc/string/byte>)
[`<tgmath.h>`](<#/doc/numeric/tgmath>) (desde C99) | [Matemática genérica por tipo](<#/doc/numeric/tgmath>) (macros que envolvem math.h e complex.h)
[`<threads.h>`](<#/doc/thread>) (desde C11) | [Biblioteca de threads](<#/doc/thread>)
[`<time.h>`](<#/doc/chrono>) | [Utilitários de tempo/data](<#/doc/chrono>)
[`<uchar.h>`](<#/doc/string/multibyte>) (desde C11) | [Utilitários de caracteres UTF-16 e UTF-32](<#/doc/string/multibyte>)
[`<wchar.h>`](<#/doc/string/wide>) (desde C95) | [Utilitários estendidos de caracteres multibyte e wide](<#/doc/string/wide>)
[`<wctype.h>`](<#/doc/string/wide>) (desde C95) | [Funções para determinar o tipo contido em dados de caracteres wide](<#/doc/string/wide>)

### Macros de teste de recurso (desde C23)

As macros de teste de recurso são definidas nos cabeçalhos correspondentes, respectivamente, desde C23. Note que nem todos os cabeçalhos contêm tal macro.

# | Header | Macro name | Value
1 | [`<assert.h>`](<#/doc/error>) | __STDC_VERSION_ASSERT_H__ | 202311L
2 | [`<complex.h>`](<#/doc/numeric/complex>) | __STDC_VERSION_COMPLEX_H__ | 202311L
3 | [`<ctype.h>`](<#/doc/string/byte>) | N/A
4 | [`<errno.h>`](<#/doc/error>) | N/A
5 | [`<fenv.h>`](<#/doc/numeric/fenv>) | __STDC_VERSION_FENV_H__ | 202311L
6 | [`<float.h>`](<#/doc/types/limits>) | __STDC_VERSION_FLOAT_H__ | 202311L
7 | [`<inttypes.h>`](<#/doc/types/integer>) | __STDC_VERSION_INTTYPES_H__ | 202311L
8 | [`<iso646.h>`](<#/doc/language/operator_alternative>) | N/A
9 | [`<limits.h>`](<#/doc/types/limits>) | __STDC_VERSION_LIMITS_H__ | 202311L
10 | [`<locale.h>`](<#/doc/locale>) | N/A
11 | [`<math.h>`](<#/doc/numeric/math>) | __STDC_VERSION_MATH_H__ | 202311L
12 | [`<setjmp.h>`](<#/doc/program>) | __STDC_VERSION_SETJMP_H__ | 202311L
13 | [`<signal.h>`](<#/doc/program>) | N/A
14 | [`<stdalign.h>`](<#/doc/types>) | N/A
15 | [`<stdarg.h>`](<#/doc/variadic>) | __STDC_VERSION_STDARG_H__ | 202311L
16 | [`<stdatomic.h>`](<#/doc/thread>) | __STDC_VERSION_STDATOMIC_H__ | 202311L
17 | [`<stdbit.h>`](<#/doc/numeric>) | __STDC_VERSION_STDBIT_H__ | 202311L
18 | [`<stdbool.h>`](<#/doc/types>) | N/A
19 | [`<stdckdint.h>`](<#/doc/numeric>) | __STDC_VERSION_STDCKDINT_H__ | 202311L
20 | [`<stddef.h>`](<#/doc/types>) | __STDC_VERSION_STDDEF_H__ | 202311L
21 | [`<stdint.h>`](<#/doc/types/integer>) | __STDC_VERSION_STDINT_H__ | 202311L
22 | [`<stdio.h>`](<#/doc/io>) | __STDC_VERSION_STDIO_H__ | 202311L
23 | [`<stdlib.h>`](<#/doc/program>) | __STDC_VERSION_STDLIB_H__ | 202311L
24 | [`<stdnoreturn.h>`](<#/doc/language/_Noreturn>) | N/A
25 | [`<string.h>`](<#/doc/string/byte>) | __STDC_VERSION_STRING_H__ | 202311L
26 | [`<tgmath.h>`](<#/doc/numeric/tgmath>) | __STDC_VERSION_TGMATH_H__ | 202311L
27 | [`<threads.h>`](<#/doc/thread>) | N/A
28 | [`<time.h>`](<#/doc/chrono>) | __STDC_VERSION_TIME_H__ | 202311L
29 | [`<uchar.h>`](<#/doc/string/multibyte>) | __STDC_VERSION_UCHAR_H__ | 202311L
30 | [`<wchar.h>`](<#/doc/string/wide>) | __STDC_VERSION_WCHAR_H__ | 202311L
31 | [`<wctype.h>`](<#/doc/string/wide>) | N/A

### Referências

*   Padrão C23 (ISO/IEC 9899:2024):

    *   7.1.2 Cabeçalhos padrão

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.1.2 Cabeçalhos padrão (p: 131-132)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.1.2 Cabeçalhos padrão (p: 181-182)

*   Padrão C99 (ISO/IEC 9899:1999):

    *   7.1.2 Cabeçalhos padrão (p: 165)

*   Padrão C89/C90 (ISO/IEC 9899:1990):

    *   4.1.2 Cabeçalhos padrão

### Veja também

[Documentação C++](<#/>) para cabeçalhos da Biblioteca Padrão C++
---