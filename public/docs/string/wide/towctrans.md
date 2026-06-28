# towctrans

Definido no cabeçalho [`<wctype.h>`](<#/doc/string/wide>)

```c
wint_t towctrans( wint_t wc, wctrans_t desc );  // desde C95
```

  
Mapeia o caractere largo wc usando a categoria de mapeamento [LC_CTYPE](<#/doc/locale/LC_categories>) do locale C atual, identificada por desc. 

### Parâmetros

wc  |  \-  |  o caractere largo a ser mapeado   
desc  |  \-  |  o mapeamento [LC_CTYPE](<#/doc/locale/LC_categories>), obtido de uma chamada para [wctrans](<#/doc/string/wide/wctrans>)  
  
### Valor de retorno

O valor mapeado de wc usando o mapeamento identificado por desc na faceta [LC_CTYPE](<#/doc/locale/LC_categories>) do locale C atual. 

### Exemplo

Execute este código
```c
    #include <locale.h>
    #include <wctype.h>
    #include <wchar.h>
    #include <stdio.h>
     
    int main(void)
    {
        setlocale(LC_ALL, "ja_JP.UTF-8");
        const wchar_t kana[] = L"ヒラガナ";
        size_t sz = sizeof kana / sizeof *kana;
        wchar_t hira[sz];
        for (size_t n = 0; n < sz; ++n)
            hira[n] = towctrans(kana[n], wctrans("tojhira"));
        printf("katakana characters %ls are %ls in hiragana\n", kana, hira);
    }
```

Saída: 
```
    katakana characters ヒラガナ are ひらがな in hiragana
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.30.3.2.1 A função towctrans (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.30.3.2.1 A função towctrans (p: TBD) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.30.3.2.1 A função towctrans (p: 454) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.25.3.2,1 A função towctrans (p: 400) 

### Veja também

[ wctrans](<#/doc/string/wide/wctrans>)(C95) |  procura uma categoria de mapeamento de caracteres no locale C atual   
(função)  
[Documentação C++](<#/>) para towctrans