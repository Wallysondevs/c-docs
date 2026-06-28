# Extensões de ponto flutuante parte 4: funções suplementares

Extensões de ponto flutuante para C - Parte 4: Funções suplementares, ISO/IEC TS 18661-4:2015, define os seguintes novos componentes para a biblioteca padrão C, conforme recomendado por ISO/IEC/IEEE 60559:2011 (a revisão atual do IEEE-754).

As funções matemáticas suplementares listadas abaixo são incorporadas ao padrão C2x.

##### Macros de teste de recurso predefinidas

---
__STDC_IEC_60559_FUNCS__ | constante inteira do tipo long e valor 201506L
(constante de macro)

##### Funções matemáticas suplementares

Definido no cabeçalho `[`<math.h>`](<#/doc/numeric/math>)`
[ exp2m1 exp2m1f exp2m1lexp2m1fN exp2m1fNxexp2m1dN exp2m1dNx](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext4/exp2m1&action=edit&redlink=1> "c/experimental/fpext4/exp2m1 \(page does not exist\)")(FP Ext 4 TS) | calcula 2x
-1
(função)
[ exp10 exp10f exp10lexp10fN exp10fNxexp10dN exp10dNx](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext4/exp10&action=edit&redlink=1> "c/experimental/fpext4/exp10 \(page does not exist\)")(FP Ext 4 TS) | calcula 10x

