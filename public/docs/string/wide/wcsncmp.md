# wcsncmp

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
int wcsncmp( const wchar_t* lhs, const wchar_t* rhs, size_t count );  // desde C95
```

Compara no máximo `count` caracteres largos de duas strings largas terminadas em nulo. A comparação é feita lexicograficamente.

O sinal do resultado é o sinal da diferença entre os valores do primeiro par de caracteres largos que diferem nas strings sendo comparadas.

O comportamento é indefinido se `lhs` ou `rhs` não forem ponteiros para strings terminadas em nulo.

### Parâmetros

- **lhs, rhs** — ponteiros para as strings largas terminadas em nulo a serem comparadas
- **count** — número máximo de caracteres a serem comparados

### Valor de retorno

Valor negativo se `lhs` aparecer antes de `rhs` na ordem lexicográfica.

Zero se `lhs` e `rhs` forem iguais na comparação.

Valor positivo se `lhs` aparecer depois de `rhs` na ordem lexicográfica.

### Notas

Esta função não é sensível ao locale, ao contrário de [wcscoll](<#/doc/string/wide/wcscoll>) e [wcsxfrm](<#/doc/string/wide/wcsxfrm>).

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <wchar.h>
    #include <locale.h>
    
    void demo(const wchar_t *lhs, const wchar_t *rhs, int sz)
    {
        int rc = wcsncmp(lhs, rhs, sz);
        if(rc == 0)
            printf("First %d characters of [%ls] equal [%ls]\n", sz, lhs, rhs);
        else if(rc < 0)
            printf("First %d characters of [%ls] precede [%ls]\n", sz, lhs, rhs);
        else if(rc > 0)
            printf("First %d characters of [%ls] follow [%ls]\n", sz, lhs, rhs);
    }
    
    int main(void)
    {
        const wchar_t *str1 = L"안녕하세요";
        const wchar_t *str2 = L"안녕히 가십시오";
    
        setlocale(LC_ALL, "en_US.utf8");
        demo(str1, str2, 5);
        demo(str2, str1, 8);
        demo(str1, str2, 2);
    }
```

Saída:
```
    First 5 characters of [안녕하세요] precede [안녕히 가십시오]
    First 8 characters of [안녕히 가십시오] follow [안녕하세요]
    First 2 characters of [안녕하세요] equal [안녕히 가십시오]
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.29.4.4.3 A função wcsncmp (p: 434)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.24.4.4.3 A função wcsncmp (p: 380)

### Veja também

[ wcscmp](<#/doc/string/wide/wcscmp>)(C95) | compara duas strings largas
(função)
[ wmemcmp](<#/doc/string/wide/wmemcmp>)(C95) | compara uma certa quantidade de caracteres largos de dois arrays
(função)
[ wcscoll](<#/doc/string/wide/wcscoll>)(C95) | compara duas strings largas de acordo com o locale atual
(função)
[Documentação C++](<#/>) para wcsncmp