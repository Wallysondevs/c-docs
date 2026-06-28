# c32rtomb

Definido no cabeçalho [`<uchar.h>`](<#/doc/string/multibyte>)

```c
size_t c32rtomb( char* restrict s, char32_t c32, mbstate_t* restrict ps );  // desde C11
```

Converte um único ponto de código de sua representação de caractere largo de 32 bits de comprimento variável (mas tipicamente, UTF-32) para sua representação de caractere multibyte estreito.

Se s não for um ponteiro nulo, a função determina o número de bytes necessários para armazenar a representação de caractere multibyte de c32 (incluindo quaisquer sequências de mudança, e levando em conta o estado de conversão multibyte atual *ps), e armazena a representação de caractere multibyte no array de caracteres cujo primeiro elemento é apontado por s, atualizando *ps conforme necessário. No máximo MB_CUR_MAX bytes podem ser escritos por esta função.

Se s for um ponteiro nulo, a chamada é equivalente a c32rtomb(buf, U'\0', ps) para algum buffer interno `buf`.

Se c32 for o caractere largo nulo U'\0', um byte nulo é armazenado, precedido por qualquer sequência de mudança necessária para restaurar o estado de mudança inicial e o parâmetro de estado de conversão *ps é atualizado para representar o estado de mudança inicial.

Se a macro __STDC_UTF_32__ for definida, a codificação de 32 bits usada por esta função é UTF-32; caso contrário, é definida pela implementação. A macro é sempre definida e a codificação é sempre UTF-32.(desde C23) Em qualquer caso, a codificação de caractere multibyte usada por esta função é especificada pela localidade C atualmente ativa.

### Parâmetros

- **s** — ponteiro para array de caracteres estreitos onde o caractere multibyte será armazenado
- **c32** — o caractere largo de 32 bits a ser convertido
- **ps** — ponteiro para o objeto de estado de conversão usado ao interpretar a string multibyte

### Valor de retorno

Em caso de sucesso, retorna o número de bytes (incluindo quaisquer sequências de mudança) escritos no array de caracteres cujo primeiro elemento é apontado por s. Este valor pode ser ​0​, por exemplo, ao processar as unidades char32_t iniciais em uma sequência de múltiplas unidades char32_t (não ocorre em UTF-32).

Em caso de falha (se c32 não for um caractere largo de 32 bits válido), retorna -1, armazena [EILSEQ](<#/doc/error/errno_macros>) em [errno](<#/doc/error/errno>), e deixa *ps em estado não especificado.

### Exemplo

Execute este código
```c
    #include <locale.h>
    #include <stdio.h>
    #include <stdlib.h>
    #include <uchar.h>
    
    mbstate_t state;
    
    int main(void)
    {
        setlocale(LC_ALL, "en_US.utf8");
        const char32_t in[] = U"zß水🍌"; // or "z\u00df\u6c34\U0001F34C"
        size_t in_sz = sizeof in / sizeof *in;
    
        printf("Processing %zu UTF-32 code units: [ ", in_sz);
        for (size_t n = 0; n < in_sz; ++n)
            printf("%#x ", in[n]);
        puts("]");
    
        char out[MB_CUR_MAX * in_sz];
        char* p = out;
        for (size_t n = 0; n < in_sz; ++n)
        {
            size_t rc = c32rtomb(p, in[n], &state);
            if(rc == (size_t)-1) break;
            p += rc;
        }
    
        size_t out_sz = p - out;
        printf("into %zu UTF-8 code units: [ ", out_sz);
        for (size_t x = 0; x < out_sz; ++x)
            printf("%#x ", +(unsigned char)out[x]);
        puts("]");
    }
```

Saída:
```
    Processing 5 UTF-32 code units: [ 0x7a 0xdf 0x6c34 0x1f34c 0 ]
    into 11 UTF-8 code units: [ 0x7a 0xc3 0x9f 0xe6 0xb0 0xb4 0xf0 0x9f 0x8d 0x8c 0 ]
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.30.1.6 A função c32rtomb (p: 411)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.28.1.4 A função c32rtomb (p: 401)

### Veja também

[ mbrtoc32](<#/doc/string/multibyte/mbrtoc32>)(C11) | converte um caractere multibyte estreito para codificação UTF-32
(função)
[Documentação C++](<#/>) para c32rtomb