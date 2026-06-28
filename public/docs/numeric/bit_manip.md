# Manipulação de bits (desde C23)

### Funções
---
Definido no cabeçalho `[`<stdbit.h>`](<#/doc/numeric>)`
[ stdc_leading_zeros](<#/doc/numeric/bit/stdc_leading_zeros>)(C23) | conta o número de bits 0 consecutivos, começando do bit mais significativo
(macro de função genérica por tipo)
[ stdc_leading_ones](<https://en.cppreference.com/mwiki/index.php?title=c/numeric/bit/stdc_leading_ones&action=edit&redlink=1> "c/numeric/bit/stdc leading ones \(page does not exist\)")(C23) | conta o número de bits 1 consecutivos, começando do bit mais significativo
(macro de função genérica por tipo)
[ stdc_trailing_zeros](<https://en.cppreference.com/mwiki/index.php?title=c/numeric/bit/stdc_trailing_zeros&action=edit&redlink=1> "c/numeric/bit/stdc trailing zeros \(page does not exist\)")(C23) | conta o número de bits 0 consecutivos, começando do bit menos significativo
(macro de função genérica por tipo)
[ stdc_trailing_ones](<https://en.cppreference.com/mwiki/index.php?title=c/numeric/bit/stdc_trailing_ones&action=edit&redlink=1> "c/numeric/bit/stdc trailing ones \(page does not exist\)")(C23) | conta o número de bits 1 consecutivos, começando do bit menos significativo
(macro de função genérica por tipo)
[ stdc_first_leading_zero](<https://en.cppreference.com/mwiki/index.php?title=c/numeric/bit/stdc_first_leading_zero&action=edit&redlink=1> "c/numeric/bit/stdc first leading zero \(page does not exist\)")(C23) | encontra a primeira posição do bit 0, começando do bit mais significativo
(macro de função genérica por tipo)
[ stdc_first_leading_one](<https://en.cppreference.com/mwiki/index.php?title=c/numeric/bit/stdc_first_leading_one&action=edit&redlink=1> "c/numeric/bit/stdc first leading one \(page does not exist\)")(C23) | encontra a primeira posição do bit 1, começando do bit mais significativo
(macro de função genérica por tipo)
[ stdc_first_trailing_zero](<https://en.cppreference.com/mwiki/index.php?title=c/numeric/bit/stdc_first_trailing_zero&action=edit&redlink=1> "c/numeric/bit/stdc first trailing zero \(page does not exist\)")(C23) | encontra a primeira posição do bit 0, começando do bit menos significativo
(macro de função genérica por tipo)
[ stdc_first_trailing_one](<https://en.cppreference.com/mwiki/index.php?title=c/numeric/bit/stdc_first_trailing_one&action=edit&redlink=1> "c/numeric/bit/stdc first trailing one \(page does not exist\)")(C23) | encontra a primeira posição do bit 1, começando do bit menos significativo
(macro de função genérica por tipo)
[ stdc_count_zeros](<https://en.cppreference.com/mwiki/index.php?title=c/numeric/bit/stdc_count_zeros&action=edit&redlink=1> "c/numeric/bit/stdc count zeros \(page does not exist\)")(C23) | conta o número de bits 0 em um inteiro sem sinal
(macro de função genérica por tipo)
[ stdc_count_ones](<https://en.cppreference.com/mwiki/index.php?title=c/numeric/bit/stdc_count_ones&action=edit&redlink=1> "c/numeric/bit/stdc count ones \(page does not exist\)")(C23) | conta o número de bits 1 em um inteiro sem sinal
(macro de função genérica por tipo)
[ stdc_has_single_bit](<https://en.cppreference.com/mwiki/index.php?title=c/numeric/bit/stdc_has_single_bit&action=edit&redlink=1> "c/numeric/bit/stdc has single bit \(page does not exist\)")(C23) | verifica se um número é uma potência integral de 2
(macro de função genérica por tipo)
[ stdc_bit_width](<https://en.cppreference.com/mwiki/index.php?title=c/numeric/bit/stdc_bit_width&action=edit&redlink=1> "c/numeric/bit/stdc bit width \(page does not exist\)")(C23) | encontra o menor número de bits necessários para representar o valor dado
(macro de função genérica por tipo)
[ stdc_bit_floor](<https://en.cppreference.com/mwiki/index.php?title=c/numeric/bit/stdc_bit_floor&action=edit&redlink=1> "c/numeric/bit/stdc bit floor \(page does not exist\)")(C23) | encontra a maior potência integral de 2 não maior que o valor dado
(macro de função genérica por tipo)
[ stdc_bit_ceil](<https://en.cppreference.com/mwiki/index.php?title=c/numeric/bit/stdc_bit_ceil&action=edit&redlink=1> "c/numeric/bit/stdc bit ceil \(page does not exist\)")(C23) | encontra a menor potência integral de 2 não menor que o valor dado
(macro de função genérica por tipo)

### Constantes de macro
---
Definido no cabeçalho `[`<stdbit.h>`](<#/doc/numeric>)`
[ __STDC_ENDIAN_LITTLE____STDC_ENDIAN_BIG__ __STDC_ENDIAN_NATIVE__](<#/doc/numeric/endian>)(C23) | indica a ordem de bytes (endianness) de tipos escalares
(constante de macro)

### Referências

* Padrão C23 (ISO/IEC 9899:2024):

* 7.18 Utilitários de bit e byte <stdbit.h>

### Veja também

[Documentação C++](<#/>) para Manipulação de bits
---