# wctrans

Definido no cabeçalho [`<wctype.h>`](<#/doc/string/wide>)

```c
wctrans_t wctrans( const char* str );  // desde C95
```

Constrói um valor do tipo wctrans_t que descreve uma categoria [LC_CTYPE](<#/doc/locale/LC_categories>) de mapeamento de caracteres largos. Pode ser um dos mapeamentos padrão, ou um mapeamento específico da localidade (locale-specific), como `"tojhira"` ou `"tojkata"`.

### Parâmetros

- **str** — String C contendo o nome do mapeamento desejado. Os seguintes valores de str são suportados em todas as localidades C (C locales): | Valor de `str` | Efeito
`"toupper"` | identifica o mapeamento usado por [towupper](<#/doc/string/wide/towupper>)
`"tolower"` | identifica o mapeamento usado por [towlower](<#/doc/string/wide/towlower>)

### Valor de retorno

Objeto wctrans_t adequado para uso com [towctrans](<#/doc/string/wide/towctrans>) para mapear caracteres largos de acordo com o mapeamento nomeado da localidade C (C locale) atual ou zero se str não nomear um mapeamento suportado pela localidade C (C locale) atual.

### Referências

*   Padrão C23 (ISO/IEC 9899:2024):

    *   7.30.3.2.2 A função wctrans (p: TBD)

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.30.3.2.2 A função wctrans (p: TBD)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.30.3.2.2 A função wctrans (p: 454)

*   Padrão C99 (ISO/IEC 9899:1999):

    *   7.25.3.2,2 A função wctrans (p: 400)

### Veja também

[ towctrans](<#/doc/string/wide/towctrans>)(C95) | realiza o mapeamento de caracteres de acordo com a categoria de mapeamento LC_CTYPE especificada
(função)
[Documentação C++](<#/>) para wctrans