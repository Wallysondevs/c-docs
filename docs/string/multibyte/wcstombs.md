# wcstombs, wcstombs_s

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
size_t wcstombs( char *dst, const wchar_t *src, size_t len );  // até C99
size_t wcstombs( char *restrict dst, const wchar_t *restrict src, size_t len );  // desde C99
errno_t wcstombs_s( size_t *restrict retval, char *restrict dst, rsize_t dstsz,
const wchar_t *restrict src, rsize_t len );  // desde C11
```

1) Converte uma sequência de caracteres largos do array cujo primeiro elemento é apontado por `src` para sua representação multibyte estreita que começa no estado de deslocamento inicial. Os caracteres convertidos são armazenados nos elementos sucessivos do array de `char` apontado por `dst`. Não mais que `len` bytes são escritos no array de destino.

Cada caractere é convertido como se por uma chamada a [wctomb](<#/doc/string/multibyte/wctomb>), exceto que o estado de conversão de wctomb não é afetado. A conversão para se:

*   O caractere nulo L'\0' foi convertido e armazenado. Os bytes armazenados neste caso são a sequência de "unshift" (se necessário) seguida por '\0',

*   Um `wchar_t` foi encontrado que não corresponde a um caractere válido na localidade C atual.

*   O próximo caractere multibyte a ser armazenado excederia `len`.

Se `src` e `dst` se sobrepõem, o comportamento é não especificado.

2) O mesmo que (1), exceto que

*   a conversão é como se por [wcrtomb](<#/doc/string/multibyte/wcrtomb>), não [wctomb](<#/doc/string/multibyte/wctomb>)

*   a função retorna seu resultado como um parâmetro de saída `retval`

*   se a conversão parar sem escrever um caractere nulo, a função armazenará '\0' no próximo byte em `dst`, que pode ser `dst[len]` ou `dst[dstsz]`, o que ocorrer primeiro (significando que até len+1/dstsz+1 bytes totais podem ser escritos). Neste caso, pode não haver sequência de "unshift" escrita antes do nulo terminador.

*   se `dst` for um ponteiro nulo, o número de bytes que seriam produzidos é armazenado em *retval

*   a função sobrescreve o array de destino a partir do nulo terminador e até `dstsz`

*   Se `src` e `dst` se sobrepõem, o comportamento é não especificado.

*   os seguintes erros são detectados em tempo de execução e chamam a função [constraint handler](<#/doc/error/set_constraint_handler_s>) atualmente instalada:

    *   `retval` ou `src` é um ponteiro nulo
    *   `dstsz` ou `len` é maior que RSIZE_MAX (a menos que `dst` seja nulo)
    *   `dstsz` não é zero (a menos que `dst` seja nulo)
    *   `len` é maior que `dstsz` e a conversão não encontra nulo ou erro de codificação no array `src` quando `dstsz` é atingido (a menos que `dst` seja nulo)

    Assim como todas as funções com verificação de limites, `wcstombs_s` é garantida de estar disponível apenas se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir [`<stdlib.h>`](<#/doc/program>).

### Notas

Na maioria das implementações, `wcstombs` atualiza um objeto estático global do tipo [mbstate_t](<#/doc/string/multibyte/mbstate_t>) à medida que processa a string, e não pode ser chamada simultaneamente por duas threads; [wcsrtombs](<#/doc/string/multibyte/wcsrtombs>) ou `wcstombs_s` devem ser usadas em tais casos.

POSIX especifica uma extensão comum: se `dst` for um ponteiro nulo, esta função retorna o número de bytes que seriam escritos em `dst`, se convertidos. Comportamento similar é padrão para [wcsrtombs](<#/doc/string/multibyte/wcsrtombs>) e `wcstombs_s`.

### Parâmetros

- **dst** — ponteiro para array de caracteres estreitos onde o caractere multibyte será armazenado
- **src** — ponteiro para o primeiro elemento de uma string larga terminada em nulo a ser convertida
- **len** — número de bytes disponíveis no array apontado por dst
- **dstsz** — número máximo de bytes que serão escritos (tamanho do array `dst`)
- **retval** — ponteiro para um objeto size_t onde o resultado será armazenado

### Valor de retorno

1) Em caso de sucesso, retorna o número de bytes (incluindo quaisquer sequências de deslocamento, mas excluindo o '\0' terminador) escritos no array de caracteres cujo primeiro elemento é apontado por `dst`. Em caso de erro de conversão (se um caractere largo inválido for encontrado), retorna ([size_t](<#/doc/types/size_t>))-1.

2) Retorna zero em caso de sucesso (caso em que o número de bytes, excluindo o zero terminador, que foram ou seriam escritos em `dst`, é armazenado em *retval), diferente de zero em caso de erro. Em caso de violação de restrição em tempo de execução, armazena ([size_t](<#/doc/types/size_t>))-1 em *retval (a menos que `retval` seja nulo) e define dst[0] como '\0' (a menos que `dst` seja nulo ou `dstmax` seja zero ou maior que RSIZE_MAX)

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
    #include <locale.h>
    
    int main(void)
    {
        // 4 wide characters
        const wchar_t src[] = L"z\u00df\u6c34\U0001f34c";
        // they occupy 10 bytes in UTF-8
        char dst[11];
    
        setlocale(LC_ALL, "en_US.utf8");
        printf("wide-character string: '%ls'\n",src);
        for (size_t ndx=0; ndx < sizeof src/sizeof src[0]; ++ndx)
            printf("   src[%2zu] = %#8x\n", ndx, src[ndx]);
    
        int rtn_val = wcstombs(dst, src, sizeof dst);
        printf("rtn_val = %d\n", rtn_val);
        if (rtn_val > 0)
            printf("multibyte string:  '%s'\n",dst);
        for (size_t ndx=0; ndx<sizeof dst; ++ndx)
            printf("   dst[%2zu] = %#2x\n", ndx, (unsigned char)dst[ndx]);
    }
```

Saída:
```
    wide-character string: 'zß水🍌'
       src[ 0] =     0x7a
       src[ 1] =     0xdf
       src[ 2] =   0x6c34
       src[ 3] =  0x1f34c
       src[ 4] =        0
    rtn_val = 10
    multibyte string:  'zß水🍌'
       dst[ 0] = 0x7a
       dst[ 1] = 0xc3
       dst[ 2] = 0x9f
       dst[ 3] = 0xe6
       dst[ 4] = 0xb0
       dst[ 5] = 0xb4
       dst[ 6] = 0xf0
       dst[ 7] = 0x9f
       dst[ 8] = 0x8d
       dst[ 9] = 0x8c
       dst[10] =  0
```

### Referências

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.22.8.2 A função wcstombs (p: 360)

    *   K.3.6.5.2 A função wcstombs_s (p: 612-614)

*   Padrão C99 (ISO/IEC 9899:1999):

    *   7.20.8.2 A função wcstombs (p: 324)

*   Padrão C89/C90 (ISO/IEC 9899:1990):

    *   4.10.8.2 A função wcstombs

### Veja também

[ wcsrtombswcsrtombs_s](<#/doc/string/multibyte/wcsrtombs>)(C95)(C11) | converte uma string larga para uma string de caracteres multibyte estreitos, dado o estado (função)
[ mbstowcsmbstowcs_s](<#/doc/string/multibyte/mbstowcs>)(C11) | converte uma string de caracteres multibyte estreitos para uma string larga (função)
[Documentação C++](<#/>) para wcstombs