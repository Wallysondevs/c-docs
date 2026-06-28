# c16rtomb

Definido no cabeçalho [`<uchar.h>`](<#/doc/string/multibyte>)

```c
size_t c16rtomb( char* restrict s, char16_t c16, mbstate_t* restrict ps );  // desde C11
```

Converte um único ponto de código de sua representação de caractere largo de 16 bits de comprimento variável (tipicamente, UTF-16) para sua representação de caractere multibyte estreito.

Se s não for um ponteiro nulo e c16 for a última unidade de código de 16 bits em uma codificação de comprimento variável válida de um ponto de código, a função determina o número de bytes necessários para armazenar a representação de caractere multibyte desse ponto de código (incluindo quaisquer sequências de mudança, e levando em consideração o estado de conversão multibyte atual *ps), e armazena a representação de caractere multibyte no array de caracteres cujo primeiro elemento é apontado por s, atualizando *ps conforme necessário. No máximo MB_CUR_MAX bytes podem ser escritos por esta função.

Se s for um ponteiro nulo, a chamada é equivalente a c16rtomb(buf, u'\0', ps) para algum buffer interno `buf`.

Se c16 for o caractere largo nulo u'\0', um byte nulo é armazenado, precedido por qualquer sequência de mudança necessária para restaurar o estado de mudança inicial e o parâmetro de estado de conversão *ps é atualizado para representar o estado de mudança inicial.

Se c16 não for a unidade de código final em uma representação de 16 bits de um caractere largo, ele não escreve no array apontado por s, apenas *ps é atualizado.

Se a macro __STDC_UTF_16__ for definida, a codificação de 16 bits usada por esta função é UTF-16; caso contrário, é definida pela implementação. A macro é sempre definida e a codificação é sempre UTF-16.(desde C23) Em qualquer caso, a codificação de caractere multibyte usada por esta função é especificada pela localidade C atualmente ativa.

### Parâmetros

- **s** — ponteiro para um array de caracteres estreitos onde o caractere multibyte será armazenado
- **c16** — o caractere largo de 16 bits a ser convertido
- **ps** — ponteiro para o objeto de estado de conversão usado ao interpretar a string multibyte

### Valor de retorno

Em caso de sucesso, retorna o número de bytes (incluindo quaisquer sequências de mudança) escritos no array de caracteres cujo primeiro elemento é apontado por s. Este valor pode ser ​0​, por exemplo, ao processar as unidades char16_t iniciais em uma sequência de múltiplas unidades char16_t (ocorre ao processar o substituto inicial em um par substituto de UTF-16).

Em caso de falha (se c16 não for uma unidade de código de 16 bits válida), retorna -1, armazena [EILSEQ](<#/doc/error/errno_macros>) em [errno](<#/doc/error/errno>), e deixa *ps em estado não especificado.

### Observações

No C11 conforme publicado, ao contrário de [mbrtoc16](<#/doc/string/multibyte/mbrtoc16>), que converte multibyte de largura variável (como UTF-8) para codificação de 16 bits de largura variável (como UTF-16), esta função só pode converter codificação de 16 bits de unidade única, o que significa que ela não pode converter UTF-16 para UTF-8, apesar de ser essa a intenção original desta função. Isso foi corrigido pelo relatório de defeito pós-C11 [DR488](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2059.htm#dr_488>).

### Exemplo

Nota: este exemplo assume que a correção para o relatório de defeito [DR488](<https://open-std.org/JTC1/SC22/WG14/www/docs/n2059.htm#dr_488>) foi aplicada

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
        const char16_t in[] = u"zß水🍌"; // or "z\u00df\u6c34\U0001F34C"
        const size_t in_sz = sizeof in / sizeof *in;
     
        printf("Processing %zu UTF-16 code units: [ ", in_sz);
        for (size_t n = 0; n < in_sz; ++n)
            printf("%#x ", in[n]);
        puts("]");
     
        char out[MB_CUR_MAX * in_sz];
        char *p = out;
        for (size_t n = 0; n < in_sz; ++n)
        {
            size_t rc = c16rtomb(p, in[n], &state);
            if (rc == (size_t)-1)
                break;
            p += rc;
        }
     
        size_t out_sz = p - out;
        printf("into %zu UTF-8 code units: [ ", out_sz);
        for (size_t x = 0; x < out_sz; ++x)
            printf("%#x ", +(unsigned char)out[x]);
        puts("]");
    }
```

Output:
```
    Processing 6 UTF-16 code units: [ 0x7a 0xdf 0x6c34 0xd83c 0xdf4c 0 ]
    into 11 UTF-8 code units: [ 0x7a 0xc3 0x9f 0xe6 0xb0 0xb4 0xf0 0x9f 0x8d 0x8c 0 ]
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.28.1.2 A função c16rtomb (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.28.1.2 A função c16rtomb (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.28.1.2 A função c16rtomb (p: 399-400)

### Veja também

[ mbrtoc16](<#/doc/string/multibyte/mbrtoc16>)(C11) | converte um caractere multibyte estreito para codificação UTF-16
(função)
[Documentação C++](<#/>) para c16rtomb