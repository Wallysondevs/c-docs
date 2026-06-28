# wctype

Definido no cabeçalho [`<wctype.h>`](<#/doc/string/wide>)

```c
wctype_t wctype( const char* str );  // desde C95
```

Constrói um valor do tipo wctype_t que descreve uma categoria [LC_CTYPE](<#/doc/locale/LC_categories>) de classificação de caracteres largos. Pode ser uma das categorias de classificação padrão, ou uma categoria específica da localidade, como `"jkanji"`.

### Parâmetros

- **str** — String C contendo o nome da categoria desejada

Os seguintes valores de `str` são suportados em todas as localidades C:

valor de `str` | efeito
`"alnum"` | identifica a categoria usada por [iswalnum](<#/doc/string/wide/iswalnum>)
`"alpha"` | identifica a categoria usada por [iswalpha](<#/doc/string/wide/iswalpha>)
`"blank"` | identifica a categoria usada por [iswblank](<#/doc/string/wide/iswblank>) (C99)
`"cntrl"` | identifica a categoria usada por [iswcntrl](<#/doc/string/wide/iswcntrl>)
`"digit"` | identifica a categoria usada por [iswdigit](<#/doc/string/wide/iswdigit>)
`"graph"` | identifica a categoria usada por [iswgraph](<#/doc/string/wide/iswgraph>)
`"lower"` | identifica a categoria usada por [iswlower](<#/doc/string/wide/iswlower>)
`"print"` | identifica a categoria usada por [iswprint](<#/doc/string/wide/iswprint>)
`"space"` | identifica a categoria usada por [iswspace](<#/doc/string/wide/iswspace>)
`"upper"` | identifica a categoria usada por [iswupper](<#/doc/string/wide/iswupper>)
`"xdigit"` | identifica a categoria usada por [iswxdigit](<#/doc/string/wide/iswxdigit>)

### Valor de retorno

Objeto wctype_t adequado para uso com [iswctype](<#/doc/string/wide/iswctype>) para classificar caracteres largos de acordo com a categoria nomeada da localidade C atual ou zero se str não nomear uma categoria suportada pela localidade C atual.

### Referências

*   Padrão C23 (ISO/IEC 9899:2024):

    *   7.30.2.2.2 A função wctype (p: TBD)
*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.30.2.2.2 A função wctype (p: TBD)
*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.30.2.2.2 A função wctype (p: 452)
*   Padrão C99 (ISO/IEC 9899:1999):

    *   7.25.2.2.2 A função wctype (p: 398)

### Veja também

[ iswctype](<#/doc/string/wide/iswctype>)(C95) | classifica um caractere largo de acordo com a categoria [LC_CTYPE](<#/doc/locale/LC_categories>) especificada
(função)
[Documentação C++](<#/>) para wctype