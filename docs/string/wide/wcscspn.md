# wcscspn

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
size_t wcscspn( const wchar_t* dest, const wchar_t* src );  // desde C95
```

Retorna o comprimento do segmento inicial máximo da string larga apontada por `dest`, que consiste apenas nos caracteres _não_ encontrados na string larga apontada por `src`.

### Parâmetros

- **dest** — ponteiro para a string larga terminada em nulo a ser analisada
- **src** — ponteiro para a string larga terminada em nulo que contém os caracteres a serem procurados

### Valor de retorno

O comprimento do segmento inicial máximo que contém apenas caracteres não encontrados na string de caracteres apontada por `src`

### Exemplo

Execute este código
```c
    #include <locale.h>
    #include <wchar.h>
    
    int main(void)
    {
        wchar_t dest[] = L"白猫 黑狗 甲虫";
        /*                      └───┐   */
        const wchar_t *src = L"甲虫,黑狗";
    
        const size_t len = wcscspn(dest, src);
        dest[len] = L'\0'; /* terminates the segment to print it out */
    
        setlocale(LC_ALL, "en_US.utf8");
        wprintf(L"The length of maximum initial segment is %td.\n"
                L"The segment is \"%ls\".\n", len, dest);
    }
```

Saída:
```
    The length of maximum initial segment is 3.
    The segment is "白猫 ".
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.29.4.5.2 A função wcscspn (p: 435-436)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.24.4.5.2 A função wcscspn (p: 381-382)

### Veja também

[ wcsspn](<#/doc/string/wide/wcsspn>)(C95) | retorna o comprimento do segmento inicial máximo que consiste apenas nos caracteres largos encontrados em outra string larga (função)
[ wcspbrk](<#/doc/string/wide/wcspbrk>)(C95) | encontra a primeira ocorrência de qualquer caractere largo de uma string larga em outra string larga (função)
[Documentação C++](<#/>) para wcscspn