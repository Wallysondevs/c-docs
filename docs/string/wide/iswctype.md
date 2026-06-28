# iswctype

Definido no cabeçalho [`<wctype.h>`](<#/doc/string/wide>)

```c
int iswctype( wint_t wc, wctype_t desc );  // desde C95
```

Classifica o caractere largo wc usando a categoria [LC_CTYPE](<#/doc/locale/LC_categories>) da localidade C atual, identificada por desc.

### Parâmetros

- **wc** — o caractere largo a ser classificado
- **desc** — a categoria [LC_CTYPE](<#/doc/locale/LC_categories>), obtida de uma chamada para [wctype](<#/doc/string/wide/wctype>)

### Valor de retorno

Diferente de zero se o caractere wc tiver a propriedade identificada por desc na faceta [LC_CTYPE](<#/doc/locale/LC_categories>) da localidade C atual, zero caso contrário.

### Exemplo

Execute este código
```c
    #include <locale.h>
    #include <stdio.h>
    #include <wchar.h>
    #include <wctype.h>
    
    const char* classify(wchar_t wc, const char* cat)
    {
        return iswctype(wc, wctype(cat)) ? "true" : "false";
    }
    
    int main(void)
    {
        setlocale(LC_ALL, "ja_JP.UTF-8");
        puts("The character \u6c34 is...");
        const char* cats[] = {"digit", "alpha", "space", "cntrl", "jkanji"};
        for (int n = 0; n < 5; ++n)
            printf("%s?\t%s\n", cats[n], classify(L'\u6c34', cats[n]));
    }
```

Saída:
```
    The character 水 is...
    digit?  false
    alpha?  true
    space?  false
    cntrl?  false
    jkanji? true
```

### Referências

* Padrão C23 (ISO/IEC 9899:2024):

  * 7.30.2.2.1 A função iswctype (p: TBD)

* Padrão C17 (ISO/IEC 9899:2018):

  * 7.30.2.2.1 A função iswctype (p: TBD)

* Padrão C11 (ISO/IEC 9899:2011):

  * 7.30.2.2.1 A função iswctype (p: 451-452)

* Padrão C99 (ISO/IEC 9899:1999):

  * 7.25.2.2.1 A função iswctype (p: 397-398)

### Veja também

[ wctype](<#/doc/string/wide/wctype>)(C95) | procura uma categoria de classificação de caractere na localidade C atual
(função)