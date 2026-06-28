# Matemática genérica por tipo

O cabeçalho `<tgmath.h>` inclui os cabeçalhos [`<math.h>`](<#/doc/numeric/math>) e [`<complex.h>`](<#/doc/numeric/complex>) e define várias macros genéricas por tipo que determinam qual função real ou, quando aplicável, complexa chamar com base nos tipos dos argumentos.
  
Para cada macro, os parâmetros cujo tipo real correspondente na função math.h sem sufixo é double são conhecidos como _parâmetros genéricos_ (por exemplo, ambos os parâmetros de [pow](<#/doc/numeric/math/pow>) são parâmetros genéricos, mas apenas o primeiro parâmetro de [scalbn](<#/doc/numeric/math/scalbn>) é um parâmetro genérico).

Quando uma macro `<tgmath.h>` é usada, os tipos dos argumentos passados para os parâmetros genéricos determinam qual função é selecionada pela macro, conforme descrito abaixo. Se os tipos dos argumentos não forem [compatíveis](<#/doc/language/compatible_type>) com os tipos de parâmetro da função selecionada, o comportamento é indefinido (por exemplo, se um argumento complexo for passado para uma macro de `<tgmath.h>` que aceita apenas tipos reais: float [complex](<#/doc/numeric/complex/complex>) fc; [ceil](<#/doc/numeric/math/ceil>)(fc); ou double [complex](<#/doc/numeric/complex/complex>) dc; double d; [fmax](<#/doc/numeric/math/fmax>)(dc, d); são exemplos de comportamento indefinido).

Nota: macros genéricas por tipo foram implementadas de maneira definida pela implementação em C99, mas a palavra-chave [`_Generic`](<#/doc/keyword/_Generic>) do C11 torna possível implementar essas macros de maneira portável.

### Macros genéricas por tipo complexo/real

Para todas as funções que possuem contrapartes reais e complexas, existe uma macro genérica por tipo `XXX`, que chama uma das seguintes:

  * função real:

    

  * variante float `XXXf`
  * variante double `XXX`
  * variante long double `XXXl`

  * função complexa:

    

  * variante float `cXXXf`
  * variante double `cXXX`
  * variante long double `cXXXl`

Uma exceção à regra acima é a macro `fabs` (veja a tabela abaixo).

A função a ser chamada é determinada da seguinte forma:

  * Se qualquer um dos argumentos para os parâmetros genéricos for imaginário, o comportamento é especificado individualmente em cada página de referência da função (em particular, `sin`, `cos`, `tag`, `cosh`, `sinh`, `tanh`, `asin`, `atan`, `asinh` e `atanh` chamam funções _reais_, os tipos de retorno de `sin`, `tan`, `sinh`, `tanh`, `asin`, `atan`, `asinh` e `atanh` são imaginários, e os tipos de retorno de `cos` e `cosh` são reais).
  * Se qualquer um dos argumentos para os parâmetros genéricos for complexo, então a função complexa é chamada; caso contrário, a função real é chamada.
  * Se qualquer um dos argumentos para os parâmetros genéricos for long double, então a variante long double é chamada. Caso contrário, se qualquer um dos parâmetros for double ou inteiro, então a variante double é chamada. Caso contrário, a variante float é chamada.

As macros genéricas por tipo são as seguintes:

Macro genérica   
por tipo  | Variantes de função   
real  | Variantes de função   
complexa   
|  float |  double |  long double |  float |  double |  long double  
fabs  | [`fabsf`](<#/doc/numeric/math/fabs>) | [`fabs`](<#/doc/numeric/math/fabs>) | [`fabsl`](<#/doc/numeric/math/fabs>) | [`cabsf`](<#/doc/numeric/complex/cabs>) | [`cabs`](<#/doc/numeric/complex/cabs>) | [`cabsl`](<#/doc/numeric/complex/cabs>)  
exp  | [`expf`](<#/doc/numeric/math/exp>) | [`exp`](<#/doc/numeric/math/exp>) | [`expl`](<#/doc/numeric/math/exp>) | [`cexpf`](<#/doc/numeric/complex/cexp>) | [`cexp`](<#/doc/numeric/complex/cexp>) | [`cexpl`](<#/doc/numeric/complex/cexp>)  
log  | [`logf`](<#/doc/numeric/math/log>) | [`log`](<#/doc/numeric/math/log>) | [`logl`](<#/doc/numeric/math/log>) | [`clogf`](<#/doc/numeric/complex/clog>) | [`clog`](<#/doc/numeric/complex/clog>) | [`clogl`](<#/doc/numeric/complex/clog>)  
pow  | [`powf`](<#/doc/numeric/math/pow>) | [`pow`](<#/doc/numeric/math/pow>) | [`powl`](<#/doc/numeric/math/pow>) | [`cpowf`](<#/doc/numeric/complex/cpow>) | [`cpow`](<#/doc/numeric/complex/cpow>) | [`cpowl`](<#/doc/numeric/complex/cpow>)  
sqrt  | [`sqrtf`](<#/doc/numeric/math/sqrt>) | [`sqrt`](<#/doc/numeric/math/sqrt>) | [`sqrtl`](<#/doc/numeric/math/sqrt>) | [`csqrtf`](<#/doc/numeric/complex/csqrt>) | [`csqrt`](<#/doc/numeric/complex/csqrt>) | [`csqrtl`](<#/doc/numeric/complex/csqrt>)  
sin  | [`sinf`](<#/doc/numeric/math/sin>) | [`sin`](<#/doc/numeric/math/sin>) | [`sinl`](<#/doc/numeric/math/sin>) | [`csinf`](<#/doc/numeric/complex/csin>) | [`csin`](<#/doc/numeric/complex/csin>) | [`csinl`](<#/doc/numeric/complex/csin>)  
cos  | [`cosf`](<#/doc/numeric/math/cos>) | [`cos`](<#/doc/numeric/math/cos>) | [`cosl`](<#/doc/numeric/math/cos>) | [`ccosf`](<#/doc/numeric/complex/ccos>) | [`ccos`](<#/doc/numeric/complex/ccos>) | [`ccosl`](<#/doc/numeric/complex/ccos>)  
tan  | [`tanf`](<#/doc/numeric/math/tan>) | [`tan`](<#/doc/numeric/math/tan>) | [`tanl`](<#/doc/numeric/math/tan>) | [`ctanf`](<#/doc/numeric/complex/ctan>) | [`ctan`](<#/doc/numeric/complex/ctan>) | [`ctanl`](<#/doc/numeric/complex/ctan>)  
asin  | [`asinf`](<#/doc/numeric/math/asin>) | [`asin`](<#/doc/numeric/math/asin>) | [`asinl`](<#/doc/numeric/math/asin>) | [`casinf`](<#/doc/numeric/complex/casin>) | [`casin`](<#/doc/numeric/complex/casin>) | [`casinl`](<#/doc/numeric/complex/casin>)  
acos  | [`acosf`](<#/doc/numeric/math/acos>) | [`acos`](<#/doc/numeric/math/acos>) | [`acosl`](<#/doc/numeric/math/acos>) | [`cacosf`](<#/doc/numeric/complex/cacos>) | [`cacos`](<#/doc/numeric/complex/cacos>) | [`cacosl`](<#/doc/numeric/complex/cacos>)  
atan  | [`atanf`](<#/doc/numeric/math/atan>) | [`atan`](<#/doc/numeric/math/atan>) | [`atanl`](<#/doc/numeric/math/atan>) | [`catanf`](<#/doc/numeric/complex/catan>) | [`catan`](<#/doc/numeric/complex/catan>) | [`catanl`](<#/doc/numeric/complex/catan>)  
sinh  | [`sinhf`](<#/doc/numeric/math/sinh>) | [`sinh`](<#/doc/numeric/math/sinh>) | [`sinhl`](<#/doc/numeric/math/sinh>) | [`csinhf`](<#/doc/numeric/complex/csinh>) | [`csinh`](<#/doc/numeric/complex/csinh>) | [`csinhl`](<#/doc/numeric/complex/csinh>)  
cosh  | [`coshf`](<#/doc/numeric/math/cosh>) | [`cosh`](<#/doc/numeric/math/cosh>) | [`coshl`](<#/doc/numeric/math/cosh>) | [`ccoshf`](<#/doc/numeric/complex/ccosh>) | [`ccosh`](<#/doc/numeric/complex/ccosh>) | [`ccoshl`](<#/doc/numeric/complex/ccosh>)  
tanh  | [`tanhf`](<#/doc/numeric/math/tanh>) | [`tanh`](<#/doc/numeric/math/tanh>) | [`tanhl`](<#/doc/numeric/math/tanh>) | [`ctanhf`](<#/doc/numeric/complex/ctanh>) | [`ctanh`](<#/doc/numeric/complex/ctanh>) | [`ctanhl`](<#/doc/numeric/complex/ctanh>)  
asinh  | [`asinhf`](<#/doc/numeric/math/asinh>) | [`asinh`](<#/doc/numeric/math/asinh>) | [`asinhl`](<#/doc/numeric/math/asinh>) | [`casinhf`](<#/doc/numeric/complex/casinh>) | [`casinh`](<#/doc/numeric/complex/casinh>) | [`casinhl`](<#/doc/numeric/complex/casinh>)  
acosh  | [`acoshf`](<#/doc/numeric/math/acosh>) | [`acosh`](<#/doc/numeric/math/acosh>) | [`acoshl`](<#/doc/numeric/math/acosh>) | [`cacoshf`](<#/doc/numeric/complex/cacosh>) | [`cacosh`](<#/doc/numeric/complex/cacosh>) | [`cacoshl`](<#/doc/numeric/complex/cacosh>)  
atanh  | [`atanhf`](<#/doc/numeric/math/atanh>) | [`atanh`](<#/doc/numeric/math/atanh>) | [`atanhl`](<#/doc/numeric/math/atanh>) | [`catanhf`](<#/doc/numeric/complex/catanh>) | [`catanh`](<#/doc/numeric/complex/catanh>) | [`catanhl`](<#/doc/numeric/complex/catanh>)  
  
### Funções apenas reais

Para todas as funções que não possuem contrapartes complexas, com exceção de `modf`, existe uma macro genérica por tipo `XXX`, que chama uma das variantes de uma função real:

  * variante float `XXXf`
  * variante double `XXX`
  * variante long double `XXXl`

A função a ser chamada é determinada da seguinte forma:

  * Se qualquer um dos argumentos para os parâmetros genéricos for long double, então a variante long double é chamada. Caso contrário, se qualquer um dos argumentos para os parâmetros genéricos for double, então a variante double é chamada. Caso contrário, a variante float é chamada.

Macro genérica   
por tipo  | Variantes de função   
real   
|  float |  double |  long double  
atan2  | [`atan2f`](<#/doc/numeric/math/atan2>) | [`atan2`](<#/doc/numeric/math/atan2>) | [`atan2l`](<#/doc/numeric/math/atan2>)  
cbrt  | [`cbrtf`](<#/doc/numeric/math/cbrt>) | [`cbrt`](<#/doc/numeric/math/cbrt>) | [`cbrtl`](<#/doc/numeric/math/cbrt>)  
ceil  | [`ceilf`](<#/doc/numeric/math/ceil>) | [`ceil`](<#/doc/numeric/math/ceil>) | [`ceill`](<#/doc/numeric/math/ceil>)  
copysign  | [`copysignf`](<#/doc/numeric/math/copysign>) | [`copysign`](<#/doc/numeric/math/copysign>) | [`copysignl`](<#/doc/numeric/math/copysign>)  
erf  | [`erff`](<#/doc/numeric/math/erf>) | [`erf`](<#/doc/numeric/math/erf>) | [`erfl`](<#/doc/numeric/math/erf>)  
erfc  | [`erfcf`](<#/doc/numeric/math/erfc>) | [`erfc`](<#/doc/numeric/math/erfc>) | [`erfcl`](<#/doc/numeric/math/erfc>)  
exp2  | [`exp2f`](<#/doc/numeric/math/exp2>) | [`exp2`](<#/doc/numeric/math/exp2>) | [`exp2l`](<#/doc/numeric/math/exp2>)  
expm1  | [`expm1f`](<#/doc/numeric/math/expm1>) | [`expm1`](<#/doc/numeric/math/expm1>) | [`expm1l`](<#/doc/numeric/math/expm1>)  
fdim  | [`fdimf`](<#/doc/numeric/math/fdim>) | [`fdim`](<#/doc/numeric/math/fdim>) | [`fdiml`](<#/doc/numeric/math/fdim>)  
floor  | [`floorf`](<#/doc/numeric/math/floor>) | [`floor`](<#/doc/numeric/math/floor>) | [`floorl`](<#/doc/numeric/math/floor>)  
fma  | [`fmaf`](<#/doc/numeric/math/fma>) | [`fma`](<#/doc/numeric/math/fma>) | [`fmal`](<#/doc/numeric/math/fma>)  
fmax  | [`fmaxf`](<#/doc/numeric/math/fmax>) | [`fmax`](<#/doc/numeric/math/fmax>) | [`fmaxl`](<#/doc/numeric/math/fmax>)  
fmin  | [`fminf`](<#/doc/numeric/math/fmin>) | [`fmin`](<#/doc/numeric/math/fmin>) | [`fminl`](<#/doc/numeric/math/fmin>)  
fmod  | [`fmodf`](<#/doc/numeric/math/fmod>) | [`fmod`](<#/doc/numeric/math/fmod>) | [`fmodl`](<#/doc/numeric/math/fmod>)  
frexp  | [`frexpf`](<#/doc/numeric/math/frexp>) | [`frexp`](<#/doc/numeric/math/frexp>) | [`frexpl`](<#/doc/numeric/math/frexp>)  
hypot  | [`hypotf`](<#/doc/numeric/math/hypot>) | [`hypot`](<#/doc/numeric/math/hypot>) | [`hypotl`](<#/doc/numeric/math/hypot>)  
ilogb  | [`ilogbf`](<#/doc/numeric/math/ilogb>) | [`ilogb`](<#/doc/numeric/math/ilogb>) | [`ilogbl`](<#/doc/numeric/math/ilogb>)  
ldexp  | [`ldexpf`](<#/doc/numeric/math/ldexp>) | [`ldexp`](<#/doc/numeric/math/ldexp>) | [`ldexpl`](<#/doc/numeric/math/ldexp>)  
lgamma  | [`lgammaf`](<#/doc/numeric/math/lgamma>) | [`lgamma`](<#/doc/numeric/math/lgamma>) | [`lgammal`](<#/doc/numeric/math/lgamma>)  
llrint  | [`llrintf`](<#/doc/numeric/math/rint>) | [`llrint`](<#/doc/numeric/math/rint>) | [`llrintl`](<#/doc/numeric/math/rint>)  
llround  | [`llroundf`](<#/doc/numeric/math/round>) | [`llround`](<#/doc/numeric/math/round>) | [`llroundl`](<#/doc/numeric/math/round>)  
log10  | [`log10f`](<#/doc/numeric/math/log10>) | [`log10`](<#/doc/numeric/math/log10>) | [`log10l`](<#/doc/numeric/math/log10>)  
log1p  | [`log1pf`](<#/doc/numeric/math/log1p>) | [`log1p`](<#/doc/numeric/math/log1p>) | [`log1pl`](<#/doc/numeric/math/log1p>)  
log2  | [`log2f`](<#/doc/numeric/math/log2>) | [`log2`](<#/doc/numeric/math/log2>) | [`log2l`](<#/doc/numeric/math/log2>)  
logb  | [`logbf`](<#/doc/numeric/math/logb>) | [`logb`](<#/doc/numeric/math/logb>) | [`logbl`](<#/doc/numeric/math/logb>)  
lrint  | [`lrintf`](<#/doc/numeric/math/rint>) | [`lrint`](<#/doc/numeric/math/rint>) | [`lrintl`](<#/doc/numeric/math/rint>)  
lround  | [`lroundf`](<#/doc/numeric/math/round>) | [`lround`](<#/doc/numeric/math/round>) | [`lroundl`](<#/doc/numeric/math/round>)  
nearbyint  | [`nearbyintf`](<#/doc/numeric/math/nearbyint>) | [`nearbyint`](<#/doc/numeric/math/nearbyint>) | [`nearbyintl`](<#/doc/numeric/math/nearbyint>)  
nextafter  | [`nextafterf`](<#/doc/numeric/math/nexttoward>) | [`nextafter`](<#/doc/numeric/math/nexttoward>) | [`nextafterl`](<#/doc/numeric/math/nexttoward>)  
nexttoward  | [`nexttowardf`](<#/doc/numeric/math/nexttoward>) | [`nexttoward`](<#/doc/numeric/math/nexttoward>) | [`nexttowardl`](<#/doc/numeric/math/nexttoward>)  
remainder  | [`remainderf`](<#/doc/numeric/math/remainder>) | [`remainder`](<#/doc/numeric/math/remainder>) | [`remainderl`](<#/doc/numeric/math/remainder>)  
remquo  | [`remquof`](<#/doc/numeric/math/remquo>) | [`remquo`](<#/doc/numeric/math/remquo>) | [`remquol`](<#/doc/numeric/math/remquo>)  
rint  | [`rintf`](<#/doc/numeric/math/rint>) | [`rint`](<#/doc/numeric/math/rint>) | [`rintl`](<#/doc/numeric/math/rint>)  
round  | [`roundf`](<#/doc/numeric/math/round>) | [`round`](<#/doc/numeric/math/round>) | [`roundl`](<#/doc/numeric/math/round>)  
scalbln  | [`scalblnf`](<#/doc/numeric/math/scalbn>) | [`scalbln`](<#/doc/numeric/math/scalbn>) | [`scalblnl`](<#/doc/numeric/math/scalbn>)  
scalbn  | [`scalbnf`](<#/doc/numeric/math/scalbn>) | [`scalbn`](<#/doc/numeric/math/scalbn>) | [`scalbnl`](<#/doc/numeric/math/scalbn>)  
tgamma  | [`tgammaf`](<#/doc/numeric/math/tgamma>) | [`tgamma`](<#/doc/numeric/math/tgamma>) | [`tgammal`](<#/doc/numeric/math/tgamma>)  
trunc  | [`truncf`](<#/doc/numeric/math/trunc>) | [`trunc`](<#/doc/numeric/math/trunc>) | [`truncl`](<#/doc/numeric/math/trunc>)  
  
### Funções apenas complexas

Para todas as funções de números complexos que não possuem contrapartes reais, existe uma macro genérica por tipo `cXXX`, que chama uma das variantes de uma função complexa:

  * variante float [complex](<#/doc/numeric/complex/complex>) `cXXXf`
  * variante double [complex](<#/doc/numeric/complex/complex>) `cXXX`
  * variante long double [complex](<#/doc/numeric/complex/complex>) `cXXXl`

A função a ser chamada é determinada da seguinte forma:

  * Se qualquer um dos argumentos para os parâmetros genéricos for real, complexo ou imaginário, então a função complexa apropriada é chamada.

Macro genérica   
por tipo  | Variantes de função   
complexa   
|  float |  double |  long double  
carg  | [`cargf`](<#/doc/numeric/complex/carg>) | [`carg`](<#/doc/numeric/complex/carg>) | [`cargl`](<#/doc/numeric/complex/carg>)  
conj  | [`conjf`](<#/doc/numeric/complex/conj>) | [`conj`](<#/doc/numeric/complex/conj>) | [`conjl`](<#/doc/numeric/complex/conj>)  
creal  | [`crealf`](<#/doc/numeric/complex/creal>) | [`creal`](<#/doc/numeric/complex/creal>) | [`creall`](<#/doc/numeric/complex/creal>)  
cimag  | [`cimagf`](<#/doc/numeric/complex/cimag>) | [`cimag`](<#/doc/numeric/complex/cimag>) | [`cimagl`](<#/doc/numeric/complex/cimag>)  
cproj  | [`cprojf`](<#/doc/numeric/complex/cproj>) | [`cproj`](<#/doc/numeric/complex/cproj>) | [`cprojl`](<#/doc/numeric/complex/cproj>)  
  
### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <tgmath.h>
     
    int main(void)
    {
        int i = 2;
        printf("sqrt(2) = %f\n", sqrt(i)); // argument type is int, calls sqrt
     
        float f = 0.5;
        printf("sin(0.5f) = %f\n", sin(f));   // argument type is float, calls sinf
     
        float complex dc = 1 + 0.5*I;
        float complex z = sqrt(dc);      // argument type is float complex, calls csqrtf
        printf("sqrt(1 + 0.5i) = %f+%fi\n",
               creal(z),  // argument type is float complex, calls crealf
               cimag(z)); // argument type is float complex, calls cimagf
    }
```

Saída:
```
    sqrt(2) = 1.414214
    sin(0.5f) = 0.479426
    sqrt(1 + 0.5i) = 1.029086+0.242934i
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.25 Matemática genérica por tipo <tgmath.h> (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.25 Matemática genérica por tipo <tgmath.h> (p: 272-273)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.25 Matemática genérica por tipo <tgmath.h> (p: 373-375)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.22 Matemática genérica por tipo <tgmath.h> (p: 335-337)