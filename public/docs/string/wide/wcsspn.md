# wcsspn

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
size_t wcsspn( const wchar_t* dest, const wchar_t* src );  // desde C95
```

Retorna o comprimento do segmento inicial máximo da wide string apontada por `dest`, que consiste apenas nos caracteres encontrados na wide string apontada por `src`.

### Parâmetros

- **dest** — ponteiro para a wide string terminada em nulo a ser analisada
- **src** — ponteiro para a wide string terminada em nulo que contém os caracteres a serem procurados

### Valor de retorno

O comprimento do segmento inicial máximo que contém apenas caracteres da wide string apontada por `src`

### Exemplo

Execute este código
```c
    #include <locale.h>
    #include <wchar.h>
     
    int main(void)
    {
        wchar_t dest[] = L"白猫 黑狗 甲虫";
        const wchar_t src[] = L" 狗猫 白黑 ";
        const size_t len = wcsspn(dest, src);
        dest[len] = L'\0'; /* terminates the segment to print it out */
     
        setlocale(LC_ALL, "en_US.utf8");
        wprintf(L"The length of maximum initial segment is %td.\n"
                L"The segment is \"%ls\".\n", len, dest);
    }
```

Saída:
```
    The length of maximum initial segment is 6.
    The segment is "白猫 黑狗 ".
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.29.4.5.5 A função wcsspn (p: 436)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.24.4.5.5 A função wcsspn (p: 382)

### Veja também

[ wcscspn](<#/doc/string/wide/wcscspn>)(C95) | retorna o comprimento do segmento inicial máximo que consiste
apenas nos wide chars _não_ encontrados em outra wide string
(função)
[ wcspbrk](<#/doc/string/wide/wcspbrk>)(C95) | encontra a primeira ocorrência de qualquer wide character em uma wide string, em outra wide string
(função)
[Documentação C++](<#/>) para wcsspn