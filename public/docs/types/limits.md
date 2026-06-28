# Limites numéricos

### Limites de tipos inteiros
  
##### Limites de tipos inteiros da linguagem principal
  
---  
Definido no cabeçalho `<limits.h>`  
BOOL_WIDTH(C23) | largura em bits de _Bool   
(macro constante)  
CHAR_BIT | largura em bits de um byte   
(macro constante)  
MB_LEN_MAX | número máximo de bytes em um caractere multibyte   
(macro constante)  
CHAR_WIDTH(C23) | largura em bits de char, o mesmo que `CHAR_BIT`   
(macro constante)  
CHAR_MIN | valor mínimo de char   
(macro constante)  
CHAR_MAX | valor máximo de char   
(macro constante)  
SCHAR_WIDTHSHRT_WIDTHINT_WIDTHLONG_WIDTHLLONG_WIDTH(C23)(C23)(C23)(C23)(C23) | largura em bits de signed char, short, int, long e long long, respectivamente   
(macro constante)  
SCHAR_MINSHRT_MININT_MINLONG_MINLLONG_MIN(C99) | valor mínimo de signed char, short, int, long e long long, respectivamente   
(macro constante)  
SCHAR_MAXSHRT_MAXINT_MAXLONG_MAXLLONG_MAX(C99) | valor máximo de signed char, short, int, long e long long, respectivamente   
(macro constante)  
UCHAR_WIDTHUSHRT_WIDTHUINT_WIDTHULONG_WIDTHULLONG_WIDTH(C23)(C23)(C23)(C23)(C23) | largura em bits de unsigned char, unsigned short, unsigned int, unsigned long e unsigned long long, respectivamente   
(macro constante)  
UCHAR_MAXUSHRT_MAXUINT_MAXULONG_MAXULLONG_MAX(C99) | valor máximo de unsigned char, unsigned short, unsigned int,  
unsigned long e unsigned long long, respectivamente   
(macro constante)  
BITINT_MAXWIDTH(C23) | largura máxima N suportada pela declaração de um inteiro de precisão de bits no especificador de tipo _BitInt(N), maior ou igual a `ULLONG_WIDTH`   
(macro constante)  
  
##### Limites de aliases de tipos da biblioteca
  
