# wcsncpy, wcsncpy_s

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
wchar_t* wcsncpy( wchar_t* dest, const wchar_t* src, size_t count );  // desde C95
(até C99)  // até C99
wchar_t *wcsncpy( wchar_t *restrict dest, const wchar_t *restrict src, size_t count );  // desde C99
errno_t wcsncpy_s( wchar_t *restrict dest, rsize_t destsz,
const wchar_t *restrict src, rsize_t count);  // desde C11
```

1) Copia no máximo `count` caracteres da string larga apontada por `src` (incluindo o caractere largo nulo terminador) para o array de caracteres largos apontado por `dest`.

Se `count` for atingido antes que a string `src` inteira seja copiada, o array de caracteres largos resultante não é terminado em nulo.

Se, após copiar o caractere largo nulo terminador de `src`, `count` não for atingido, caracteres largos nulos adicionais são escritos em `dest` até que o total de `count` caracteres tenha sido escrito.

Se as strings se sobrepuserem, o comportamento é indefinido.

2) O mesmo que (1), exceto que a função não continua escrevendo zeros no array de destino para preencher até `count`, ela para após escrever o caractere nulo terminador (se não houver nulo na origem, ela escreve um em dest[count] e então para). Além disso, os seguintes erros são detectados em tempo de execução e chamam a função [constraint handler](<#/doc/error/set_constraint_handler_s>) atualmente instalada:

*   `src` ou `dest` é um ponteiro nulo`
*   `destsz` ou `count` é zero ou maior que RSIZE_MAX/sizeof(wchar_t)`
*   `count` é maior ou igual a `destsz`, mas `destsz` é menor ou igual a wcsnlen_s(src, count), em outras palavras, ocorreria truncamento`
*   `ocorreria sobreposição entre as strings de origem e destino`

Assim como todas as funções com verificação de limites, `wcsncpy_s` tem sua disponibilidade garantida apenas se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir `[`<wchar.h>`](<#/doc/string/wide>)`.

### Parâmetros

- **dest** — ponteiro para o array de caracteres largos para o qual copiar
- **src** — ponteiro para a string larga da qual copiar
- **count** — número máximo de caracteres largos a copiar
- **destsz** — o tamanho do buffer de destino

### Valor de retorno

1) retorna uma cópia de `dest`

2) retorna zero em caso de sucesso, retorna um valor diferente de zero em caso de erro. Além disso, em caso de erro, escreve L'\0' em dest[0] (a menos que `dest` seja um ponteiro nulo ou `destsz` seja zero ou maior que RSIZE_MAX/sizeof(wchar_t)) e pode sobrescrever o restante do array de destino com valores não especificados.

### Notas

No uso típico, `count` é o número de elementos no array de destino.

Embora o truncamento para caber no buffer de destino seja um risco de segurança e, portanto, uma violação de restrições em tempo de execução para `wcsncpy_s`, é possível obter o comportamento de truncamento especificando `count` igual ao tamanho do array de destino menos um: ele copiará os primeiros `count` caracteres largos e anexará o terminador nulo largo como sempre: wcsncpy_s(dst, sizeof dst / sizeof *dst, src, (sizeof dst / sizeof *dst)-1);

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <wchar.h>
    #include <locale.h>
    
    int main(void)
    {
        const wchar_t src[] = L"わゐ";
        wchar_t dest[6] = {L'あ', L'い', L'う', L'え', L'お'};
    
        wcsncpy(dest, src, 4); // this will copy わゐ and repeat L'\0' two times
    
        puts("The contents of dest are: ");
        setlocale(LC_ALL, "en_US.utf8");
    
        const long dest_size = sizeof dest / sizeof *dest;
        for(wchar_t* p = dest; p-dest != dest_size; ++p) {
            *p ? printf("%lc ", *p)
               : printf("\\0 ");
        }
    }
```

Saída possível:
```
    The contents of dest are: 
    わ ゐ \0 \0 お \0
```

### Referências

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.29.4.2.2 A função wcsncpy (p: 314)

    *   K.3.9.2.1.2 A função wcsncpy_s (p: 464)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.29.4.2.2 A função wcsncpy (p: 431)

    *   K.3.9.2.1.2 A função wcsncpy_s (p: 640-641)

*   Padrão C99 (ISO/IEC 9899:1999):

    *   7.24.4.2.2 A função wcsncpy (p: 377)

### Veja também

[ wcscpywcscpy_s](<#/doc/string/wide/wcscpy>)(C95)(C11) | copia uma string larga para outra
(função)
[ wmemcpywmemcpy_s](<#/doc/string/wide/wmemcpy>)(C95)(C11) | copia uma certa quantidade de caracteres largos entre dois arrays não sobrepostos
(função)
[ strncpystrncpy_s](<#/doc/string/byte/strncpy>)(C11) | copia uma certa quantidade de caracteres de uma string para outra
(função)
[Documentação C++](<#/>) para wcsncpy