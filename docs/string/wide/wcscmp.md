# wcscmp

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
int wcscmp( const wchar_t* lhs, const wchar_t* rhs );  // desde C95
```

Compara duas wide strings terminadas em nulo lexicograficamente.

O sinal do resultado é o sinal da diferença entre os valores do primeiro par de wide characters que diferem nas strings sendo comparadas.

O comportamento é indefinido se lhs ou rhs não forem ponteiros para wide strings terminadas em nulo.

### Parâmetros

- **lhs, rhs** — ponteiros para as wide strings terminadas em nulo a serem comparadas

### Valor de retorno

Valor negativo se lhs aparecer antes de rhs na ordem lexicográfica.

Zero se lhs e rhs forem iguais.

Valor positivo se lhs aparecer depois de rhs na ordem lexicográfica.

### Notas

Esta função não é sensível à localidade, ao contrário de [wcscoll](<#/doc/string/wide/wcscoll>), e a ordem pode não ser significativa quando caracteres de diferentes blocos Unicode são usados juntos ou quando a ordem das unidades de código não corresponde a nenhuma ordem de agrupamento.

### Exemplo

Execute este código
```c
    #include <locale.h>
    #include <stdio.h>
    #include <wchar.h>
    
    void demo(const wchar_t* lhs, const wchar_t* rhs)
    {
        int rc = wcscmp(lhs, rhs);
        const char *rel = rc < 0 ? "precedes" : rc > 0 ? "follows" : "equals";
    
        setlocale(LC_ALL, "en_US.utf8");
        printf("[%ls] %s [%ls]\n", lhs, rel, rhs);
    }
    
    int main(void)
    {
        const wchar_t* string = L"どうもありがとうございます";
        demo(string, L"どうも");
        demo(string, L"助かった");
        demo(string + 9, L"ありがとうございます" + 6);
    }
```

Saída possível:
```
    [どうもありがとうございます] follows [どうも]
    [どうもありがとうございます] precedes [助かった]
    [ざいます] equals [ざいます]
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.29.4.4.1 A função wcscmp (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.29.4.4.1 A função wcscmp (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.29.4.4.1 A função wcscmp (p: 433)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.24.4.4.1 A função wcscmp (p: 379)

### Veja também

[ wcsncmp](<#/doc/string/wide/wcsncmp>)(C95) | compara uma certa quantidade de caracteres de duas wide strings
(função)
[ wmemcmp](<#/doc/string/wide/wmemcmp>)(C95) | compara uma certa quantidade de wide characters de dois arrays
(função)
[ strcmp](<#/doc/string/byte/strcmp>) | compara duas strings
(função)
[ wcscoll](<#/doc/string/wide/wcscoll>)(C95) | compara duas wide strings de acordo com a localidade atual
(função)
[Documentação C++](<#/>) para wcscmp