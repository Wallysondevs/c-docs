# strcoll

Definido no cabeçalho [`<string.h>`](<#/doc/string/byte>)

```c
int strcoll( const char* lhs, const char* rhs );
```

Compara duas strings de bytes terminadas em nulo de acordo com a localidade atual, conforme definido pela categoria [LC_COLLATE](<#/doc/locale/LC_categories>).

### Parâmetros

- **lhs, rhs** — ponteiros para as strings de bytes terminadas em nulo a serem comparadas

### Valor de retorno

*   Valor negativo se lhs for _menor que_ (precede) rhs.
*   ​0​ se lhs for _igual a_ rhs.
*   Valor positivo se lhs for _maior que_ (segue) rhs.

### Notas

A ordem de agrupamento é a ordem do dicionário: a posição da letra no alfabeto nacional (sua _classe de equivalência_) tem prioridade maior do que sua caixa ou variante. Dentro de uma classe de equivalência, caracteres minúsculos agrupam-se antes de seus equivalentes maiúsculos e uma ordem específica da localidade pode ser aplicada a caracteres com diacríticos. Em algumas localidades, grupos de caracteres são comparados como unidades de agrupamento únicas. Por exemplo, "ch" em tcheco segue "h" e precede "i", e "dzs" em húngaro segue "dz" e precede "g".

### Exemplo

Execute este código
```c
    #include <locale.h>
    #include <stdio.h>
    #include <string.h>
    
    int main(void)
    {
        setlocale(LC_COLLATE, "cs_CZ.utf8");
        // Alternatively, ISO-8859-2 (a.k.a. Latin-2)
        // may also work on some OS:
        // setlocale(LC_COLLATE, "cs_CZ.iso88592");
    
        const char* s1 = "hrnec";
        const char* s2 = "chrt";
    
        printf("In the Czech locale: ");
        if (strcoll(s1, s2) < 0)
            printf("%s before %s\n", s1, s2);
        else
            printf("%s before %s\n", s2, s1);
    
        printf("In lexicographical comparison: ");
        if (strcmp(s1, s2) < 0)
            printf("%s before %s\n", s1, s2);
        else
            printf("%s before %s\n", s2, s1);
    }
```

Saída:
```
    In the Czech locale: hrnec before chrt
    In lexicographical comparison: chrt before hrnec
```

### Referências

*   Padrão C23 (ISO/IEC 9899:2024):

    *   7.24.4.3 A função strcoll (p: TBD)
*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.24.4.3 A função strcoll (p: TBD)
*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.24.4.3 A função strcoll (p: 366)
*   Padrão C99 (ISO/IEC 9899:1999):

    *   7.21.4.3 A função strcoll (p: 329)
*   Padrão C89/C90 (ISO/IEC 9899:1990):

    *   4.11.4.3 A função strcoll

### Veja também

[wcscoll](<#/doc/string/wide/wcscoll>)(C95) | compara duas wide strings de acordo com a localidade atual
(função)
[strxfrm](<#/doc/string/byte/strxfrm>) | transforma uma string para que strcmp produza o mesmo resultado que strcoll
(função)
[wcsxfrm](<#/doc/string/wide/wcsxfrm>)(C95) | transforma uma wide string para que wcscmp produza o mesmo resultado que wcscoll
(função)
[strcmp](<#/doc/string/byte/strcmp>) | compara duas strings
(função)
[Documentação C++](<#/>) para strcoll