# Extensões de ponto flutuante parte 1: aritmética de ponto flutuante binária

Extensões de ponto flutuante para C - Parte 1: Aritmética de ponto flutuante binária, ISO/IEC TS 18661-1:2014, define os seguintes novos componentes para a biblioteca padrão C, conforme recomendado por ISO/IEC/IEEE 60559:2011 (a revisão atual do IEEE-754)

__STDC_IEC_60559_BFP__ | constante inteira do tipo long e valor 201ymmL, substitui __STDC_IEC_559__
(macro constante)
__STDC_IEC_60559_COMPLEX__ | constante inteira do tipo long e valor 201ymmL, substitui __STDC_IEC_559_COMPLEX__
(macro constante)
Definido no cabeçalho `[`<limits.h>`](<#/doc/types/limits>)`
CHAR_WIDTH SCHAR_WIDTH UCHAR_WIDTHSHRT_WIDTH USHRT_WIDTHINT_WIDTH UINT_WIDTHLONG_WIDTH ULONG_WIDTHLLONG_WIDTH ULLONG_WIDTH(FP Ext 1 TS) | largura, em bits, do tipo correspondente
(macro constante)
Definido no cabeçalho `[`<float.h>`](<#/doc/types/limits>)`
[ CR_DECIMAL_DIG](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext1/CR_DECIMAL_DIG&action=edit&redlink=1> "c/experimental/fpext1/CR DECIMAL DIG \(page does not exist\)")(FP Ext 1 TS) | conversões entre todos os tipos de ponto flutuante binário suportados e sequências de caracteres com no máximo CR_DECIMAL_DIG dígitos decimais significativos são corretamente arredondadas (isso é pelo menos DECIMAL_DIG + 3)
(macro constante)
Definido no cabeçalho `[`<fenv.h>`](<#/doc/numeric/fenv>)`
femode_t(FP Ext 1 TS) | coleção de modos de controle de ponto flutuante dinâmicos suportados pela implementação, incluindo o modo de direção de arredondamento dinâmico
(typedef)
FE_DFL_MODE(FP Ext 1 TS) | ponteiro para o femode_t padrão
(macro constante)
FE_SNANS_ALWAYS_SIGNAL(FP Ext 1 TS) | definido (como constante inteira 1) se argumentos sNaN fizerem com que as funções que suprimem qNaNs, como [hypot](<#/doc/numeric/math/hypot>) ou [fmax](<#/doc/numeric/math/fmax>), levantem FE_INVALID e retornem um qNaN
(macro constante)
[ fesetexcept](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext1/fesetexcept&action=edit&redlink=1> "c/experimental/fpext1/fesetexcept \(page does not exist\)")(FP Ext 1 TS) | define os sinalizadores de exceção de ponto flutuante especificados sem causar quaisquer efeitos colaterais que levantá-los causaria
(função)
[ fetestexceptflag](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext1/fetestexceptflag&action=edit&redlink=1> "c/experimental/fpext1/fetestexceptflag \(page does not exist\)")(FP Ext 1 TS) | testa se os sinalizadores dados estão em uma representação salva dos sinalizadores de exceção de ponto flutuante
(função)
[ fegetmodefesetmode](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext1/fegetmode_fesetmode&action=edit&redlink=1> "c/experimental/fpext1/fegetmode fesetmode \(page does not exist\)")(FP Ext 1 TS) | obtém e define coletivamente todos os modos de controle de ponto flutuante dinâmicos da implementação
(função)
Definido no cabeçalho `[`<stdint.h>`](<#/doc/types/integer>)`
INTn_WIDTH UINTn_WIDTHINT_LEASTn_WIDTH UINT_LEASTn_WIDTHINT_FASTn_WIDTH UINT_FASTn_WIDTHINTPTR_WIDTH UINTPTR_WIDTHINTMAX_WIDTH UINTMAX_WIDTHPTRDIFF_WIDTHSIG_ATOMIC_WIDTHSIZE_WIDTHWCHAR_WIDTH WINT_WIDTH(FP Ext 1 TS) | largura, em bits, do tipo correspondente
(macro constante)
Definido no cabeçalho `[`<stdlib.h>`](<#/doc/program>)`
[ strfromdstrfromfstrfroml](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext1/strfromf&action=edit&redlink=1> "c/experimental/fpext1/strfromf \(page does not exist\)")(FP Ext 1 TS) | converte um único número de ponto flutuante para string usando o formato snprintf especificado
(função)
Definido no cabeçalho `[`<math.h>`](<#/doc/numeric/math>)`
FP_INT_UPWARDFP_INT_DOWNWARDFP_INT_TOWARDZERO FP_INT_TONEARESTFROMZEROFP_INT_TONEAREST(FP Ext 1 TS) | direção de arredondamento para as funções ceil, floor, trunc, round e roundeven, adequadas para uso com a família de funções fromfp
(macro constante)
FP_LLOGB0(FP Ext 1 TS) | valor retornado por llogb se o argumento for zero
(macro constante)
FP_LLOGBNAN(FP Ext 1 TS) | valor retornado por llogb se o argumento for NaN
(macro constante)
[ SNANFSNANSNANL](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext1/SNAN&action=edit&redlink=1> "c/experimental/fpext1/SNAN \(page does not exist\)")(FP Ext 1 TS) | representa um NaN sinalizador para float, double, long double respectivamente
(macro constante)
FP_FAST_FADD FP_FAST_FADDL FP_FAST_DADDLFP_FAST_FSUB FP_FAST_FSUBL FP_FAST_DSUBLFP_FAST_FMUL FP_FAST_FMULL FP_FAST_DMULLFP_FAST_FDIV FP_FAST_FDIVL FP_FAST_DDIVLFP_FAST_FFMA FP_FAST_FFMAL FP_FAST_DFMALFP_FAST_FSQRT FP_FAST_FSQRTL FP_FAST_DSQRTL(FP Ext 1 TS) | se definido, indica que a função correspondente é executada mais rapidamente do que a função equivalente em um tipo maior seguida por um cast para o tipo de destino
(macro constante)
iseqsig(FP Ext 1 TS) |
(macro de função)
iscanonical(FP Ext 1 TS) | testa se o valor de ponto flutuante é canônico
(macro de função)
issignaling(FP Ext 1 TS) | testa se o valor de ponto flutuante é um NaN sinalizador
(macro de função)
issubnormal(FP Ext 1 TS) | testa se o valor de ponto flutuante é subnormal
(macro de função)
iszero(FP Ext 1 TS) | testa se o valor de ponto flutuante é zero (positivo, negativo, sem sinal)
(macro de função)
[ fromfpfromfpffromfpl](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext1/fromfp&action=edit&redlink=1> "c/experimental/fpext1/fromfp \(page does not exist\)")(FP Ext 1 TS) | arredonda para inteiro com sinal usando a direção de arredondamento especificada
(função)
[ ufromfpufromfpfufromfpl](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext1/ufromfp&action=edit&redlink=1> "c/experimental/fpext1/ufromfp \(page does not exist\)")(FP Ext 1 TS) | arredonda para inteiro sem sinal usando a direção de arredondamento especificada
(função)
[ fromfpxfromfpxffromfpxl](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext1/fromfpx&action=edit&redlink=1> "c/experimental/fpext1/fromfpx \(page does not exist\)")(FP Ext 1 TS) | arredonda para inteiro com sinal usando a direção de arredondamento especificada, reportando imprecisão
(função)
[ ufromfpxufromfpxfufromfpxl](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext1/ufromfpx&action=edit&redlink=1> "c/experimental/fpext1/ufromfpx \(page does not exist\)")(FP Ext 1 TS) | arredonda para inteiro sem sinal usando a direção de arredondamento especificada, reportando imprecisão
(função)
[ roundevenroundevenfroundevenl](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext1/roundeven&action=edit&redlink=1> "c/experimental/fpext1/roundeven \(page does not exist\)")(FP Ext 1 TS) | arredonda para o mais próximo, casos intermediários para par
(função)
[ llogbllogbfllogbl](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext1/llogb&action=edit&redlink=1> "c/experimental/fpext1/llogb \(page does not exist\)")(FP Ext 1 TS) | equivalente a [logb](<#/doc/numeric/math/logb>) exceto que o tipo de retorno é long
(função)
[ fmaxmagfmaxmagffmaxmagl](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext1/fmaxmag&action=edit&redlink=1> "c/experimental/fpext1/fmaxmag \(page does not exist\)")(FP Ext 1 TS) | retorna o valor do argumento de maior magnitude
(função)
[ fminmagfminmagffminmagl](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext1/fminmag&action=edit&redlink=1> "c/experimental/fpext1/fminmag \(page does not exist\)")(FP Ext 1 TS) | retorna o valor do argumento de menor magnitude
(função)
[ nextupnextupfnextupl](<#/doc/experimental/fpext1/nextup>)(FP Ext 1 TS) | retorna o próximo valor de ponto flutuante representável maior
(função)
[ nextdownnextdownfnextdown l](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext1/nextdown&action=edit&redlink=1> "c/experimental/fpext1/nextdown \(page does not exist\)")(FP Ext 1 TS) | retorna o próximo valor de ponto flutuante representável menor
(função)
[ faddfaddldaddl](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext1/fadd&action=edit&redlink=1> "c/experimental/fpext1/fadd \(page does not exist\)")(FP Ext 1 TS) | calcula x+y como se em precisão infinita e arredondado uma vez para o tipo de destino
(função)
[ fsubfsubldsubl](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext1/fsub&action=edit&redlink=1> "c/experimental/fpext1/fsub \(page does not exist\)")(FP Ext 1 TS) | calcula x-y como se em precisão infinita e arredondado uma vez para o tipo de destino
(função)
[ fmulfmulldmull](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext1/fmul&action=edit&redlink=1> "c/experimental/fpext1/fmul \(page does not exist\)")(FP Ext 1 TS) | calcula x*y como se em precisão infinita e arredondado uma vez para o tipo de destino
(função)
[ fdivfdivlddivl](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext1/fdiv&action=edit&redlink=1> "c/experimental/fpext1/fdiv \(page does not exist\)")(FP Ext 1 TS) | calcula x/y como se em precisão infinita e arredondado uma vez para o tipo de destino
(função)
[ ffmaffmaldfmal](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext1/ffma&action=edit&redlink=1> "c/experimental/fpext1/ffma \(page does not exist\)")(FP Ext 1 TS) | calcula o mesmo que [fma](<#/doc/numeric/math/fma>) como se em precisão infinita e arredondado uma vez para o tipo de destino
(função)
[ fsqrtfsqrtldsqrtl](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext1/fsqrt&action=edit&redlink=1> "c/experimental/fpext1/fsqrt \(page does not exist\)")(FP Ext 1 TS) | calcula o mesmo que [sqrt](<#/doc/numeric/math/sqrt>) como se em precisão infinita e arredondado uma vez para o tipo de destino
(função)
[ totalordertotalorderftotalorderl](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext1/totalorder&action=edit&redlink=1> "c/experimental/fpext1/totalorder \(page does not exist\)")(FP Ext 1 TS) | ordena dois valores de ponto flutuante usando a relação de ordem total ISO 60559
(função)
[ totalordermagtotalordermagftotalordermagl](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext1/totalordermag&action=edit&redlink=1> "c/experimental/fpext1/totalordermag \(page does not exist\)")(FP Ext 1 TS) | ordena as magnitudes de dois valores de ponto flutuante usando a relação de ordem total ISO 60559
(função)
[ canonicalizecanonicalizefcanonicalizel](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext1/canonicalize&action=edit&redlink=1> "c/experimental/fpext1/canonicalize \(page does not exist\)")(FP Ext 1 TS) | obtém a codificação binária canônica ISO 60559 do valor de ponto flutuante dado
(função)
[ getpayloadgetpayloadfgetpayloadl](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext1/getpayload&action=edit&redlink=1> "c/experimental/fpext1/getpayload \(page does not exist\)")(FP Ext 1 TS) | extrai o payload do valor NaN dado
(função)
[ setpayloadsetpayloadfsetpayloadl](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext1/setpayload&action=edit&redlink=1> "c/experimental/fpext1/setpayload \(page does not exist\)")(FP Ext 1 TS) | cria um NaN silencioso com o payload especificado
(função)
[ setpayloadsigsetpayloadsigfsetpayloadsigl](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext1/setpayloadsig&action=edit&redlink=1> "c/experimental/fpext1/setpayloadsig \(page does not exist\)")(FP Ext 1 TS) | cria um NaN sinalizador com o payload especificado
(função)
Definido no cabeçalho `[`<tgmath.h>`](<#/doc/numeric/tgmath>)`
roundeven(FP Ext 1 TS) | sobrecarga genérica de roundeven
(função)
llogb(FP Ext 1 TS) | sobrecarga genérica de llogb
(função)
fmaxmag(FP Ext 1 TS) | sobrecarga genérica de fmaxmag
(função)
fminmag(FP Ext 1 TS) | sobrecarga genérica de fminmag
(função)
nextup(FP Ext 1 TS) | sobrecarga genérica de nextup
(função)
nextdown(FP Ext 1 TS) | sobrecarga genérica de nextdown
(função)
fromfp(FP Ext 1 TS) | sobrecarga genérica de fromfp
(função)
ufromfp(FP Ext 1 TS) | sobrecarga genérica de ufromfp
(função)
fromfpx(FP Ext 1 TS) | sobrecarga genérica de fromfpx
(função)
ufromfpx(FP Ext 1 TS) | sobrecarga genérica de ufromfpx
(função)
nextdown(FP Ext 1 TS) | sobrecarga genérica de nextdown
(função)
totalorder(FP Ext 1 TS) | sobrecarga genérica de totalorder
(função)
totalordermag(FP Ext 1 TS) | sobrecarga genérica de totalordermag
(função)
fadd(FP Ext 1 TS) | sobrecarga genérica de fadd
(função)
dadd(FP Ext 1 TS) | sobrecarga genérica de dadd
(função)
fsub(FP Ext 1 TS) | sobrecarga genérica de fsub
(função)
dsub(FP Ext 1 TS) | sobrecarga genérica de dsub
(função)
fmul(FP Ext 1 TS) | sobrecarga genérica de fmul
(função)
dmul(FP Ext 1 TS) | sobrecarga genérica de dmul
(função)
fdiv(FP Ext 1 TS) | sobrecarga genérica de fdiv
(função)
ddiv(FP Ext 1 TS) | sobrecarga genérica de ddiv
(função)
ffma(FP Ext 1 TS) | sobrecarga genérica de ffma
(função)
dfma(FP Ext 1 TS) | sobrecarga genérica de dfma
(função)
fsqrt(FP Ext 1 TS) | sobrecarga genérica de fsqrt
(função)
dsqrt(FP Ext 1 TS) | sobrecarga genérica de dsqrt
(função)

### Notas

As macros C padrão __STDC_IEC_559__ e __STDC_IEC_559_COMPLEX__ são tornadas obsoletas por esta especificação técnica.

Todas as funções e macros adicionadas à biblioteca C por esta extensão são declaradas apenas se uma macro __STDC_WANT_IEC_60559_BFP_EXT__ for definida antes que o cabeçalho correspondente seja incluído.

Além das adições à biblioteca padrão, ISO/IEC TS 18661-1:2014 faz uma série de mudanças na linguagem central, notavelmente dividindo o controle de ponto flutuante entre estático (controlado pelo novo #pragma STDC FENV_ROUND) e dinâmico (controlado por [fesetround](<#/doc/numeric/fenv/feround>)). A maioria das funções de math.h respeita o modo de arredondamento estático, se definido, em detrimento do modo de arredondamento dinâmico.

| Esta seção está incompleta
Razão: adicionar à página pragma ou descrever o pragma na íntegra aqui?