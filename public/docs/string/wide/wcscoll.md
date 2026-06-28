# wcscoll

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
int wcscoll( const wchar_t *lhs, const wchar_t *rhs );  // desde C95
```

Compara duas wide strings terminadas em nulo de acordo com a ordem de agrupamento (collation order) definida pela categoria [LC_COLLATE](<#/doc/locale/LC_categories>) da localidade atualmente instalada.

### Parâmetros

- **lhs, rhs** — ponteiros para as wide strings terminadas em nulo a serem comparadas

### Valor de retorno

Valor negativo se `lhs` for _menor que_ (precede) `rhs`.

​0​ se `lhs` for _igual a_ `rhs`.

Valor positivo se `lhs` for _maior que_ (segue) `rhs`.

### Observações

A ordem de agrupamento (collation order) é a ordem de dicionário: a posição da letra no alfabeto nacional (sua _classe de equivalência_) tem prioridade maior do que seu caso ou variante. Dentro de uma classe de equivalência, caracteres minúsculos agrupam antes de seus equivalentes maiúsculos e uma ordem específica da localidade pode ser aplicada aos caracteres com diacríticos. Em algumas localidades, grupos de caracteres são comparados como unidades de agrupamento (collation units) únicas. Por exemplo, "ch" em tcheco segue "h" e precede "i", e "dzs" em húngaro segue "dz" e precede "g".

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <wchar.h>
    #include <locale.h>
     
    void try_compare(const wchar_t* p1, const wchar_t* p2)
    {
        if(wcscoll(p1, p2) < 0)
            printf("%ls before %ls\n", p1, p2);
        else
            printf("%ls before %ls\n", p2, p1);
    }
     
    int main(void)
    {
        setlocale(LC_ALL, "en_US.utf8");
        printf("In the American locale: ");
        try_compare(L"hrnec", L"chrt");
     
        setlocale(LC_COLLATE, "cs_CZ.utf8");
        printf("In the Czech locale: ");
        try_compare(L"hrnec", L"chrt");
     
        setlocale(LC_COLLATE, "en_US.utf8");
        printf("In the American locale: ");
        try_compare(L"år", L"ängel");
     
        setlocale(LC_COLLATE, "sv_SE.utf8");
        printf("In the Swedish locale: ");
        try_compare(L"år", L"ängel");
    }
```

Saída possível:
```
    In the American locale: chrt before hrnec
    In the Czech locale: hrnec before chrt
    In the American locale: ängel before år
    In the Swedish locale: år before ängel
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.29.4.4.2 A função wcscoll (p: 433-434)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.24.4.4.2 A função wcscoll (p: 379-380)

### Veja também

[ strcoll](<#/doc/string/byte/strcoll>) | compara duas strings de acordo com a localidade atual
(função)
[ wcsxfrm](<#/doc/string/wide/wcsxfrm>)(C95) | transforma uma wide string para que wcscmp produza o mesmo resultado que wcscoll
(função)
[ wcscmp](<#/doc/string/wide/wcscmp>)(C95) | compara duas wide strings
(função)
[Documentação C++](<#/>) para wcscoll