Definido no cabeçalho `[`<stdint.h>`](<#/doc/types/integer>)`  
PTRDIFF_WIDTH(C23) | largura em bits de objeto do tipo [ptrdiff_t](<#/doc/types/ptrdiff_t>)   
(macro constante)  
PTRDIFF_MIN(C99) | valor mínimo de [ptrdiff_t](<#/doc/types/ptrdiff_t>)   
(macro constante)  
PTRDIFF_MAX(C99) | valor máximo de [ptrdiff_t](<#/doc/types/ptrdiff_t>)   
(macro constante)  
SIZE_WIDTH(C23) | largura em bits de objeto do tipo [size_t](<#/doc/types/size_t>)   
(macro constante)  
SIZE_MAX(C99) | valor máximo de [size_t](<#/doc/types/size_t>)   
(macro constante)  
SIG_ATOMIC_WIDTH(C23) | largura em bits de objeto do tipo [sig_atomic_t](<#/doc/program/sig_atomic_t>)   
(macro constante)  
SIG_ATOMIC_MIN(C99) | valor mínimo de [sig_atomic_t](<#/doc/program/sig_atomic_t>)   
(macro constante)  
SIG_ATOMIC_MAX(C99) | valor máximo de [sig_atomic_t](<#/doc/program/sig_atomic_t>)   
(macro constante)  
WINT_WIDTH(C23) | largura em bits de objeto do tipo wint_t   
(macro constante)  
WINT_MIN(C99) | valor mínimo de `wint_t`   
(macro constante)  
WINT_MAX(C99) | valor máximo de `wint_t`   
(macro constante)  
Definido no cabeçalho `[`<wchar.h>`](<#/doc/string/wide>)`  
Definido no cabeçalho `[`<stdint.h>`](<#/doc/types/integer>)`  
WCHAR_WIDTH(C23) | largura em bits de objeto do tipo wchar_t   
(macro constante)  
WCHAR_MIN(C99) | valor mínimo de wchar_t   
(macro constante)  
WCHAR_MAX(C99) | valor máximo de wchar_t   
(macro constante)  
  
#### Notas

Os tipos dessas constantes, exceto `CHAR_BIT` e `MB_LEN_MAX`, devem corresponder aos resultados das [promoções integrais](<#/doc/language/conversion>) conforme aplicadas a objetos dos tipos que descrevem: `CHAR_MAX` pode ter o tipo int ou unsigned int, mas nunca char. Da mesma forma, `USHRT_MAX` pode não ser de um tipo unsigned: seu tipo pode ser int. 

Uma implementação *freestanding* pode não possuir os nomes de tipo [sig_atomic_t](<#/doc/program/sig_atomic_t>) e/ou wint_t, caso em que as macros `SIG_ATOMIC_*` e/ou `WINT_*` estarão correspondentemente ausentes. 

#### Exemplo

Execute este código
```c
    #include <limits.h>
    #include <stdint.h>
    #include <stdio.h>
    
    int main(void)
    {
        printf("CHAR_BIT       = %d\n", CHAR_BIT);
        printf("MB_LEN_MAX     = %d\n\n", MB_LEN_MAX);
    
        printf("CHAR_MIN       = %+d\n", CHAR_MIN);
        printf("CHAR_MAX       = %+d\n", CHAR_MAX);
        printf("SCHAR_MIN      = %+d\n", SCHAR_MIN);
        printf("SCHAR_MAX      = %+d\n", SCHAR_MAX);
        printf("UCHAR_MAX      = %u\n\n", UCHAR_MAX);
    
        printf("SHRT_MIN       = %+d\n", SHRT_MIN);
        printf("SHRT_MAX       = %+d\n", SHRT_MAX);
        printf("USHRT_MAX      = %u\n\n", USHRT_MAX);
    
        printf("INT_MIN        = %+d\n", INT_MIN);
        printf("INT_MAX        = %+d\n", INT_MAX);
        printf("UINT_MAX       = %u\n\n", UINT_MAX);
    
        printf("LONG_MIN       = %+ld\n", LONG_MIN);
        printf("LONG_MAX       = %+ld\n", LONG_MAX);
        printf("ULONG_MAX      = %lu\n\n", ULONG_MAX);
    
        printf("LLONG_MIN      = %+lld\n", LLONG_MIN);
        printf("LLONG_MAX      = %+lld\n", LLONG_MAX);
        printf("ULLONG_MAX     = %llu\n\n", ULLONG_MAX);
    
        printf("PTRDIFF_MIN    = %td\n", PTRDIFF_MIN);
        printf("PTRDIFF_MAX    = %+td\n", PTRDIFF_MAX);
        printf("SIZE_MAX       = %zu\n", SIZE_MAX);
        printf("SIG_ATOMIC_MIN = %+jd\n",((intmax_t)SIG_ATOMIC_MIN));
        printf("SIG_ATOMIC_MAX = %+jd\n",((intmax_t)SIG_ATOMIC_MAX));
        printf("WCHAR_MIN      = %+jd\n",((intmax_t)WCHAR_MIN));
        printf("WCHAR_MAX      = %+jd\n",((intmax_t)WCHAR_MAX));
        printf("WINT_MIN       = %jd\n", ((intmax_t)WINT_MIN));
        printf("WINT_MAX       = %jd\n", ((intmax_t)WINT_MAX));
    }
```

Saída possível: 
```
    CHAR_BIT       = 8
    MB_LEN_MAX     = 16
    
    CHAR_MIN       = -128
    CHAR_MAX       = +127
    SCHAR_MIN      = -128
    SCHAR_MAX      = +127
    UCHAR_MAX      = 255
    
    SHRT_MIN       = -32768
    SHRT_MAX       = +32767
    USHRT_MAX      = 65535
    
    INT_MIN        = -2147483648
    INT_MAX        = +2147483647
    UINT_MAX       = 4294967295
    
    LONG_MIN       = -9223372036854775808
    LONG_MAX       = +9223372036854775807
    ULONG_MAX      = 18446744073709551615
    
    LLONG_MIN      = -9223372036854775808
    LLONG_MAX      = +9223372036854775807
    ULLONG_MAX     = 18446744073709551615
    
    PTRDIFF_MIN    = -9223372036854775808
    PTRDIFF_MAX    = +9223372036854775807
    SIZE_MAX       = 18446744073709551615
    SIG_ATOMIC_MIN = -2147483648
    SIG_ATOMIC_MAX = +2147483647
    WCHAR_MIN      = -2147483648
    WCHAR_MAX      = +2147483647
    WINT_MIN       = 0
    WINT_MAX       = 4294967295
```

### Limites de tipos de ponto flutuante

Definido no cabeçalho `[`<float.h>`](<#/doc/types/limits>)`  
---  
FLT_RADIX | a base (base inteira) usada pela representação de todos os três tipos de ponto flutuante   
(macro constante)  
DECIMAL_DIG(C99) | a conversão de long double para decimal com pelo menos `DECIMAL_DIG` dígitos e de volta para long double é a conversão de identidade: esta é a precisão decimal necessária para serializar/desserializar um long double   
(macro constante)  
FLT_DECIMAL_DIGDBL_DECIMAL_DIGLDBL_DECIMAL_DIG(C11) | a conversão de float/double/long double para decimal com pelo menos `FLT_DECIMAL_DIG`/`DBL_DECIMAL_DIG`/`LDBL_DECIMAL_DIG` dígitos e de volta é a conversão de identidade: esta é a precisão decimal necessária para serializar/desserializar um valor de ponto flutuante. Definido para pelo menos 6, 10 e 10, respectivamente, ou 9 para float IEEE e 17 para double IEEE (veja também o análogo em C++: [`max_digits10`](<#/>))   
(macro constante)  
FLT_MINDBL_MINLDBL_MIN | valor mínimo, normalizado e positivo de float, double e long double, respectivamente   
(macro constante)  
FLT_TRUE_MINDBL_TRUE_MINLDBL_TRUE_MIN(C11) | valor positivo mínimo de float, double e long double, respectivamente   
(macro constante)  
FLT_MAXDBL_MAXLDBL_MAX | valor finito máximo de float, double e long double, respectivamente   
(macro constante)  
FLT_EPSILONDBL_EPSILONLDBL_EPSILON | diferença de valor absoluto entre 1.0 e o próximo valor representável para float, double e long double, respectivamente   
(macro constante)  
FLT_DIGDBL_DIGLDBL_DIG | número de dígitos decimais que são garantidos serem preservados em uma viagem de ida e volta texto → float/double/long double → texto sem alteração devido a arredondamento ou estouro (veja o análogo em C++ [`digits10`](<#/>) para detalhes)   
(macro constante)  
FLT_MANT_DIGDBL_MANT_DIGLDBL_MANT_DIG | número de dígitos de base-`FLT_RADIX` que estão na mantissa de ponto flutuante e que podem ser representados sem perda de precisão para float, double e long double, respectivamente   
(macro constante)  
FLT_MIN_EXPDBL_MIN_EXPLDBL_MIN_EXP | menor inteiro negativo tal que `FLT_RADIX` elevado à potência um a menos que esse inteiro é um float, double e long double normalizado, respectivamente   
(macro constante)  
FLT_MIN_10_EXPDBL_MIN_10_EXPLDBL_MIN_10_EXP | menor inteiro negativo tal que 10 elevado a essa potência é um float, double e long double normalizado, respectivamente   
(macro constante)  
FLT_MAX_EXPDBL_MAX_EXPLDBL_MAX_EXP | maior inteiro positivo tal que `FLT_RADIX` elevado à potência um a menos que esse inteiro é um float, double e long double finito representável, respectivamente   
(macro constante)  
FLT_MAX_10_EXPDBL_MAX_10_EXPLDBL_MAX_10_EXP | maior inteiro positivo tal que 10 elevado a essa potência é um float, double e long double finito representável, respectivamente   
(macro constante)  
[ FLT_ROUNDS](<#/doc/types/limits/FLT_ROUNDS>) | modo de arredondamento da aritmética de ponto flutuante   
(macro constante)  
[ FLT_EVAL_METHOD](<#/doc/types/limits/FLT_EVAL_METHOD>)(C99) | especifica em qual precisão todas as operações aritméticas são realizadas   
(macro constante)  
FLT_HAS_SUBNORMDBL_HAS_SUBNORMLDBL_HAS_SUBNORM(C11)(obsoleto em C23) | se o tipo suporta números subnormais ([denormais](<https://en.wikipedia.org/wiki/Denormal_number> "enwiki:Denormal number")):  
-1 – indeterminável, ​0​ – ausente, 1 – presente   
(macro constante)  
  
#### Exemplo

Execute este código
```c
    #include <float.h>
    #include <math.h>
    #include <stdio.h>
    
    int main(void)
    {
        printf("DECIMAL_DIG     = %d\n", DECIMAL_DIG);
        printf("FLT_DECIMAL_DIG = %d\n", FLT_DECIMAL_DIG);
        printf("FLT_RADIX       = %d\n", FLT_RADIX);
        printf("FLT_MIN         = %e\n", FLT_MIN);
        printf("FLT_MAX         = %e\n", FLT_MAX);
        printf("FLT_EPSILON     = %e\n", FLT_EPSILON);
        printf("FLT_DIG         = %d\n", FLT_DIG);
        printf("FLT_MANT_DIG    = %d\n", FLT_MANT_DIG);
        printf("FLT_MIN_EXP     = %d\n", FLT_MIN_EXP);
        printf("FLT_MIN_10_EXP  = %d\n", FLT_MIN_10_EXP);
        printf("FLT_MAX_EXP     = %d\n", FLT_MAX_EXP);
        printf("FLT_MAX_10_EXP  = %d\n", FLT_MAX_10_EXP);
        printf("FLT_ROUNDS      = %d\n", FLT_ROUNDS);
        printf("FLT_EVAL_METHOD = %d\n", FLT_EVAL_METHOD);
        printf("FLT_HAS_SUBNORM = %d\n", FLT_HAS_SUBNORM);
    }
```

Saída possível: 
```
    DECIMAL_DIG     = 37
    FLT_DECIMAL_DIG = 9
    FLT_RADIX       = 2
    FLT_MIN         = 1.175494e-38
    FLT_MAX         = 3.402823e+38
    FLT_EPSILON     = 1.192093e-07
    FLT_DIG         = 6
    FLT_MANT_DIG    = 24
    FLT_MIN_EXP     = -125
    FLT_MIN_10_EXP  = -37
    FLT_MAX_EXP     = 128
    FLT_MAX_10_EXP  = 38
    FLT_ROUNDS      = 1
    FLT_EVAL_METHOD = 1
    FLT_HAS_SUBNORM = 1
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 5.2.4.2 Limites numéricos (p: TBD) 

    

  * 7.22.3 Limites de outros tipos inteiros (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 5.2.4.2 Limites numéricos (p: 20-27) 

    

  * 7.20.3 Limites de outros tipos inteiros (p: 215-216) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 5.2.4.2 Limites numéricos (p: 26-34) 

    

  * 7.20.3 Limites de outros tipos inteiros (p: 293-294) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 5.2.4.2 Limites numéricos (p: 21-28) 

    

  * 7.18.3 Limites de outros tipos inteiros (p: 259-260) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 2.2.4.2 Limites numéricos 

### Veja também

[documentação C++](<#/>) para a interface de limites numéricos de C  
---