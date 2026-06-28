# mbsrtowcs, mbsrtowcs_s

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
size_t mbsrtowcs( wchar_t* dst, const char** src, size_t len, mbstate_t* ps );  // desde C95
(ate C99)  // ate C99
size_t mbsrtowcs( wchar_t *restrict dst, const char **restrict src, size_t len,
mbstate_t *restrict ps );  // desde C99
errno_t mbsrtowcs_s( size_t *restrict retval,
wchar_t *restrict dst, rsize_t dstsz,
const char **restrict src, rsize_t len,
mbstate_t *restrict ps );  // desde C11
```

  
1) Converte uma sequência de caracteres multibyte terminada em nulo, que começa no estado de conversão descrito por `*ps`, do array cujo primeiro elemento é apontado por *src para sua representação de caractere largo. Se `dst` não for nulo, os caracteres convertidos são armazenados nos elementos sucessivos do array de `wchar_t` apontado por `dst`. Não mais do que `len` caracteres largos são escritos no array de destino. Cada caractere multibyte é convertido como se por uma chamada para [mbrtowc](<#/doc/string/multibyte/mbrtowc>). A conversão para se: 

  * O caractere nulo multibyte foi convertido e armazenado. *src é definido para o valor de ponteiro nulo e `*ps` representa o estado de deslocamento inicial. 
  * Um caractere multibyte inválido (de acordo com a localidade C atual) foi encontrado. *src é definido para apontar para o início do primeiro caractere multibyte não convertido. 
  * o próximo caractere largo a ser armazenado excederia `len`. *src é definido para apontar para o início do primeiro caractere multibyte não convertido. Esta condição não é verificada se `dst` for um ponteiro nulo.

2) O mesmo que (1), exceto que 

  * a função retorna seu resultado como um parâmetro de saída `retval`
  * se nenhum caractere nulo foi escrito em `dst` após `len` caracteres largos terem sido escritos, então L'\0' é armazenado em `dst[len]`, o que significa que um total de len+1 caracteres largos são escritos 
  * a função sobrescreve o array de destino a partir do nulo terminador e até `dstsz`
  * Se `src` e `dst` se sobrepuserem, o comportamento é não especificado. 
  * os seguintes erros são detectados em tempo de execução e chamam a função [constraint handler](<#/doc/error/set_constraint_handler_s>) atualmente instalada: 

    

  * `retval`, `ps`, `src`, ou *src é um ponteiro nulo 
  * `dstsz` ou `len` é maior que RSIZE_MAX/sizeof(wchar_t) (a menos que `dst` seja nulo) 
  * `dstsz` não é zero (a menos que `dst` seja nulo) 
  * Não há caractere nulo nos primeiros `dstsz` caracteres multibyte no array *src e `len` é maior que `dstsz` (a menos que `dst` seja nulo) 

    Assim como todas as funções com verificação de limites, `mbsrtowcs_s` só é garantida como disponível se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir [`<wchar.h>`](<#/doc/string/wide>).

### Parâmetros

dst  |  \-  |  ponteiro para array de caracteres largos onde os resultados serão armazenados   
src  |  \-  |  ponteiro para ponteiro para o primeiro elemento de uma string multibyte terminada em nulo   
len  |  \-  |  número de caracteres largos disponíveis no array apontado por dst   
ps  |  \-  |  ponteiro para o objeto de estado de conversão   
dstsz  |  \-  |  número máximo de caracteres largos que serão escritos (tamanho do array `dst`)   
retval  |  \-  |  ponteiro para um objeto size_t onde o resultado será armazenado   
  
### Valor de retorno

1) Em caso de sucesso, retorna o número de caracteres largos, excluindo o L'\0' terminador, escritos no array de caracteres. Se `dst` for um ponteiro nulo, retorna o número de caracteres largos que teriam sido escritos dada uma extensão ilimitada. Em caso de erro de conversão (se um caractere multibyte inválido for encontrado), retorna ([size_t](<#/doc/types/size_t>))-1, armazena [EILSEQ](<#/doc/error/errno_macros>) em [errno](<#/doc/error/errno>), e deixa *ps em estado não especificado.

2) zero em caso de sucesso (nesse caso, o número de caracteres largos, excluindo o zero terminador, que foram ou seriam escritos em `dst`, é armazenado em *retval), diferente de zero em caso de erro. Em caso de violação de restrição em tempo de execução, armazena ([size_t](<#/doc/types/size_t>))-1 em *retval (a menos que `retval` seja nulo) e define dst[0] como L'\0' (a menos que `dst` seja nulo ou `dstmax` seja zero ou maior que RSIZE_MAX)

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <locale.h>
    #include <wchar.h>
    #include <string.h>
    
    void print_as_wide(const char* mbstr)
    {
        mbstate_t state;
        memset(&state, 0, sizeof state);
        size_t len = 1 + mbsrtowcs(NULL, &mbstr, 0, &state);
        wchar_t wstr[len];
        mbsrtowcs(&wstr[0], &mbstr, len, &state);
        wprintf(L"Wide string: %ls \n", wstr);
        wprintf(L"The length, including L'\\0': %zu\n", len);
    }
    
    int main(void)
    {
        setlocale(LC_ALL, "en_US.utf8");
        print_as_wide(u8"z\u00df\u6c34\U0001f34c"); // u8"zß水🍌"
    }
```

Saída: 
```
    Wide string: zß水🍌
    The length, including L'\0': 5
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.29.6.4.1 A função mbsrtowcs (p: 445) 

    

  * K.3.9.3.2.1 A função mbsrtowcs_s (p: 648-649) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.24.6.4.1 A função mbsrtowcs (p: 391) 

### Veja também

[ mbstowcsmbstowcs_s](<#/doc/string/multibyte/mbstowcs>)(C11) | converte uma string de caracteres multibyte estreita para string larga   
(função)  
[ mbrtowc](<#/doc/string/multibyte/mbrtowc>)(C95) | converte o próximo caractere multibyte para caractere largo, dado o estado   
(função)  
[ wcsrtombswcsrtombs_s](<#/doc/string/multibyte/wcsrtombs>)(C95)(C11) | converte uma string larga para string de caracteres multibyte estreita, dado o estado   
(função)  
[Documentação C++](<#/>) para mbsrtowcs