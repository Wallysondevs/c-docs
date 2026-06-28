# stdc_leading_zeros

Definido no cabeçalho [`<stdbit.h>`](<#/doc/numeric>)

```c
unsigned int stdc_leading_zeros_uc( unsigned char value ) [[unsequenced]];  // desde C23
unsigned int stdc_leading_zeros_us( unsigned short value ) [[unsequenced]];  // desde C23
unsigned int stdc_leading_zeros_ui( unsigned int value ) [[unsequenced]];  // desde C23
unsigned int stdc_leading_zeros_ul( unsigned long int value ) [[unsequenced]];  // desde C23
unsigned int stdc_leading_zeros_ull( unsigned long long int value ) [[unsequenced]];  // desde C23
#define stdc_leading_zeros( value )
// interface exposta:
generic_return_type stdc_leading_zeros( generic_value_type value ) [[unsequenced]];  // desde C23
```

  
1-5) Retorna o número de bits ​0​ consecutivos no valor, começando pelo bit mais significativo.

6) A função genérica por tipo (marcada pelo seu argumento `generic_value_type`) retorna o valor apropriado com base no tipo do valor de entrada, desde que seja um(a):

  * tipo inteiro sem sinal padrão, excluindo bool;
  * tipo inteiro sem sinal estendido;
  * ou, tipo inteiro sem sinal com precisão de bit cuja largura corresponda a um tipo inteiro padrão ou estendido, excluindo bool.

O `generic_return_type` deve ser um tipo inteiro sem sinal grande e adequado, capaz de representar o resultado calculado.

### Parâmetros

- **value** — valor de tipo inteiro sem sinal
  
### Valor de retorno

O número de bits ​0​ consecutivos no valor, começando pelo bit mais significativo.

### Exemplo

Execute este código
```c
    #include <limits.h>
    #include <stdbit.h>
    #include <stdint.h>
    #include <stdio.h>
    
    #define bits_num(value) (sizeof(value) * CHAR_BIT)
    
    #define bin_impl(T, suffix) \
    const char* bin_##suffix(T x) \
    { \
        static char buf[bits_num(x) * CHAR_BIT + 1]; \
        for (T i = 0, mask = ((T)1 << (bits_num(x) - 1)); mask; mask >>= 1) \
            buf[i++] = x & mask ? '1' : '0'; \
        buf[bits_num(x)] = '\0'; \
        return buf; \
    }
    
    bin_impl(uint8_t, u8)
    bin_impl(uint16_t, u16)
    bin_impl(uint32_t, u32)
    bin_impl(uint64_t, u64)
    
    #define bin(x) _Generic((x), \
        uint8_t: bin_u8, uint16_t: bin_u16, uint32_t: bin_u32, default: bin_u64)(x)
    
    int main()
    {
        puts("uint8_t:");
        for (uint8_t x = 0b11000000; ; x >>= 1)
        {
            printf("x = [%s], leading zeros: %d\n", bin(x), stdc_leading_zeros(x));
            if (!x)
                break;
        }
    
        puts("uint16_t:");
        for (uint16_t x = 0b11000000; ; x >>= 1)
        {
            printf("x = [%s], leading zeros: %d\n", bin(x), stdc_leading_zeros(x));
            if (!x)
                break;
        }
    }
```

Saída:
```
    uint8_t:
    x = [11000000], leading zeros: 0
    x = [01100000], leading zeros: 1
    x = [00110000], leading zeros: 2
    x = [00011000], leading zeros: 3
    x = [00001100], leading zeros: 4
    x = [00000110], leading zeros: 5
    x = [00000011], leading zeros: 6
    x = [00000001], leading zeros: 7
    x = [00000000], leading zeros: 8
    uint16_t:
    x = [0000000011000000], leading zeros: 8
    x = [0000000001100000], leading zeros: 9
    x = [0000000000110000], leading zeros: 10
    x = [0000000000011000], leading zeros: 11
    x = [0000000000001100], leading zeros: 12
    x = [0000000000000110], leading zeros: 13
    x = [0000000000000011], leading zeros: 14
    x = [0000000000000001], leading zeros: 15
    x = [0000000000000000], leading zeros: 16
```

### Veja também

[ stdc_first_leading_zero](<https://en.cppreference.com/mwiki/index.php?title=c/numeric/bit/stdc_first_leading_zero&action=edit&redlink=1> "c/numeric/bit/stdc first leading zero \(page does not exist\)")(C23) | encontra a primeira posição do bit ​0​, começando pelo bit mais significativo
(macro de função genérica por tipo)
[ stdc_count_zeros](<https://en.cppreference.com/mwiki/index.php?title=c/numeric/bit/stdc_count_zeros&action=edit&redlink=1> "c/numeric/bit/stdc count zeros \(page does not exist\)")(C23) | conta o número de bits ​0​ em um inteiro sem sinal
(macro de função genérica por tipo)
[ stdc_leading_ones](<https://en.cppreference.com/mwiki/index.php?title=c/numeric/bit/stdc_leading_ones&action=edit&redlink=1> "c/numeric/bit/stdc leading ones \(page does not exist\)")(C23) | conta o número de bits 1 consecutivos, começando pelo bit mais significativo
(macro de função genérica por tipo)
[Documentação C++](<#/>) para countl_zero