# Funções matemáticas comuns

### Tipos  
  
Definidos no cabeçalho `[`<stdlib.h>`](<#/doc/program>)`  
---  
[ div_t](<#/doc/numeric/math/div>) | tipo de estrutura, retorno da função [div](<#/doc/numeric/math/div>)   
(typedef)  
[ ldiv_t](<#/doc/numeric/math/div>) | tipo de estrutura, retorno da função [ldiv](<#/doc/numeric/math/div>)   
(typedef)  
[ lldiv_t](<#/doc/numeric/math/div>)(C99) | tipo de estrutura, retorno da função lldiv   
(typedef)  
Definidos no cabeçalho `[`<inttypes.h>`](<#/doc/types/integer>)`  
[ imaxdiv_t](<#/doc/numeric/math/div>)(C99) | tipo de estrutura, retorno da função imaxdiv   
(typedef)  
Definidos no cabeçalho `<math.h>`  
[ float_t](<#/doc/numeric/math/float_t>)(C99) | tipo de ponto flutuante mais eficiente, pelo menos tão largo quanto float   
(typedef)  
[ double_t](<#/doc/numeric/math/float_t>)(C99) | tipo de ponto flutuante mais eficiente, pelo menos tão largo quanto double   
(typedef)  
  
### Constantes

Definidos no cabeçalho `<math.h>`  
---  
[ HUGE_VALFHUGE_VALHUGE_VALL](<#/doc/numeric/math/HUGE_VAL>)(C99)(C99) | indica valor muito grande para ser representável (infinito) por float, double e long double, respectivamente   
(macro constante)  
[ INFINITY](<#/doc/numeric/math/INFINITY>)(C99) | avalia para infinito positivo ou o valor garantido para causar overflow em um float   
(macro constante)  
[ NAN](<#/doc/numeric/math/NAN>)(C99) | avalia para um NaN silencioso do tipo float   
(macro constante)  
[ FP_FAST_FMAFFP_FAST_FMAFP_FAST_FMAL](<#/doc/numeric/math/fma>)(C99)(C99)(C99) | indica que a função fma geralmente executa tão rápido quanto, ou mais rápido que, uma multiplicação e uma adição de operandos double   
(macro constante)  
[ FP_ILOGB0FP_ILOGBNAN](<#/doc/numeric/math/ilogb>)(C99)(C99) | avalia para [ilogb](<#/doc/numeric/math/ilogb>)(x) se x for zero ou NaN, respectivamente   
(macro constante)  
[ math_errhandlingMATH_ERRNOMATH_ERREXCEPT](<#/doc/numeric/math/math_errhandling>)(C99)(C99)(C99) | define o mecanismo de tratamento de erros usado pelas funções matemáticas comuns   
(macro constante)  
  
##### Classificação   
  
[ FP_NORMALFP_SUBNORMALFP_ZEROFP_INFINITEFP_NAN](<#/doc/numeric/math/FP_categories>)(C99)(C99)(C99)(C99)(C99) | indica uma categoria de ponto flutuante   
(macro constante)  
  
### Funções

Definidos no cabeçalho `[`<stdlib.h>`](<#/doc/program>)`  
---  
[ abslabsllabs](<#/doc/numeric/math/abs>)(C99) | calcula o valor absoluto de um valor integral (\\(\small{|x|}\\)|x|)   
(função)  
[ divldivlldiv](<#/doc/numeric/math/div>)(C99) | calcula o quociente e o resto da divisão inteira   
(função)  
Definidos no cabeçalho `[`<inttypes.h>`](<#/doc/types/integer>)`  
[ imaxabs](<#/doc/numeric/math/abs>)(C99) | calcula o valor absoluto de um valor integral (\\(\small{|x|}\\)|x|)   
(função)  
[ imaxdiv](<#/doc/numeric/math/div>)(C99) | calcula o quociente e o resto da divisão inteira   
(função)  
Definidos no cabeçalho `<math.h>`  
  
##### Operações básicas   
  
[ fabsfabsffabsl](<#/doc/numeric/math/fabs>)(C99)(C99) | calcula o valor absoluto de um valor de ponto flutuante (\\(\small{|x|}\\)|x|)   
(função)  
[ fmodfmodffmodl](<#/doc/numeric/math/fmod>)(C99)(C99) | calcula o resto da operação de divisão de ponto flutuante   
(função)  
[ remainderremainderfremainderl](<#/doc/numeric/math/remainder>)(C99)(C99)(C99) | calcula o resto com sinal da operação de divisão de ponto flutuante   
(função)  
[ remquoremquofremquol](<#/doc/numeric/math/remquo>)(C99)(C99)(C99) | calcula o resto com sinal, bem como os três últimos bits da operação de divisão   
(função)  
[ fmafmaffmal](<#/doc/numeric/math/fma>)(C99)(C99)(C99) | calcula a operação de multiplicação-adição fundida   
(função)  
[ fmaxfmaxffmaxl](<#/doc/numeric/math/fmax>)(C99)(C99)(C99) | determina o maior de dois valores de ponto flutuante   
(função)  
[ fminfminffminl](<#/doc/numeric/math/fmin>)(C99)(C99)(C99) | determina o menor de dois valores de ponto flutuante   
(função)  
[ fdimfdimffdiml](<#/doc/numeric/math/fdim>)(C99)(C99)(C99) | determina a diferença positiva de dois valores de ponto flutuante (\\({\small\max{(0, x-y)} }\\)max(0, x-y))   
(função)  
[ nannanfnanl](<#/doc/numeric/math/nan.2>)(C99)(C99)(C99) | retorna um NaN (não é um número)   
(função)  
  
##### Funções exponenciais   
  
[ expexpfexpl](<#/doc/numeric/math/exp>)(C99)(C99) | calcula _e_ elevado à potência dada (\\({\small e^x}\\)ex)   
(função)  
[ exp2exp2fexp2l](<#/doc/numeric/math/exp2>)(C99)(C99)(C99) | calcula _2_ elevado à potência dada (\\({\small 2^x}\\)2x)   
(função)  
[ expm1expm1fexpm1l](<#/doc/numeric/math/expm1>)(C99)(C99)(C99) | calcula _e_ elevado à potência dada, menos um (\\({\small e^x-1}\\)ex-1)   
(função)  
[ loglogflogl](<#/doc/numeric/math/log>)(C99)(C99) | calcula o logaritmo natural (base-_e_) (\\({\small \ln{x} }\\)ln(x))   
(função)  
[ log10log10flog10l](<#/doc/numeric/math/log10>)(C99)(C99) | calcula o logaritmo comum (base-_10_) (\\({\small \log_{10}{x} }\\)log10(x))   
(função)  
[ log2log2flog2l](<#/doc/numeric/math/log2>)(C99)(C99)(C99) | calcula o logaritmo de base-2 (\\({\small \log_{2}{x} }\\)log2(x))   
(função)  
[ log1plog1pflog1pl](<#/doc/numeric/math/log1p>)(C99)(C99)(C99) | calcula o logaritmo natural (base-_e_) de 1 mais o número dado (\\({\small \ln{(1+x)} }\\)ln(1+x))   
(função)  
  
##### Funções de potência   
  
[ powpowfpowl](<#/doc/numeric/math/pow>)(C99)(C99) | calcula um número elevado à potência dada (\\(\small{x^y}\\)xy)   
(função)  
[ sqrtsqrtfsqrtl](<#/doc/numeric/math/sqrt>)(C99)(C99) | calcula a raiz quadrada (\\(\small{\sqrt{x} }\\)√x)   
(função)  
[ cbrtcbrtfcbrtl](<#/doc/numeric/math/cbrt>)(C99)(C99)(C99) | calcula a raiz cúbica (\\(\small{\sqrt[3]{x} }\\)3√x)   
(função)  
[ hypothypotfhypotl](<#/doc/numeric/math/hypot>)(C99)(C99)(C99) | calcula a raiz quadrada da soma dos quadrados de dois números dados (\\(\scriptsize{\sqrt{x^2+y^2} }\\)√x2  
+y2  
)   
(função)  
  
##### Funções trigonométricas   
  
[ sinsinfsinl](<#/doc/numeric/math/sin>)(C99)(C99) | calcula o seno (\\({\small\sin{x} }\\)sin(x))   
(função)  
[ coscosfcosl](<#/doc/numeric/math/cos>)(C99)(C99) | calcula o cosseno (\\({\small\cos{x} }\\)cos(x))   
(função)  
[ tantanftanl](<#/doc/numeric/math/tan>)(C99)(C99) | calcula a tangente (\\({\small\tan{x} }\\)tan(x))   
(função)  
[ asinasinfasinl](<#/doc/numeric/math/asin>)(C99)(C99) | calcula o arco seno (\\({\small\arcsin{x} }\\)arcsin(x))   
(função)  
[ acosacosfacosl](<#/doc/numeric/math/acos>)(C99)(C99) | calcula o arco cosseno (\\({\small\arccos{x} }\\)arccos(x))   
(função)  
[ atanatanfatanl](<#/doc/numeric/math/atan>)(C99)(C99) | calcula o arco tangente (\\({\small\arctan{x} }\\)arctan(x))   
(função)  
[ atan2atan2fatan2l](<#/doc/numeric/math/atan2>)(C99)(C99) | calcula o arco tangente, usando sinais para determinar os quadrantes   
(função)  
  
##### Funções hiperbólicas   
  
[ sinhsinhfsinhl](<#/doc/numeric/math/sinh>)(C99)(C99) | calcula o seno hiperbólico (\\({\small\sinh{x} }\\)sinh(x))   
(função)  
[ coshcoshfcoshl](<#/doc/numeric/math/cosh>)(C99)(C99) | calcula o cosseno hiperbólico (\\({\small\cosh{x} }\\)cosh(x))   
(função)  
[ tanhtanhftanhl](<#/doc/numeric/math/tanh>)(C99)(C99) | calcula a tangente hiperbólica (\\({\small\tanh{x} }\\)tanh(x))   
(função)  
[ asinhasinhfasinhl](<#/doc/numeric/math/asinh>)(C99)(C99)(C99) | calcula o seno hiperbólico inverso (\\({\small\operatorname{arsinh}{x} }\\)arsinh(x))   
(função)  
[ acoshacoshfacoshl](<#/doc/numeric/math/acosh>)(C99)(C99)(C99) | calcula o cosseno hiperbólico inverso (\\({\small\operatorname{arcosh}{x} }\\)arcosh(x))   
(função)  
[ atanhatanhfatanhl](<#/doc/numeric/math/atanh>)(C99)(C99)(C99) | calcula a tangente hiperbólica inversa (\\({\small\operatorname{artanh}{x} }\\)artanh(x))   
(função)  
  
##### Funções de erro e gama   
  
[ erferfferfl](<#/doc/numeric/math/erf>)(C99)(C99)(C99) | calcula a função de erro   
(função)  
[ erfcerfcferfcl](<#/doc/numeric/math/erfc>)(C99)(C99)(C99) | calcula a função de erro complementar   
(função)  
[ tgammatgammaftgammal](<#/doc/numeric/math/tgamma>)(C99)(C99)(C99) | calcula a função gama   
(função)  
[ lgammalgammaflgammal](<#/doc/numeric/math/lgamma>)(C99)(C99)(C99) | calcula o logaritmo natural (base-_e_) da função gama   
(função)  
  
##### Operações de ponto flutuante para o inteiro mais próximo   
  
[ ceilceilfceill](<#/doc/numeric/math/ceil>)(C99)(C99) | calcula o menor inteiro não menor que o valor dado   
(função)  
[ floorfloorffloorl](<#/doc/numeric/math/floor>)(C99)(C99) | calcula o maior inteiro não maior que o valor dado   
(função)  
[ trunctruncftruncl](<#/doc/numeric/math/trunc>)(C99)(C99)(C99) | arredonda para o inteiro mais próximo não maior em magnitude que o valor dado   
(função)  
[ roundroundfroundllroundlroundflroundlllroundllroundfllroundl](<#/doc/numeric/math/round>)(C99)(C99)(C99)(C99)(C99)(C99)(C99)(C99)(C99) | arredonda para o inteiro mais próximo, arredondando para longe de zero em casos de meio termo   
(função)  
[ nearbyintnearbyintfnearbyintl](<#/doc/numeric/math/nearbyint>)(C99)(C99)(C99) | arredonda para um inteiro usando o modo de arredondamento atual   
(função)  
[ rintrintfrintllrintlrintflrintlllrintllrintfllrintl](<#/doc/numeric/math/rint>)(C99)(C99)(C99)(C99)(C99)(C99)(C99)(C99)(C99) | arredonda para um inteiro usando o modo de arredondamento atual com exceção se o resultado for diferente   
(função)  
  
##### Funções de manipulação de ponto flutuante   
  
[ frexpfrexpffrexpl](<#/doc/numeric/math/frexp>)(C99)(C99) | divide um número em mantissa e uma potência de 2   
(função)  
[ ldexpldexpfldexpl](<#/doc/numeric/math/ldexp>)(C99)(C99) | multiplica um número por 2 elevado a uma potência   
(função)  
[ modfmodffmodfl](<#/doc/numeric/math/modf>)(C99)(C99) | divide um número em partes inteira e fracionária   
(função)  
[ scalbnscalbnfscalbnlscalblnscalblnfscalblnl](<#/doc/numeric/math/scalbn>)(C99)(C99)(C99)(C99)(C99)(C99) | calcula eficientemente um número vezes [FLT_RADIX](<#/doc/types/limits>) elevado a uma potência   
(função)  
[ ilogbilogbfilogbl](<#/doc/numeric/math/ilogb>)(C99)(C99)(C99) | extrai o expoente do número dado   
(função)  
[ logblogbflogbl](<#/doc/numeric/math/logb>)(C99)(C99)(C99) | extrai o expoente do número dado   
(função)  
[ nextafternextafterfnextafterlnexttowardnexttowardfnexttowardl](<#/doc/numeric/math/nexttoward>)(C99)(C99)(C99)(C99)(C99)(C99) | determina o próximo valor de ponto flutuante representável em direção ao valor dado   
(função)  
[ copysigncopysignfcopysignl](<#/doc/numeric/math/copysign>)(C99)(C99)(C99) | produz um valor com a magnitude de um valor dado e o sinal de outro valor dado   
(função)  
  
##### Classificação e comparação   
  
[ fpclassify](<#/doc/numeric/math/fpclassify>)(C99) | classifica o valor de ponto flutuante dado   
(macro de função)  
[ isfinite](<#/doc/numeric/math/isfinite>)(C99) | verifica se o número dado tem valor finito   
(macro de função)  
[ isinf](<#/doc/numeric/math/isinf>)(C99) | verifica se o número dado é infinito   
(macro de função)  
[ isnan](<#/doc/numeric/math/isnan>)(C99) | verifica se o número dado é NaN   
(macro de função)  
[ isnormal](<#/doc/numeric/math/isnormal>)(C99) | verifica se o número dado é normal   
(macro de função)  
[ signbit](<#/doc/numeric/math/signbit>)(C99) | verifica se o número dado é negativo   
(macro de função)  
[ isgreater](<#/doc/numeric/math/isgreater>)(C99) | verifica se o primeiro argumento de ponto flutuante é maior que o segundo   
(macro de função)  
[ isgreaterequal](<#/doc/numeric/math/isgreaterequal>)(C99) | verifica se o primeiro argumento de ponto flutuante é maior ou igual ao segundo   
(macro de função)  
[ isless](<#/doc/numeric/math/isless>)(C99) | verifica se o primeiro argumento de ponto flutuante é menor que o segundo   
(macro de função)  
[ islessequal](<#/doc/numeric/math/islessequal>)(C99) | verifica se o primeiro argumento de ponto flutuante é menor ou igual ao segundo   
(macro de função)  
[ islessgreater](<#/doc/numeric/math/islessgreater>)(C99) | verifica se o primeiro argumento de ponto flutuante é menor ou maior que o segundo   
(macro de função)  
[ isunordered](<#/doc/numeric/math/isunordered>)(C99) | verifica se dois valores de ponto flutuante estão desordenados   
(macro de função)  
  
### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.8 Conversão de formato de tipos inteiros <inttypes.h> (p: TBD) 

    

  * 7.12 Matemática <math.h> (p: TBD) 

    

  * 7.22 Utilitários gerais <stdlib.h> (p: TBD) 

    

  * 7.31.5 Conversão de formato de tipos inteiros <inttypes.h> (p: TBD) 

    

  * 7.31.12 Utilitários gerais <stdlib.h> (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.8 Conversão de formato de tipos inteiros <inttypes.h> (p: 158-160) 

    

  * 7.12 Matemática <math.h> (p: 169-190) 

    

  * 7.22 Utilitários gerais <stdlib.h> (p: 248-262) 

    

  * 7.31.5 Conversão de formato de tipos inteiros <inttypes.h> (p: 332) 

    

  * 7.31.12 Utilitários gerais <stdlib.h> (p: 333) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.8 Conversão de formato de tipos inteiros <inttypes.h> (p: 217-220) 

    

  * 7.12 Matemática <math.h> (p: 231-261) 

    

  * 7.22 Utilitários gerais <stdlib.h> (p: 340-360) 

    

  * 7.31.5 Conversão de formato de tipos inteiros <inttypes.h> (p: 455) 

    

  * 7.31.12 Utilitários gerais <stdlib.h> (p: 456) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.8 Conversão de formato de tipos inteiros <inttypes.h> (p: 198-201) 

    

  * 7.12 Matemática <math.h> (p: 212-242) 

    

  * 7.20 Utilitários gerais <stdlib.h> (p: 306-324) 

    

  * 7.26.4 Conversão de formato de tipos inteiros <inttypes.h> (p: 401) 

    

  * 7.26.10 Utilitários gerais <stdlib.h> (p: 402) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.5 MATEMÁTICA <math.h>

    

  * 4.10 UTILITÁRIOS GERAIS <stdlib.h>

    

  * 4.13.4 Matemática <math.h>

    

  * 7.13.7 Utilitários gerais <stdlib.h>

### Veja também

[Documentação C++](<#/>) para Funções matemáticas comuns  
---