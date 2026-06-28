# mbstowcs, mbstowcs_s

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
size_t mbstowcs( wchar_t *dst, const char *src, size_t len)  // até C99
size_t mbstowcs( wchar_t *restrict dst, const char *restrict src, size_t len)  // desde C99
errno_t mbstowcs_s(size_t *restrict retval, wchar_t *restrict dst,
rsize_t dstsz, const char *restrict src, rsize_t len);  // desde C11
```

1) Converte uma string de caracteres multibyte do array cujo primeiro elemento é apontado por `src` para sua representação de caracteres largos. Caracteres convertidos são armazenados nos elementos sucessivos do array apontado por `dst`. Não mais que `len` caracteres largos são escritos no array de destino.

Cada caractere é convertido como se por uma chamada a [mbtowc](<#/doc/string/multibyte/mbtowc>), exceto que o estado de conversão de mbtowc não é afetado. A conversão para se:

* O caractere nulo multibyte foi convertido e armazenado.

* Um caractere multibyte inválido (na localidade C atual) foi encontrado.

* O próximo caractere largo a ser armazenado excederia `len`.

Se `src` e `dst` se sobrepõem, o comportamento é indefinido.

2) O mesmo que (1), exceto que

* a conversão é como se por [mbrtowc](<#/doc/string/multibyte/mbrtowc>), não [mbtowc](<#/doc/string/multibyte/mbtowc>)

* a função retorna seu resultado como um parâmetro de saída `retval`

* se nenhum caractere nulo foi escrito em `dst` após `len` caracteres largos terem sido escritos, então `L'\0'` é armazenado em `dst[len]`, o que significa que um total de `len+1` caracteres largos são escritos

* se `dst` é um ponteiro nulo, o número de caracteres largos que seriam produzidos é armazenado em `*retval`

* a função sobrescreve o array de destino a partir do nulo terminador e até `dstsz`

* Se `src` e `dst` se sobrepõem, o comportamento é não especificado.

* os seguintes erros são detectados em tempo de execução e chamam a função [constraint handler](<#/doc/error/set_constraint_handler_s>) atualmente instalada:

  * `retval` ou `src` é um ponteiro nulo
  * `dstsz` ou `len` é maior que `RSIZE_MAX/sizeof(wchar_t)` (a menos que `dst` seja nulo)
  * `dstsz` não é zero (a menos que `dst` seja nulo)
  * Não há caractere nulo nos primeiros `dstsz` caracteres multibyte no array `src` e `len` é maior que `dstsz` (a menos que `dst` seja nulo)

    Assim como todas as funções com verificação de limites, `mbstowcs_s` tem sua disponibilidade garantida apenas se `__STDC_LIB_EXT1__` for definido pela implementação e se o usuário definir `__STDC_WANT_LIB_EXT1__` para a constante inteira 1 antes de incluir [`<stdlib.h>`](<#/doc/program>).

### Notas

Na maioria das implementações, `mbstowcs` atualiza um objeto estático global do tipo [mbstate_t](<#/doc/string/multibyte/mbstate_t>) à medida que processa a string, e não pode ser chamada simultaneamente por duas threads; [mbsrtowcs](<#/doc/string/multibyte/mbsrtowcs>) deve ser usada em tais casos.

POSIX especifica uma extensão comum: se `dst` é um ponteiro nulo, esta função retorna o número de caracteres largos que seriam escritos em `dst`, se convertidos. Comportamento similar é padrão para `mbstowcs_s` e para [mbsrtowcs](<#/doc/string/multibyte/mbsrtowcs>).

### Parâmetros

- **dst** — ponteiro para o array de caracteres largos onde a string larga será armazenada
- **src** — ponteiro para o primeiro elemento de uma string multibyte terminada em nulo a ser convertida
- **len** — número de caracteres largos disponíveis no array apontado por dst
- **dstsz** — número máximo de caracteres largos que serão escritos (tamanho do array `dst`)
- **retval** — ponteiro para um objeto size_t onde o resultado será armazenado

### Valor de retorno

1) Em caso de sucesso, retorna o número de caracteres largos, excluindo o `L'\0'` terminador, escritos no array de destino. Em caso de erro de conversão (se um caractere multibyte inválido foi encontrado), retorna ([size_t](<#/doc/types/size_t>))-1.

2) zero em caso de sucesso (neste caso, o número de caracteres largos, excluindo o zero terminador, que foram, ou seriam escritos em `dst`, é armazenado em `*retval`), diferente de zero em caso de erro. Em caso de violação de restrição em tempo de execução, armazena ([size_t](<#/doc/types/size_t>))-1 em `*retval` (a menos que `retval` seja nulo) e define `dst[0]` como `L'\0'` (a menos que `dst` seja nulo ou `dstmax` seja zero ou maior que `RSIZE_MAX`).

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <locale.h>
    #include <stdlib.h>
    #include <wchar.h>
    
    int main(void)
    {
        setlocale(LC_ALL, "en_US.utf8");
        const char* mbstr = u8"z\u00df\u6c34\U0001F34C"; // or u8"zß水🍌"
        wchar_t wstr[5];
        mbstowcs(wstr, mbstr, 5);
        wprintf(L"MB string: %s\n", mbstr);
        wprintf(L"Wide string: %ls\n", wstr);
    }
```

Saída:
```
    MB string: zß水🍌
    Wide string: zß水🍌
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    * 7.22.8.1 A função mbstowcs (p: 359)

    * K.3.6.5.1 A função mbstowcs_s (p: 611-612)

  * Padrão C99 (ISO/IEC 9899:1999):

    * 7.20.8.1 A função mbstowcs (p: 323)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    * 4.10.8.1 A função mbstowcs

### Veja também

[ mbsrtowcsmbsrtowcs_s](<#/doc/string/multibyte/mbsrtowcs>)(C95)(C11) | converte uma string de caracteres multibyte estreita para string larga, dado o estado
(função)
[ wcstombswcstombs_s](<#/doc/string/multibyte/wcstombs>)(C11) | converte uma string larga para string de caracteres multibyte estreita
(função)
[Documentação C++](<#/>) para mbstowcs