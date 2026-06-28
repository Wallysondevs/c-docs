# wctomb, wctomb_s

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
int wctomb( char *s, wchar_t wc );
errno_t wctomb_s( int *restrict status, char *restrict s, rsize_t ssz, wchar_t wc );  // desde C11
```

1) Converte um caractere largo `wc` para codificação multibyte e o armazena (incluindo quaisquer sequências de mudança de estado) no array de `char` cujo primeiro elemento é apontado por `s`. Não mais do que `MB_CUR_MAX` caracteres são armazenados. A conversão é afetada pela categoria `LC_CTYPE` da localidade atual.

Se `wc` for o caractere nulo, o byte nulo é escrito em `s`, precedido por quaisquer sequências de mudança de estado necessárias para restaurar o estado de mudança de estado inicial.

Se `s` for um ponteiro nulo, esta função redefine o estado de conversão global e determina se sequências de mudança de estado são usadas.

2) O mesmo que (1), exceto que o resultado é retornado no parâmetro de saída `status` e os seguintes erros são detectados em tempo de execução e chamam a função [manipulador de restrição](<#/doc/error/set_constraint_handler_s>) atualmente instalada:

* `ssz` é menor que o número de bytes que seriam escritos (a menos que `s` seja nulo)
* `ssz` é maior que `RSIZE_MAX` (a menos que `s` seja nulo)
* `s` é um ponteiro nulo, mas `ssz` não é zero

Assim como todas as funções com verificação de limites, `wctomb_s` é garantida como disponível apenas se `__STDC_LIB_EXT1__` for definido pela implementação e se o usuário definir `__STDC_WANT_LIB_EXT1__` para a constante inteira 1 antes de incluir `[`<stdlib.h>`](<#/doc/program>)`.

### Notas

Cada chamada a `wctomb` atualiza o estado de conversão global interno (um objeto estático do tipo [mbstate_t](<#/doc/string/multibyte/mbstate_t>), conhecido apenas por esta função). Se a codificação multibyte usar estados de mudança, esta função não é reentrante. Em qualquer caso, múltiplas threads não devem chamar `wctomb` sem sincronização: [wcrtomb](<#/doc/string/multibyte/wcrtomb>) ou `wctomb_s` podem ser usadas em vez disso.

Ao contrário da maioria das funções com verificação de limites, `wctomb_s` não termina sua saída com nulo, porque ela é projetada para ser usada em laços que processam strings caractere por caractere.

### Parâmetros

- **s** — ponteiro para o array de caracteres para saída
- **wc** — caractere largo a ser convertido
- **ssz** — número máximo de bytes a serem escritos em `s` (tamanho do array `s`)
- **status** — ponteiro para um parâmetro de saída onde o resultado (comprimento da sequência multibyte ou o status da sequência de mudança de estado) será armazenado

### Valor de retorno

1) Se `s` não for um ponteiro nulo, retorna o número de bytes contidos na representação multibyte de `wc` ou -1 se `wc` não for um caractere válido.

Se `s` for um ponteiro nulo, redefine seu estado de conversão interno para representar o estado de mudança de estado inicial e retorna `0` se a codificação multibyte atual não for dependente de estado (não usa sequências de mudança de estado) ou um valor diferente de zero se a codificação multibyte atual for dependente de estado (usa sequências de mudança de estado).

2) zero em caso de sucesso, caso em que a representação multibyte de `wc` é armazenada em `s` e seu comprimento é armazenado em `*status`, ou, se `s` for nulo, o status da sequência de mudança de estado é armazenado em `status`). Diferente de zero em caso de erro de codificação ou violação de restrição em tempo de execução, caso em que `([size_t](<#/doc/types/size_t>))-1` é armazenado em `*status`. O valor armazenado em `*status` nunca excede `MB_CUR_MAX`.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
    #include <locale.h>
    
    void demo(wchar_t wc)
    {
        const char* dep = wctomb(NULL, wc) ? "Yes" : "No";
        printf("State-dependent encoding? %s.\n", dep);
    
        char mb[MB_CUR_MAX];
        int len = wctomb(mb, wc);
        printf("wide char '%lc' -> multibyte char [", wc);
        for (int idx = 0; idx < len; ++idx)
            printf("%s%#2x", idx ? " " : "", (unsigned char)mb[idx]);
        printf("]\n");
    }
    
    int main(void)
    {
        setlocale(LC_ALL, "en_US.utf8");
        printf("MB_CUR_MAX = %zu\n", MB_CUR_MAX);
        demo(L'A');
        demo(L'\u00df');
        demo(L'\U0001d10b');
    }
```

Saída possível:
```
    MB_CUR_MAX = 6
    State-dependent encoding? No.
    wide char 'A' -> multibyte char [0x41]
    State-dependent encoding? No.
    wide char 'ß' -> multibyte char [0xc3 0x9f]
    State-dependent encoding? No.
    wide char '𝄋' -> multibyte char [0xf0 0x9d 0x84 0x8b]
```

### Referências

* Padrão C17 (ISO/IEC 9899:2018):

  * 7.22.7.3 A função wctomb (p: 261)

  * K.3.6.4.1 A função wctomb_s (p: 443)

* Padrão C11 (ISO/IEC 9899:2011):

  * 7.22.7.3 A função wctomb (p: 358-359)

  * K.3.6.4.1 A função wctomb_s (p: 610-611)

* Padrão C99 (ISO/IEC 9899:1999):

  * 7.20.7.3 A função wctomb (p: 322-323)

* Padrão C89/C90 (ISO/IEC 9899:1990):

  * 4.10.7.3 A função wctomb

### Veja também

[ mbtowc](<#/doc/string/multibyte/mbtowc>) | converte o próximo caractere multibyte para caractere largo
(função)
[ wcrtombwcrtomb_s](<#/doc/string/multibyte/wcrtomb>)(C95)(C11) | converte um caractere largo para sua representação multibyte, dado o estado
(função)
[Documentação C++](<#/>) para wctomb