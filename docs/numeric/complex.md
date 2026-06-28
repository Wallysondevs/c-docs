# Aritmética de números complexos

Se a constante de macro `__STDC_NO_COMPLEX__` for definida pela implementação, os tipos complexos, o cabeçalho `<complex.h>` e todos os nomes listados aqui não são fornecidos. | (desde C11)

A linguagem de programação C, a partir do C99, suporta matemática de números complexos com os três tipos embutidos double _Complex, float _Complex e long double _Complex (veja [`_Complex`](<#/>)). Quando o cabeçalho `<complex.h>` é incluído, os três tipos de números complexos também são acessíveis como double [complex](<#/doc/numeric/complex/complex>), float [complex](<#/doc/numeric/complex/complex>), long double [complex](<#/doc/numeric/complex/complex>).

Além dos tipos complexos, os três tipos imaginários podem ser suportados: double _Imaginary, float _Imaginary e long double _Imaginary (veja [`_Imaginary`](<#/doc/keyword/_Imaginary>)). Quando o cabeçalho `<complex.h>` é incluído, os três tipos imaginários também são acessíveis como double [imaginary](<#/doc/numeric/complex/imaginary>), float [imaginary](<#/doc/numeric/complex/imaginary>) e long double [imaginary](<#/doc/numeric/complex/imaginary>).

Operadores aritméticos padrão +, -, *, / podem ser usados com tipos reais, complexos e imaginários em qualquer combinação.

Um compilador que define `__STDC_IEC_559_COMPLEX__` é recomendado, mas não é exigido para suportar números imaginários. POSIX recomenda verificar se a macro [_Imaginary_I](<#/doc/numeric/complex/Imaginary_I>) está definida para identificar o suporte a números imaginários. | (desde C99)
(até C11)
Números imaginários são suportados se `__STDC_IEC_559_COMPLEX__` ou `__STDC_IEC_60559_COMPLEX__`(desde C23) for definido. | (desde C11)
---
Definido no cabeçalho `<complex.h>`

##### Tipos

[ imaginary](<#/doc/numeric/complex/imaginary>)(C99) | macro de tipo imaginário
(macro de palavra-chave)
[ complex](<#/doc/numeric/complex/complex>)(C99) | macro de tipo complexo
(macro de palavra-chave)

##### A constante imaginária

[ _Imaginary_I](<#/doc/numeric/complex/Imaginary_I>)(C99) | a constante da unidade imaginária i
(constante de macro)
[ _Complex_I](<#/doc/numeric/complex/Complex_I>)(C99) | a constante da unidade complexa i
(constante de macro)
[ I](<#/doc/numeric/complex/I>)(C99) | a constante da unidade complexa ou imaginária i
(constante de macro)

##### Manipulação

[ CMPLXCMPLXFCMPLXL](<#/doc/numeric/complex/CMPLX>)(C11)(C11)(C11) | constrói um número complexo a partir de partes real e imaginária
(macro de função)
[ crealcrealfcreall](<#/doc/numeric/complex/creal>)(C99)(C99)(C99) | calcula a parte real de um número complexo
(função)
[ cimagcimagfcimagl](<#/doc/numeric/complex/cimag>)(C99)(C99)(C99) | calcula a parte imaginária de um número complexo
(função)
[ cabscabsfcabsl](<#/doc/numeric/complex/cabs>)(C99)(C99)(C99) | calcula a magnitude de um número complexo
(função)
[ cargcargfcargl](<#/doc/numeric/complex/carg>)(C99)(C99)(C99) | calcula o ângulo de fase de um número complexo
(função)
[ conjconjfconjl](<#/doc/numeric/complex/conj>)(C99)(C99)(C99) | calcula o conjugado complexo
(função)
[ cprojcprojfcprojl](<#/doc/numeric/complex/cproj>)(C99)(C99)(C99) | calcula a projeção na esfera de Riemann
(função)

##### Funções exponenciais

[ cexpcexpfcexpl](<#/doc/numeric/complex/cexp>)(C99)(C99)(C99) | calcula a exponencial complexa de base e
(função)
[ clogclogfclogl](<#/doc/numeric/complex/clog>)(C99)(C99)(C99) | calcula o logaritmo natural complexo
(função)

##### Funções de potência

[ cpowcpowfcpowl](<#/doc/numeric/complex/cpow>)(C99)(C99)(C99) | calcula a função de potência complexa
(função)
[ csqrtcsqrtfcsqrtl](<#/doc/numeric/complex/csqrt>)(C99)(C99)(C99) | calcula a raiz quadrada complexa
(função)

##### Funções trigonométricas

[ csincsinfcsinl](<#/doc/numeric/complex/csin>)(C99)(C99)(C99) | calcula o seno complexo
(função)
[ ccosccosfccosl](<#/doc/numeric/complex/ccos>)(C99)(C99)(C99) | calcula o cosseno complexo
(função)
[ ctanctanfctanl](<#/doc/numeric/complex/ctan>)(C99)(C99)(C99) | calcula a tangente complexa
(função)
[ casincasinfcasinl](<#/doc/numeric/complex/casin>)(C99)(C99)(C99) | calcula o arco seno complexo
(função)
[ cacoscacosfcacosl](<#/doc/numeric/complex/cacos>)(C99)(C99)(C99) | calcula o arco cosseno complexo
(função)
[ catancatanfcatanl](<#/doc/numeric/complex/catan>)(C99)(C99)(C99) | calcula o arco tangente complexo
(função)

##### Funções hiperbólicas

[ csinhcsinhfcsinhl](<#/doc/numeric/complex/csinh>)(C99)(C99)(C99) | calcula o seno hiperbólico complexo
(função)
[ ccoshccoshfccoshl](<#/doc/numeric/complex/ccosh>)(C99)(C99)(C99) | calcula o cosseno hiperbólico complexo
(função)
[ ctanhctanhfctanhl](<#/doc/numeric/complex/ctanh>)(C99)(C99)(C99) | calcula a tangente hiperbólica complexa
(função)
[ casinhcasinhfcasinhl](<#/doc/numeric/complex/casinh>)(C99)(C99)(C99) | calcula o arco seno hiperbólico complexo
(função)
[ cacoshcacoshfcacoshl](<#/doc/numeric/complex/cacosh>)(C99)(C99)(C99) | calcula o arco cosseno hiperbólico complexo
(função)
[ catanhcatanhfcatanhl](<#/doc/numeric/complex/catanh>)(C99)(C99)(C99) | calcula o arco tangente hiperbólico complexo
(função)

### Notas

Os seguintes nomes de função são potencialmente (desde C23) reservados para futura adição a `<complex.h>` e não estão disponíveis para uso em programas que incluem esse cabeçalho: cerf, cerfc, cexp2, cexpm1, clog10, clog1p, clog2, clgamma, ctgamma, csinpi, ccospi, ctanpi, casinpi, cacospi, catanpi, ccompoundn, cpown, cpowr, crootn, crsqrt, cexp10m1, cexp10, cexp2m1, clog10p1, clog2p1, clogp1(desde C23), juntamente com suas variantes sufixadas com -`f` e -`l`.

Embora o padrão C nomeie as funções hiperbólicas inversas como "seno hiperbólico de arco complexo" etc., as funções inversas das funções hiperbólicas são as funções de área. Seu argumento é a área de um setor hiperbólico, não um arco. Os nomes corretos são "seno hiperbólico inverso complexo" etc. Alguns autores usam "seno hiperbólico de área complexa" etc.

Um número complexo ou imaginário é infinito se uma de suas partes for infinita, mesmo que a outra parte seja NaN.

Um número complexo ou imaginário é finito se ambas as partes não forem infinitas nem NaNs.

Um número complexo ou imaginário é um zero se ambas as partes forem zeros positivos ou negativos.

Embora o MSVC forneça um cabeçalho [`<complex.h>`](<https://learn.microsoft.com/en-us/cpp/c-runtime-library/complex-math-support>), ele não implementa números complexos como tipos nativos, mas como structs, que são incompatíveis com os tipos complexos padrão do C e não suportam os operadores +, -, *, /.

### Exemplo

Execute este código
```c
    #include <complex.h>
    #include <stdio.h>
    #include <tgmath.h>
    
    int main(void)
    {
        double complex z1 = I * I;     // imaginary unit squared
        printf("I * I = %.1f%+.1fi\n", creal(z1), cimag(z1));
    
        double complex z2 = pow(I, 2); // imaginary unit squared
        printf("pow(I, 2) = %.1f%+.1fi\n", creal(z2), cimag(z2));
    
        double PI = acos(-1);
        double complex z3 = exp(I * PI); // Euler's formula
        printf("exp(I*PI) = %.1f%+.1fi\n", creal(z3), cimag(z3));
    
        double complex z4 = 1 + 2 * I, z5 = 1 - 2 * I; // conjugates
        printf("(1+2i)*(1-2i) = %.1f%+.1fi\n", creal(z4 * z5), cimag(z4 * z5));
    }
```

Saída:
```
    I * I = -1.0+0.0i
    pow(I, 2) = -1.0+0.0i
    exp(I*PI) = -1.0+0.0i
    (1+2i)*(1-2i) = 5.0+0.0i
```

### Referências

Conteúdo estendido
---

*   Padrão C23 (ISO/IEC 9899:2024):

    *   6.10.8.3/1/2 `__STDC_NO_COMPLEX__` (p: TBD)
    *   6.10.8.3/1/2 `__STDC_IEC_559_COMPLEX__` (p: TBD)
    *   7.3 Aritmética complexa `<complex.h>` (p: TBD)
    *   7.25 Matemática genérica por tipo `<tgmath.h>` (p: TBD)
    *   7.31.1 Aritmética complexa `<complex.h>` (p: TBD)
    *   Anexo G (normativo) Aritmética complexa compatível com IEC 60559 (p: TBD)

*   Padrão C17 (ISO/IEC 9899:2018):

    *   6.10.8.3/1/2 `__STDC_NO_COMPLEX__` (p: 128)
    *   6.10.8.3/1/2 `__STDC_IEC_559_COMPLEX__` (p: 128)
    *   7.3 Aritmética complexa `<complex.h>` (p: 136-144)
    *   7.25 Matemática genérica por tipo `<tgmath.h>` (p: 272-273)
    *   7.31.1 Aritmética complexa `<complex.h>` (p: 391)
    *   Anexo G (normativo) Aritmética complexa compatível com IEC 60559 (p: 469-479)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   6.10.8.3/1/2 `__STDC_NO_COMPLEX__` (p: 177)
    *   6.10.8.3/1/2 `__STDC_IEC_559_COMPLEX__` (p: 177)
    *   7.3 Aritmética complexa `<complex.h>` (p: 188-199)
    *   7.25 Matemática genérica por tipo `<tgmath.h>` (p: 373-375)
    *   7.31.1 Aritmética complexa `<complex.h>` (p: 455)
    *   Anexo G (normativo) Aritmética complexa compatível com IEC 60559 (p: 532-545)

*   Padrão C99 (ISO/IEC 9899:1999):

    *   6.10.8/2 `__STDC_IEC_559_COMPLEX__` (p: 161)
    *   7.3 Aritmética complexa `<complex.h>` (p: 170-180)
    *   7.22 Matemática genérica por tipo `<tgmath.h>` (p: 335-337)
    *   7.26.1 Aritmética complexa `<complex.h>` (p: 401)
    *   Anexo G (informativo) Aritmética complexa compatível com IEC 60559 (p: 467-480)

### Veja também

[Documentação C++](<#/>) para Aritmética de números complexos
---