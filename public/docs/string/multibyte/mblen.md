# mblen

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
int mblen( const char* s, `size_t` n );
```

Determina o tamanho, em bytes, do caractere multibyte cujo primeiro byte é apontado por `s`.

Se `s` for um ponteiro nulo, redefine o estado de conversão global e (até C23) determina se sequências de mudança (shift sequences) são usadas.

Esta função é equivalente à chamada [`mbtowc`](<#/doc/string/multibyte/mbtowc>)((wchar_t*)0, s, n), exceto que o estado de conversão de [`mbtowc`](<#/doc/string/multibyte/mbtowc>) não é afetado.

### Parâmetros

- **s** — ponteiro para o caractere multibyte
- **n** — limite no número de bytes em s que podem ser examinados

### Valor de retorno

Se `s` não for um ponteiro nulo, retorna o número de bytes contidos no caractere multibyte ou -1 se os primeiros bytes apontados por `s` não formarem um caractere multibyte válido ou ​0​ se `s` estiver apontando para o caractere nulo '\0'.

Se `s` for um ponteiro nulo, redefine seu estado de conversão interno para representar o estado de mudança inicial e (até C23) retorna ​0​ se a codificação multibyte atual não for dependente de estado (não usa sequências de mudança) ou um valor diferente de zero se a codificação multibyte atual for dependente de estado (usa sequências de mudança).

### Observações

Cada chamada para `mblen` atualiza o estado de conversão global interno (um objeto estático do tipo [`mbstate_t`](<#/doc/string/multibyte/mbstate_t>), conhecido apenas por esta função). Se a codificação multibyte usar estados de mudança, deve-se ter cuidado para evitar retrocessos ou múltiplas varreduras. Em qualquer caso, múltiplas threads não devem chamar `mblen` sem sincronização: [`mbrlen`](<#/doc/string/multibyte/mbrlen>) pode ser usado em vez disso. | (até C23)
`mblen` não tem permissão para ter um estado interno. | (desde C23)

### Exemplo

Execute este código
```c
    #include <locale.h>
    #include <stdio.h>
    #include <stdlib.h>
    #include <string.h>
    
    // o número de caracteres em uma string multibyte é a soma dos mblen()'s
    // nota: a abordagem mais simples é mbstowcs(NULL, str, sz)
    size_t strlen_mb(const char* ptr)
    {
        size_t result = 0;
        const char* end = ptr + strlen(ptr);
        mblen(NULL, 0); // redefine o estado de conversão
        while(ptr < end) {
            int next = mblen(ptr, end - ptr);
            if (next == -1) {
               perror("strlen_mb");
               break;
            }
            ptr += next;
            ++result;
        }
        return result;
    }
    
    void dump_bytes(const char* str)
    {
        for (const char* end = str + strlen(str); str != end; ++str)
            printf("%02X ", (unsigned char)str[0]);
        printf("\n");
    }
    
    int main(void)
    {
        setlocale(LC_ALL, "en_US.utf8");
        const char* str = "z\u00df\u6c34\U0001f34c";
        printf("A string \"%s\" consiste em %zu caracteres, mas %zu bytes: ",
                str, strlen_mb(str), strlen(str));
        dump_bytes(str);
    }
```

Saída possível:
```
    The string "zß水🍌" consists of 4 characters, but 10 bytes: 7A C3 9F E6 B0 B4 F0 9F 8D 8C
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.22.7.1 A função mblen (p: 260)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.22.7.1 A função mblen (p: 357)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.20.7.1 A função mblen (p: 321)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.10.7.1 A função mblen

### Veja também

[`mbtowc`](<#/doc/string/multibyte/mbtowc>) | converte o próximo caractere multibyte para caractere largo
(função)
[`mbrlen`](<#/doc/string/multibyte/mbrlen>)(C95) | retorna o número de bytes no próximo caractere multibyte, dado o estado
(função)
[Documentação C++](<#/>) para mblen