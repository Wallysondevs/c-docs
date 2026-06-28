# wcsrtombs, wcsrtombs_s

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
size_t wcsrtombs( char *dst, const wchar_t **src, size_t len, mbstate_t* ps );  // desde C95
(até C99)  // até C99
size_t wcsrtombs( char *restrict dst, const wchar_t **restrict src, size_t len,
mbstate_t *restrict ps );  // desde C99
errno_t wcsrtombs_s( size_t *restrict retval, char *restrict dst, rsize_t dstsz,
const wchar_t **restrict src, rsize_t len,
mbstate_t *restrict ps );  // desde C11
```

  
1) Converte uma sequência de caracteres largos do array cujo primeiro elemento é apontado por *src para sua representação multibyte estreita que começa no estado de conversão descrito por *ps. Se `dst` não for nulo, os caracteres convertidos são armazenados nos elementos sucessivos do array de `char` apontado por `dst`. Não mais que `len` bytes são escritos no array de destino. Cada caractere é convertido como se por uma chamada para [wcrtomb](<#/doc/string/multibyte/wcrtomb>). A conversão para se: 

  * O caractere nulo L'\0' foi convertido e armazenado. Os bytes armazenados neste caso são a sequência de "unshift" (se necessário) seguida por '\0', *src é definido para o valor de ponteiro nulo e *ps representa o estado de deslocamento inicial. 
  * Um wchar_t foi encontrado que não corresponde a um caractere válido na localidade C atual. *src é definido para apontar para o primeiro caractere largo não convertido. 
  * o próximo caractere multibyte a ser armazenado excederia `len`. *src é definido para apontar para o primeiro caractere largo não convertido. Esta condição não é verificada se `dst` for um ponteiro nulo.

2) O mesmo que (1), exceto que 

  * a função retorna seu resultado como um parâmetro de saída `retval`
  * se a conversão parar sem escrever um caractere nulo, a função armazenará '\0' no próximo byte em `dst`, que pode ser dst[len] ou dst[dstsz], o que ocorrer primeiro (significando que até len+1/dstsz+1 bytes totais podem ser escritos). Neste caso, pode não haver sequência de "unshift" escrita antes do nulo terminador. 
  * a função sobrescreve o array de destino a partir do nulo terminador e até `dstsz`
  * Se `src` e `dst` se sobrepuserem, o comportamento é não especificado. 
  * os seguintes erros são detectados em tempo de execução e chamam a função [constraint handler](<#/doc/error/set_constraint_handler_s>) atualmente instalada: 

    

  * `retval`, `ps`, `src`, ou *src é um ponteiro nulo 
  * `dstsz` ou `len` é maior que RSIZE_MAX (a menos que `dst` seja nulo) 
  * `dstsz` não é zero (a menos que `dst` seja nulo) 
  * `len` é maior que `dstsz` e a conversão não encontra nulo ou erro de codificação no array `src` até que `dstsz` seja atingido (a menos que `dst` seja nulo) 

    Assim como todas as funções com verificação de limites, `wcsrtombs_s` é garantida para estar disponível apenas se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir [`<wchar.h>`](<#/doc/string/wide>).

### Parâmetros

dst  |  \-  |  ponteiro para array de caracteres estreitos onde os caracteres multibyte serão armazenados   
src  |  \-  |  ponteiro para ponteiro para o primeiro elemento de uma string larga terminada em nulo   
len  |  \-  |  número de bytes disponíveis no array apontado por dst   
ps  |  \-  |  ponteiro para o objeto de estado de conversão   
dstsz  |  \-  |  número máximo de bytes que serão escritos (tamanho do array `dst`)   
retval  |  \-  |  ponteiro para um objeto [size_t](<#/doc/types/size_t>) onde o resultado será armazenado   
  
### Valor de retorno

1) Em caso de sucesso, retorna o número de bytes (incluindo quaisquer sequências de deslocamento, mas excluindo o '\0' terminador) escritos no array de caracteres cujo primeiro elemento é apontado por `dst`. Se `dst` for um ponteiro nulo, retorna o número de bytes que teriam sido escritos. Em caso de erro de conversão (se um caractere largo inválido for encontrado), retorna ([size_t](<#/doc/types/size_t>))-1, armazena [EILSEQ](<#/doc/error/errno_macros>) em [errno](<#/doc/error/errno>), e deixa *ps em estado não especificado.

2) Retorna zero em caso de sucesso (neste caso, o número de bytes, excluindo o zero terminador, que foram ou seriam escritos em `dst`, é armazenado em *retval), diferente de zero em caso de erro. Em caso de violação de restrição em tempo de execução, armazena ([size_t](<#/doc/types/size_t>))-1 em *retval (a menos que `retval` seja nulo) e define dst[0] para '\0' (a menos que `dst` seja nulo ou `dstmax` seja zero ou maior que RSIZE_MAX)

### Exemplo

Run this code
```c
    #include <stdio.h>
    #include <locale.h>
    #include <string.h>
    #include <wchar.h>
    
    void print_wide(const wchar_t* wstr)
    {
        mbstate_t state;
        memset(&state, 0, sizeof state);
        size_t len = 1 + wcsrtombs(NULL, &wstr, 0, &state);
        char mbstr[len];
        wcsrtombs(mbstr, &wstr, len, &state);
        printf("Multibyte string: %s\n", mbstr);
        printf("Length, including '\\0': %zu\n", len);
    }
    
    int main(void)
    {
        setlocale(LC_ALL, "en_US.utf8");
        print_wide(L"z\u00df\u6c34\U0001f34c"); // ou L"zß水🍌"
    }
```

Saída: 
```
    Multibyte string: zß水🍌
    Length, including '\0': 11
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.29.6.4.2 A função wcsrtombs (p: 324-325) 

    

  * K.3.9.3.2.2 A função wcsrtombs_s (p: 471-472) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.29.6.4.2 A função wcsrtombs (p: 446) 

    

  * K.3.9.3.2.2 A função wcsrtombs_s (p: 649-651) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.24.6.4.2 A função wcsrtombs (p: 392) 

### Veja também

[ wcstombswcstombs_s](<#/doc/string/multibyte/wcstombs>)(C11) |  converte uma string larga para uma string de caracteres multibyte estreitos   
(função)  
[ wcrtombwcrtomb_s](<#/doc/string/multibyte/wcrtomb>)(C95)(C11) |  converte um caractere largo para sua representação multibyte, dado o estado   
(função)  
[ mbsrtowcsmbsrtowcs_s](<#/doc/string/multibyte/mbsrtowcs>)(C95)(C11) |  converte uma string de caracteres multibyte estreitos para uma string larga, dado o estado   
(função)  
[Documentação C++](<#/>) para wcsrtombs