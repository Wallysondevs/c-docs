# wmemcpy, wmemcpy_s

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
wchar_t* wmemcpy( wchar_t* dest, const wchar_t* src, size_t count );  // desde C95
(ate C99)  // ate C99
wchar_t *wmemcpy(wchar_t *restrict dest, const wchar_t *restrict src,
size_t count );  // desde C99
errno_t wmemcpy_s( wchar_t *restrict dest, rsize_t destsz,
const wchar_t *restrict src, rsize_t count );  // desde C11
```

1) Copia exatamente `count` caracteres largos sucessivos do array de caracteres largos apontado por `src` para o array de caracteres largos apontado por `dest`. Se os objetos se sobrepuserem, o comportamento é indefinido. Se `count` for zero, a função não faz nada.

2) O mesmo que (1), exceto que os seguintes erros são detectados em tempo de execução e chamam a função [constraint handler](<#/doc/error/set_constraint_handler_s>) atualmente instalada:

  * `src` ou `dest` é um ponteiro nulo
  * `destsz` ou `count` é maior que RSIZE_MAX/sizeof(wchar_t)
  * `count` é maior que `destsz` (ocorreria um estouro)
  * ocorreria sobreposição entre os arrays de origem e destino

Assim como todas as funções com verificação de limites, `wmemcpy_s` é garantida como disponível apenas se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir [`<wchar.h>`](<#/doc/string/wide>).

### Parâmetros

- **dest** — ponteiro para o array de caracteres largos para o qual copiar
- **src** — ponteiro para o array de caracteres largos do qual copiar
- **count** — número de caracteres largos a copiar
- **destsz** — número máximo de caracteres largos a escrever (o tamanho do buffer de destino)

### Valor de retorno

1) retorna uma cópia de `dest`

2) retorna zero em caso de sucesso, retorna um valor diferente de zero em caso de erro. Além disso, em caso de erro, preenche todo o `dst` até, mas não incluindo, dst+dstsz com caracteres largos nulos, L'\0' (a menos que `dest` seja nulo ou `destsz` seja maior que RSIZE_MAX/sizeof(wchar_t))

### Observações

O análogo desta função para strings de byte é [strncpy](<#/doc/string/byte/strncpy>), não [strcpy](<#/doc/string/byte/strcpy>).

Esta função não é sensível à localidade e não presta atenção aos valores dos objetos wchar_t que copia: nulos, assim como caracteres inválidos, também são copiados.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <wchar.h>
    #include <locale.h>
    
    int main(void)
    {
        wchar_t from1[] = L"नमस्ते";
        size_t sz1 = sizeof from1 / sizeof *from1;
        wchar_t from2[] = L"Բարև";
        size_t sz2 = sizeof from2 / sizeof *from2;
        wchar_t to[sz1 + sz2];
        wmemcpy(to, from1, sz1); // copia from1, juntamente com seu terminador nulo
        wmemcpy(to + sz1, from2, sz2); // anexa from2, juntamente com seu terminador nulo
    
        setlocale(LC_ALL, "en_US.utf8");
        printf("Wide array contains: ");
        for(size_t n = 0; n < sizeof to / sizeof *to; ++n)
            if(to[n])
                printf("%lc", to[n]);
            else
                printf("\\0");
        printf("\n");
    }
```

Saída possível:
```
    Wide array contains: नमस्ते\0Բարև\0
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    * 7.29.4.2.3 A função wmemcpy (p: 431)

    * K.3.9.2.1.3 A função wmemcpy_s (p: 641)

  * Padrão C99 (ISO/IEC 9899:1999):

    * 7.24.4.2.3 A função wmemcpy (p: 377)

### Veja também

[ wmemmovewmemmove_s](<#/doc/string/wide/wmemmove>)(C95)(C11) | copia uma certa quantidade de caracteres largos entre dois arrays, possivelmente sobrepostos
(função)
[ strncpystrncpy_s](<#/doc/string/byte/strncpy>)(C11) | copia uma certa quantidade de caracteres de uma string para outra
(função)
[Documentação C++](<#/>) para wmemcpy