(função)
[ exp10m1 exp10m1f exp10m1lexp10m1fN exp10m1fNxexp10m1dN exp10m1dNx](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext4/exp10m1&action=edit&redlink=1> "c/experimental/fpext4/exp10m1 \(page does not exist\)")(FP Ext 4 TS) | calcula 10x
-1
(função)
[ logp1 logp1f logp1llogp1fN logp1fNxlogp1dN logp1dNx](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext4/logp1&action=edit&redlink=1> "c/experimental/fpext4/logp1 \(page does not exist\)")(FP Ext 4 TS) | calcula ln(1+x) (o mesmo que [log1p](<#/doc/numeric/math/log1p>))
(função)
[ log2p1 log2p1f log2p1llog2p1fN log2p1fNxlog2p1dN log2p1dNx](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext4/log2p1&action=edit&redlink=1> "c/experimental/fpext4/log2p1 \(page does not exist\)")(FP Ext 4 TS) | calcula log2(1+x)
(função)
[ log10p1 log10p1f log10p1llog10p1fN log10p1fNxlog10p1dN log10p1dNx](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext4/log10p1&action=edit&redlink=1> "c/experimental/fpext4/log10p1 \(page does not exist\)")(FP Ext 4 TS) | calcula log10(1+x)
(função)
[ rsqrt rsqrtf rsqrtlrsqrtfN rsqrtfNxrsqrtdN rsqrtdNx](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext4/rsqrt&action=edit&redlink=1> "c/experimental/fpext4/rsqrt \(page does not exist\)")(FP Ext 4 TS) | calcula a raiz quadrada inversa x-1/2

(função)
[ compoundn compoundnf compoundnlcompoundnfN compoundnfNxcompoundndN compoundndNx](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext4/compoundn&action=edit&redlink=1> "c/experimental/fpext4/compoundn \(page does not exist\)")(FP Ext 4 TS) | calcula juros compostos, (1+x)n

(função)
[ rootn rootnf rootnlrootnfN rootnfNxrootndN rootndNx](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext4/rootn&action=edit&redlink=1> "c/experimental/fpext4/rootn \(page does not exist\)")(FP Ext 4 TS) | calcula a n-ésima raiz de x, x1/n

(função)
[ pown pownf pownlpownfN pownfNxpowndN powndNx](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext4/pown&action=edit&redlink=1> "c/experimental/fpext4/pown \(page does not exist\)")(FP Ext 4 TS) | calcula x elevado à n-ésima potência, onde n é um inteiro
(função)
[ powr powrf powrlpowrfN powrfNxpowrdN powrdNx](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext4/powr&action=edit&redlink=1> "c/experimental/fpext4/powr \(page does not exist\)")(FP Ext 4 TS) | calcula x elevado à potência y, xy

(função)
[ acospi acospif acospilacospifN acospifNxacospidN acospidNx](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext4/acospi&action=edit&redlink=1> "c/experimental/fpext4/acospi \(page does not exist\)")(FP Ext 4 TS) | calcula arccos(x)/π (medindo o ângulo em meias-revoluções)
(função)
[ asinpi asinpif asinpilasinpifN asinpifNxasinpidN asinpidNx](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext4/asinpi&action=edit&redlink=1> "c/experimental/fpext4/asinpi \(page does not exist\)")(FP Ext 4 TS) | calcula arcsin(x)/π (medindo o ângulo em meias-revoluções)
(função)
[ atanpi atanpif atanpilatanpifN atanpifNxatanpidN atanpidNx](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext4/atanpi&action=edit&redlink=1> "c/experimental/fpext4/atanpi \(page does not exist\)")(FP Ext 4 TS) | calcula arctan(x)/π (medindo o ângulo em meias-revoluções)
(função)
[ atan2pi atan2pif atan2pilatan2pifN atan2pifNxatan2pidN atan2pidNx](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext4/atan2pi&action=edit&redlink=1> "c/experimental/fpext4/atan2pi \(page does not exist\)")(FP Ext 4 TS) | calcula arctan(y/x)/π (medindo o ângulo em meias-revoluções)
(função)
[ cospi cospif cospilcospifN cospifNxcospidN cospidNx](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext4/cospi&action=edit&redlink=1> "c/experimental/fpext4/cospi \(page does not exist\)")(FP Ext 4 TS) | calcula cos(πx) (medindo o ângulo em meias-revoluções)
(função)
[ sinpi sinpif sinpilsinpifN sinpifNxsinpidN sinpidNx](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext4/sinpi&action=edit&redlink=1> "c/experimental/fpext4/sinpi \(page does not exist\)")(FP Ext 4 TS) | calcula sin(πx) (medindo o ângulo em meias-revoluções)
(função)
[ tanpi tanpif tanpiltanpifN tanpifNxtanpidN tanpidNx](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext4/tanpi&action=edit&redlink=1> "c/experimental/fpext4/tanpi \(page does not exist\)")(FP Ext 4 TS) | calcula tan(πx) (medindo o ângulo em meias-revoluções)
(função)

##### Funções de redução

Definido no cabeçalho `[`<math.h>`](<#/doc/numeric/math>)`
[ reduc_sum reduc_sumf reduc_sumlreduc_sumfN reduc_sumfNxreduc_sumdN reduc_sumdNx](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext4/reduc_sum&action=edit&redlink=1> "c/experimental/fpext4/reduc sum \(page does not exist\)")(FP Ext 4 TS) | calcula a soma de n membros de um array
(função)
[ reduc_sumabs reduc_sumabsf reduc_sumabslreduc_sumabsfN reduc_sumabsfNxreduc_sumabsdN reduc_sumabsdNx](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext4/reduc_sumabs&action=edit&redlink=1> "c/experimental/fpext4/reduc sumabs \(page does not exist\)")(FP Ext 4 TS) | calcula a soma dos valores absolutos de n membros de um array
(função)
[ reduc_sumsq reduc_sumsqf reduc_sumsqlreduc_sumsqfN reduc_sumsqfNxreduc_sumsqdN reduc_sumsqdNx](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext4/reduc_sumsq&action=edit&redlink=1> "c/experimental/fpext4/reduc sumsq \(page does not exist\)")(FP Ext 4 TS) | calcula a soma dos quadrados de n membros de um array
(função)
[ reduc_sumprod reduc_sumprodf reduc_sumprodlreduc_sumprodfN reduc_sumprodfNxreduc_sumproddN reduc_sumproddNx](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext4/reduc_sumprod&action=edit&redlink=1> "c/experimental/fpext4/reduc sumprod \(page does not exist\)")(FP Ext 4 TS) | calcula o produto escalar entre n membros de dois arrays
(função)
[ scaled_prod scaled_prodf scaled_prodlscaled_prodfN scaled_prodfNxscaled_proddN scaled_proddNx](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext4/scaled_prod&action=edit&redlink=1> "c/experimental/fpext4/scaled prod \(page does not exist\)")(FP Ext 4 TS) | calcula o produto de n membros de um array como um valor escalado e um fator de escala
(função)
[ scaled_prodsum scaled_prodsumf scaled_prodsumlscaled_prodsumfN scaled_prodsumfNxscaled_prodsumdN scaled_prodsumdNx](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext4/scaled_prodsum&action=edit&redlink=1> "c/experimental/fpext4/scaled prodsum \(page does not exist\)")(FP Ext 4 TS) | calcula o produto escalar de n membros de dois arrays como um valor escalado e um fator de escala
(função)
[ scaled_proddiff scaled_proddifff scaled_proddifflscaled_proddifffN scaled_proddifffNxscaled_proddiffdN scaled_proddiffdNx](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/fpext4/scaled_proddiff&action=edit&redlink=1> "c/experimental/fpext4/scaled proddiff \(page does not exist\)")(FP Ext 4 TS) | calcula o produto das diferenças entre n membros correspondentes de dois arrays como um valor escalado e um fator de escala
(função)

##### Versões de funções com arredondamento correto

Definido no cabeçalho `[`<math.h>`](<#/doc/numeric/math>)`
crexp(optional)(FP Ext 4 TS) | versão com arredondamento correto de [exp](<#/doc/numeric/math/exp>)
(função)
crexpm1(optional)(FP Ext 4 TS) | versão com arredondamento correto de [expm1](<#/doc/numeric/math/expm1>)
(função)
crexp2(optional)(FP Ext 4 TS) | versão com arredondamento correto de [exp2](<#/doc/numeric/math/exp2>)
(função)
crexp2m1(optional)(FP Ext 4 TS) | versão com arredondamento correto de exp2m1
(função)
crexp10(optional)(FP Ext 4 TS) | versão com arredondamento correto de exp10
(função)
crexp10m1(optional)(FP Ext 4 TS) | versão com arredondamento correto de exp10m1
(função)
crlog(optional)(FP Ext 4 TS) | versão com arredondamento correto de [log](<#/doc/numeric/math/log>)
(função)
crlog2(optional)(FP Ext 4 TS) | versão com arredondamento correto de log2
(função)
crlog10(optional)(FP Ext 4 TS) | versão com arredondamento correto de [log10](<#/doc/numeric/math/log10>)
(função)
crlog1p(optional)(FP Ext 4 TS) | versão com arredondamento correto de [log1p](<#/doc/numeric/math/log1p>)
(função)
crlogp1(optional)(FP Ext 4 TS) | versão com arredondamento correto de logp1
(função)
crlog2p1(optional)(FP Ext 4 TS) | versão com arredondamento correto de log2p1
(função)
crlog10p1(optional)(FP Ext 4 TS) | versão com arredondamento correto de log10p1
(função)
crrsqrt(optional)(FP Ext 4 TS) | versão com arredondamento correto de rsqrt
(função)
crcompoundn(optional)(FP Ext 4 TS) | versão com arredondamento correto de compoundn
(função)
crrootn(optional)(FP Ext 4 TS) | versão com arredondamento correto de rootn
(função)
crpown(optional)(FP Ext 4 TS) | versão com arredondamento correto de pown
(função)
crpow(optional)(FP Ext 4 TS) | versão com arredondamento correto de [pow](<#/doc/numeric/math/pow>)
(função)
crpowr(optional)(FP Ext 4 TS) | versão com arredondamento correto de powr
(função)
crsin(optional)(FP Ext 4 TS) | versão com arredondamento correto de [sin](<#/doc/numeric/math/sin>)
(função)
crcos(optional)(FP Ext 4 TS) | versão com arredondamento correto de [cos](<#/doc/numeric/math/cos>)
(função)
crtan(optional)(FP Ext 4 TS) | versão com arredondamento correto de [tan](<#/doc/numeric/math/tan>)
(função)
crsinpi(optional)(FP Ext 4 TS) | versão com arredondamento correto de sinpi
(função)
crcospi(optional)(FP Ext 4 TS) | versão com arredondamento correto de cospi
(função)
crtanpi(optional)(FP Ext 4 TS) | versão com arredondamento correto de tanpi
(função)
crasinpi(optional)(FP Ext 4 TS) | versão com arredondamento correto de asinpi
(função)
cracospi(optional)(FP Ext 4 TS) | versão com arredondamento correto de acospi
(função)
cracospi(optional)(FP Ext 4 TS) | versão com arredondamento correto de acospi
(função)
cratanpi(optional)(FP Ext 4 TS) | versão com arredondamento correto de atanpi
(função)
cratan2pi(optional)(FP Ext 4 TS) | versão com arredondamento correto de atan2pi
(função)
crasin(optional)(FP Ext 4 TS) | versão com arredondamento correto de [asin](<#/doc/numeric/math/asin>)
(função)
cracos(optional)(FP Ext 4 TS) | versão com arredondamento correto de [acos](<#/doc/numeric/math/acos>)
(função)
cratan(optional)(FP Ext 4 TS) | versão com arredondamento correto de [atan](<#/doc/numeric/math/atan>)
(função)
cratan2(optional)(FP Ext 4 TS) | versão com arredondamento correto de [atan2](<#/doc/numeric/math/atan2>)
(função)
crsinh(optional)(FP Ext 4 TS) | versão com arredondamento correto de [sinh](<#/doc/numeric/math/sinh>)
(função)
crcosh(optional)(FP Ext 4 TS) | versão com arredondamento correto de [cosh](<#/doc/numeric/math/cosh>)
(função)
crtanh(optional)(FP Ext 4 TS) | versão com arredondamento correto de [tanh](<#/doc/numeric/math/tanh>)
(função)
crasinh(optional)(FP Ext 4 TS) | versão com arredondamento correto de [asinh](<#/doc/numeric/math/asinh>)
(função)
cracosh(optional)(FP Ext 4 TS) | versão com arredondamento correto de [acosh](<#/doc/numeric/math/acosh>)
(função)
cratanh(optional)(FP Ext 4 TS) | versão com arredondamento correto de [atanh](<#/doc/numeric/math/atanh>)
(função)
crhypot(optional)(FP Ext 4 TS) | versão com arredondamento correto de [hypot](<#/doc/numeric/math/hypot>)
(função)

##### Versões complexas de funções

Definido no cabeçalho `[`<complex.h>`](<#/doc/numeric/complex>)`
cexp2m1(optional)(FP Ext 4 TS) | versão para números complexos de exp2m1
(função)
cexp10(optional)(FP Ext 4 TS) | versão para números complexos de exp10
(função)
cexp10m1(optional)(FP Ext 4 TS) | versão para números complexos de exp10m1
(função)
clogp1(optional)(FP Ext 4 TS) | versão para números complexos de logp1
(função)
clog2p1(optional)(FP Ext 4 TS) | versão para números complexos de log2p1
(função)
clog10p1(optional)(FP Ext 4 TS) | versão para números complexos de log10p1
(função)
crsqrt (optional)(FP Ext 4 TS) | versão para números complexos de rsqrt
(função)
ccompoundn (optional)(FP Ext 4 TS) | versão para números complexos de compoundn
(função)
crootn(optional)(FP Ext 4 TS) | versão para números complexos de rootn
(função)
cpown (optional)(FP Ext 4 TS) | versão para números complexos de pown
(função)
cpowr(optional)(FP Ext 4 TS) | versão para números complexos de powr
(função)
cacospi(optional)(FP Ext 4 TS) | versão para números complexos de acospi
(função)
casinpi(optional)(FP Ext 4 TS) | versão para números complexos de asinpi
(função)
catanpi(optional)(FP Ext 4 TS) | versão para números complexos de atanpi
(função)
ccospi(optional)(FP Ext 4 TS) | versão para números complexos de cospi
(função)
csinpi(optional)(FP Ext 4 TS) | versão para números complexos de sinpi
(função)
ctanpi(optional)(FP Ext 4 TS) | versão para números complexos de tanpi
(função)

### Notas

Todas as funções adicionadas à biblioteca C por esta extensão são declaradas apenas se a macro __STDC_WANT_IEC_60559_FUNCS_EXT__ for definida antes que math.h seja incluído.

As variantes de ponto flutuante decimal de cada função são definidas apenas se __STDC_WANT_IEC_60559_DFP_EXT__ também for definida antes que math.h seja incluído.

As variantes de precisão estendida de cada função são definidas apenas se __STDC_WANT_IEC_60559_TYPES_EXT__ for definida antes que math.h seja incluído.

As versões com arredondamento correto de todas as funções (com o prefixo cr-) são opcionais.