# wmemcmp

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
int wmemcmp( const wchar_t* lhs, const wchar_t* rhs, size_t count );  // desde C95
```

Compara os primeiros `count` caracteres largos (ou tipo inteiro compatível) dos arrays de caracteres largos apontados por `lhs` e `rhs`. A comparação é feita lexicograficamente.

O sinal do resultado é o sinal da diferença entre os valores do primeiro par de caracteres largos que diferem nos arrays sendo comparados.

Se `count` for zero, a função não faz nada.

### Parâmetros

- **lhs, rhs** — ponteiros para os arrays de caracteres largos a serem comparados
- **count** — número de caracteres largos a serem examinados

### Valor de retorno

Valor negativo se o valor do primeiro caractere largo diferente em `lhs` for menor que o valor do caractere largo correspondente em `rhs`: `lhs` precede `rhs` na ordem lexicográfica.

`0` se todos os `count` caracteres largos de `lhs` e `rhs` forem iguais.

Valor positivo se o valor do primeiro caractere largo diferente em `lhs` for maior que o valor do caractere largo correspondente em `rhs`: `rhs` precede `lhs` na ordem lexicográfica.

### Observações

Esta função não é sensível ao locale e não presta atenção aos valores dos objetos `wchar_t` que examina: nulos, assim como caracteres largos inválidos, também são comparados.

### Exemplo

Execute este código
```c
    #include <locale.h>
    #include <stdio.h>
    #include <wchar.h>
    
    void demo(const wchar_t* lhs, const wchar_t* rhs, size_t sz)
    {
        for (size_t n = 0; n < sz; ++n)
            putwchar(lhs[n]);
    
        int rc = wmemcmp(lhs, rhs, sz);
        if (rc == 0)
            wprintf(L" compares equal to ");
        else if(rc < 0)
            wprintf(L" precedes ");
        else if(rc > 0)
            wprintf(L" follows ");
    
        for (size_t n = 0; n < sz; ++n)
            putwchar(rhs[n]);
        wprintf(L" in lexicographical order\n");
    }
    
    int main(void)
    {
        setlocale(LC_ALL, "en_US.utf8");
    
        wchar_t a1[] = {L'α',L'β',L'γ'};
        wchar_t a2[] = {L'α',L'β',L'δ'};
    
        size_t sz = sizeof a1 / sizeof *a1;
        demo(a1, a2, sz);
        demo(a2, a1, sz);
        demo(a1, a1, sz);
    }
```

Saída:
```
    αβγ precedes αβδ in lexicographical order
    αβδ follows αβγ in lexicographical order
    αβγ compares equal to αβγ in lexicographical order
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.29.4.4.5 A função wmemcmp (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.29.4.4.5 A função wmemcmp (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.29.4.4.5 A função wmemcmp (p: 435)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.24.4.4.5 A função wmemcmp (p: 381)

### Veja também

[ wcscmp](<#/doc/string/wide/wcscmp>)(C95) | compara duas strings largas
(função)
[ memcmp](<#/doc/string/byte/memcmp>) | compara dois buffers
(função)
[ wcsncmp](<#/doc/string/wide/wcsncmp>)(C95) | compara uma certa quantidade de caracteres de duas strings largas
(função)
[Documentação C++](<#/>) para wmemcmp