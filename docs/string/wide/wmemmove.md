# wmemmove, wmemmove_s

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
`wchar_t* wmemmove( wchar_t* dest, const wchar_t* src, size_t count );`  // desde C95
`errno_t wmemmove_s( wchar_t *dest, rsize_t destsz, const wchar_t *src, rsize_t count);`  // desde C11
```

1) Copia exatamente `count` caracteres largos sucessivos do array de caracteres largos apontado por `src` para o array de caracteres largos apontado por `dest`. Se `count` for zero, a função não faz nada. Os arrays podem se sobrepor: a cópia ocorre como se os caracteres largos fossem copiados para um array temporário de caracteres largos e depois copiados do array temporário para `dest`.

2) O mesmo que (1), exceto que os seguintes erros são detectados em tempo de execução e chamam a função [constraint handler](<#/doc/error/set_constraint_handler_s>) atualmente instalada:

  * `src` ou `dest` é um ponteiro nulo
  * `destsz` ou `count` é maior que `RSIZE_MAX / sizeof(wchar_t)`
  * `count` é maior que `destsz` (ocorreria um estouro)

Assim como todas as funções com verificação de limites, `wmemcpy_s` tem sua disponibilidade garantida apenas se `__STDC_LIB_EXT1__` for definido pela implementação e se o usuário definir `__STDC_WANT_LIB_EXT1__` para a constante inteira 1 antes de incluir [`<wchar.h>`](<#/doc/string/wide>).

### Parâmetros

- **dest** — ponteiro para o array de caracteres largos para copiar
- **src** — ponteiro para o array de caracteres largos de onde copiar
- **destsz** — número máximo de caracteres largos a serem escritos (o tamanho do buffer de destino)
- **count** — número de caracteres largos a serem copiados

### Valor de retorno

1) Retorna uma cópia de `dest`

2) Retorna zero em caso de sucesso, retorna um valor diferente de zero em caso de erro. Além disso, em caso de erro, preenche todo o `dst` até, mas não incluindo, `dst+dstsz` com caracteres largos nulos, `L'\0'` (a menos que `dest` seja nulo ou `destsz` seja maior que `RSIZE_MAX/sizeof(wchar_t)`)

### Observações

Esta função não é sensível à localidade e não presta atenção aos valores dos objetos `wchar_t` que copia: nulos, bem como caracteres inválidos, também são copiados.

### Exemplo

Execute este código
```c
    #include <locale.h>
    #include <stdio.h>
    #include <wchar.h>
    
    int main(void)
    {
        setlocale(LC_ALL, "en_US.utf8");
    
        wchar_t str[] = L"αβγδεζηθικλμνξοπρστυφχψω";
        printf("%ls\n", str);
        wmemmove(str + 4, str + 3, 3); // copy from [δεζ] to [εζη]
        printf("%ls\n", str);
    }
```

Saída:
```
    αβγδεζηθικλμνξοπρστυφχψω
    αβγδδεζθικλμνξοπρστυφχψω
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    * 7.29.4.2.4 A função wmemmove (p: TBD)

    * K.3.9.2.1.4 A função wmemmove_s (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    * 7.29.4.2.4 A função wmemmove (p: TBD)

    * K.3.9.2.1.4 A função wmemmove_s (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    * 7.29.4.2.4 A função wmemmove (p: 432)

    * K.3.9.2.1.4 A função wmemmove_s (p: 642)

  * Padrão C99 (ISO/IEC 9899:1999):

    * 7.24.4.2.4 A função wmemmove (p: 378)

### Veja também

[ memmovememmove_s](<#/doc/string/byte/memmove>)(C11) | move um buffer para outro
(função)
[ wmemcpywmemcpy_s](<#/doc/string/wide/wmemcpy>)(C95)(C11) | copia uma certa quantidade de caracteres largos entre dois arrays não sobrepostos
(função)
[Documentação C++](<#/>) para wmemmove