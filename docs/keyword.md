# Palavras-chave C

Esta é uma lista de palavras-chave reservadas em C. Como são usadas pela linguagem, essas palavras-chave não estão disponíveis para redefinição. Como exceção, elas não são consideradas reservadas em [attribute-tokens](<#/doc/language/attributes>)(desde C23)  
  
[`alignas`](<#/doc/keyword/alignas>) (C23)  
[`alignof`](<#/doc/keyword/alignof>) (C23)  
[`auto`](<#/doc/keyword/auto>)  
[`bool`](<#/doc/keyword/bool>) (C23)  
[`break`](<#/doc/keyword/break>)  
[`case`](<#/doc/keyword/case>)  
[`char`](<#/doc/keyword/char>)  
[`const`](<#/doc/keyword/const>)  
[`constexpr`](<#/doc/keyword/constexpr>) (C23)  
[`continue`](<#/doc/keyword/continue>)  
[`default`](<#/doc/keyword/default>)  
[`do`](<#/doc/keyword/do>)  
[`double`](<#/doc/keyword/double>)  
[`else`](<#/doc/keyword/else>)  
[`enum`](<#/doc/keyword/enum>)  
|  [`extern`](<#/doc/keyword/extern>)  
[`false`](<#/doc/keyword/false>) (C23)  
[`float`](<#/doc/keyword/float>)  
[`for`](<#/doc/keyword/for>)  
[`goto`](<#/doc/keyword/goto>)  
[`if`](<#/doc/keyword/if>)  
[`inline`](<#/doc/keyword/inline>) (C99)  
[`int`](<#/doc/keyword/int>)  
[`long`](<#/doc/keyword/long>)  
[`nullptr`](<#/doc/keyword/nullptr>) (C23)  
[`register`](<#/doc/keyword/register>)  
[`restrict`](<#/doc/keyword/restrict>) (C99)  
[`return`](<#/doc/keyword/return>)  
[`short`](<#/doc/keyword/short>)  
[`signed`](<#/doc/keyword/signed>)  
|  [`sizeof`](<#/doc/keyword/sizeof>)  
[`static`](<#/doc/keyword/static>)  
[`static_assert`](<#/doc/keyword/static_assert>) (C23)  
[`struct`](<#/doc/keyword/struct>)  
[`switch`](<#/doc/keyword/switch>)  
[`thread_local`](<#/doc/keyword/thread_local>) (C23)  
[`true`](<#/doc/keyword/true>) (C23)  
[`typedef`](<#/doc/keyword/typedef>)  
[`typeof`](<#/doc/keyword/typeof>) (C23)  
[`typeof_unqual`](<#/doc/keyword/typeof_unqual>) (C23)  
[`union`](<#/doc/keyword/union>)  
[`unsigned`](<#/doc/keyword/unsigned>)  
[`void`](<#/doc/keyword/void>)  
[`volatile`](<#/doc/keyword/volatile>)  
[`while`](<#/doc/keyword/while>)  
|  [`_Alignas`](<#/doc/keyword/_Alignas>) (C11)(obsoleto em C23)  
[`_Alignof`](<#/doc/keyword/_Alignof>) (C11)(obsoleto em C23)  
[`_Atomic`](<#/doc/keyword/_Atomic>) (C11)  
[`_BitInt`](<https://en.cppreference.com/mwiki/index.php?title=c/keyword/_BitInt&action=edit&redlink=1> "c/keyword/ BitInt \(page does not exist\)") (C23)  
[`_Bool`](<#/doc/keyword/_Bool>) (C99)(obsoleto em C23)  
[`_Complex`](<#/doc/keyword/_Complex>) (C99)  
[`_Decimal128`](<#/doc/keyword/_Decimal128>) (C23)  
[`_Decimal32`](<#/doc/keyword/_Decimal32>) (C23)  
[`_Decimal64`](<#/doc/keyword/_Decimal64>) (C23)  
[`_Generic`](<#/doc/keyword/_Generic>) (C11)  
[`_Imaginary`](<#/doc/keyword/_Imaginary>) (C99)  
[`_Noreturn`](<#/doc/keyword/_Noreturn>) (C11)(obsoleto em C23)  
[`_Static_assert`](<#/doc/keyword/_Static_assert>) (C11)(obsoleto em C23)  
[`_Thread_local`](<#/doc/keyword/_Thread_local>) (C11)(obsoleto em C23)  
  
  
As palavras-chave mais comuns que começam com um sublinhado são geralmente usadas através de suas macros de conveniência: 

palavra-chave  | usado como  | definido em   
[`_Alignas`](<#/doc/keyword/_Alignas>) (C11)(obsoleto em C23) | [`alignas`](<#/doc/types>) (removido em C23) | `stdalign.h`  
[`_Alignof`](<#/doc/keyword/_Alignof>) (C11)(obsoleto em C23) | [`alignof`](<#/doc/types>) (removido em C23) | `stdalign.h`  
[`_Atomic`](<#/doc/keyword/_Atomic>) (C11) | [`atomic_bool, atomic_int, ...`](<#/doc/thread>) | `stdatomic.h`  
[`_BitInt`](<https://en.cppreference.com/mwiki/index.php?title=c/keyword/_BitInt&action=edit&redlink=1> "c/keyword/ BitInt \(page does not exist\)") (C23) | (sem macro)  |   
[`_Bool`](<#/doc/keyword/_Bool>) (C99)(obsoleto em C23) | [`bool`](<#/doc/types>) (removido em C23) | `stdbool.h`  
[`_Complex`](<#/doc/keyword/_Complex>) (C99) | [`complex`](<#/doc/numeric/complex/complex>) | `complex.h`  
[`_Decimal128`](<#/doc/keyword/_Decimal128>) (C23) | (sem macro)  |   
[`_Decimal32`](<#/doc/keyword/_Decimal32>) (C23) | (sem macro)  |   
[`_Decimal64`](<#/doc/keyword/_Decimal64>) (C23) | (sem macro)  |   
[`_Generic`](<#/doc/keyword/_Generic>) (C11) | (sem macro)  |   
[`_Imaginary`](<#/doc/keyword/_Imaginary>) (C99) | [`imaginary`](<#/doc/numeric/complex/imaginary>) | `complex.h`  
[`_Noreturn`](<#/doc/keyword/_Noreturn>) (C11)(obsoleto em C23) | [`noreturn`](<#/doc/types>) | `stdnoreturn.h`  
[`_Static_assert`](<#/doc/keyword/_Static_assert>) (C11)(obsoleto em C23) | [`static_assert`](<#/doc/error/static_assert>) (removido em C23) | `assert.h`  
[`_Thread_local`](<#/doc/keyword/_Thread_local>) (C11)(obsoleto em C23) | [`thread_local`](<#/doc/thread/thread_local>) (removido em C23) | `threads.h`  
  
Algumas palavras-chave são obsoletas e mantidas como grafias alternativas para fins de compatibilidade. Elas podem ser usadas onde quer que a palavra-chave possa. 

palavra-chave  | grafia alternativa   
`alignas` (C23) | `_Alignas` (C11)(obsoleto em C23)  
`alignof` (C23) | `_Alignof` (C11)(obsoleto em C23)  
`bool` (C23) | `_Bool` (C99)(obsoleto em C23)  
`static_assert` (C23) | `_Static_assert` (C11)(obsoleto em C23)  
`thread_local` (C23) | `_Thread_local` (C11)(obsoleto em C23)  
  
Não é especificado se alguma das grafias dessas palavras-chave, suas formas alternativas, ou `true` e `false` é implementada como uma macro predefinida. 

Cada nome que começa com um sublinhado duplo `__` ou um sublinhado `_` seguido por uma letra maiúscula é reservado: veja [identificador](<#/doc/language/identifier>) para detalhes. 

Note que os dígrafos `<%`, `%>`, `<:`, `:>`, `%:`, e `%:%:` fornecem uma [maneira alternativa de representar tokens padrão](<#/doc/language/operator_alternative>). 

Os seguintes tokens são reconhecidos pelo [pré-processador](<#/doc/preprocessor>) quando usados _dentro_ do contexto de uma diretiva de pré-processador: 

[`if`](<#/doc/preprocessor/conditional>)  
[`elif`](<#/doc/preprocessor/conditional>)  
[`else`](<#/doc/preprocessor/conditional>)  
[`endif`](<#/doc/preprocessor/conditional>)  
|  [`ifdef`](<#/doc/preprocessor/conditional>)  
[`ifndef`](<#/doc/preprocessor/conditional>)  
[`elifdef`](<#/doc/preprocessor/conditional>) (C23)  
[`elifndef`](<#/doc/preprocessor/conditional>) (C23)  
[`define`](<#/doc/preprocessor/replace>)  
[`undef`](<#/doc/preprocessor/replace>)  
|  [`include`](<#/doc/preprocessor/include>)  
[`embed`](<#/doc/preprocessor/embed>) (C23)  
[`line`](<#/doc/preprocessor/line>)  
[`error`](<#/doc/preprocessor/error>)  
[`warning`](<#/doc/preprocessor/error>) (C23)  
[`pragma`](<#/doc/preprocessor/impl>)  
|  [`defined`](<#/doc/preprocessor/conditional>)  
[`__has_include`](<#/doc/preprocessor/include>) (C23)  
[`__has_embed`](<#/doc/preprocessor/embed>) (C23)  
[`__has_c_attribute`](<#/doc/language/attributes>) (C23)  
  
Os seguintes tokens são reconhecidos pelo pré-processador quando usados _fora_ do contexto de uma diretiva de pré-processador: 

[`_Pragma`](<#/doc/preprocessor/impl>) (C99)  
---  
  
As seguintes palavras-chave adicionais são classificadas como extensões e suportadas condicionalmente: 

[`asm`](<#/doc/language/asm>)  
[`fortran`](<#/doc/keyword/fortran>)  
---  
  
### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 6.4.1 Palavras-chave (p: TBD) 

    

  * J.5.9 A palavra-chave fortran (p: TBD) 

    

  * J.5.10 A palavra-chave asm (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 6.4.1 Palavras-chave (p: 42-43) 

    

  * J.5.9 A palavra-chave fortran (p: 422) 

    

  * J.5.10 A palavra-chave asm (p: 422) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 6.4.1 Palavras-chave (p: 58-59) 

    

  * J.5.9 A palavra-chave fortran (p: 580) 

    

  * J.5.10 A palavra-chave asm (p: 580) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 6.4.1 Palavras-chave (p: 50) 

    

  * J.5.9 A palavra-chave fortran (p: 514) 

    

  * J.5.10 A palavra-chave asm (p: 514) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 3.1.1 Palavras-chave 

    

  * G.5.9 A palavra-chave fortran 

    

  * G.5.10 A palavra-chave asm 

### Veja também

[documentação C++](<#/>) para palavras-chave C++  
---