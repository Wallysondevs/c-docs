# wcschr

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
wchar_t *wcschr( const wchar_t *str, wchar_t ch );  // desde C95
/*QWchar_t*/ *wcschr( /*QWchar_t*/ *str, wchar_t ch );  // desde C23
```

1) Encontra a primeira ocorrência do caractere largo `ch` na string larga apontada por `str`.

2) Função genérica de tipo equivalente a (1). Seja `T` um tipo de objeto de caractere largo não qualificado.

    * Se `str` for do tipo const T*, o tipo de retorno é const wchar_t*.
    * Caso contrário, se `str` for do tipo T*, o tipo de retorno é wchar_t*.
    * Caso contrário, o comportamento é indefinido.

Se uma definição de macro de cada uma dessas funções genéricas for suprimida para acessar uma função real (por exemplo, se (wcschr) ou um ponteiro de função for usado), a declaração de função real (1) se torna visível.

### Parâmetros

- **str** — ponteiro para a string larga terminada em nulo a ser analisada
- **ch** — caractere largo a ser procurado

### Valor de retorno

Ponteiro para o caractere encontrado em `str`, ou um ponteiro nulo se nenhum caractere for encontrado.

### Exemplo

Execute este código
```c
    #include <wchar.h>
    #include <stdio.h>
    #include <locale.h>
     
    int main(void)
    {
        wchar_t arr[] = L"白猫 黒猫 кошки";
        wchar_t *cat = wcschr(arr, L'猫');
        wchar_t *dog = wcschr(arr, L'犬');
     
        setlocale(LC_ALL, "en_US.utf8");
        if(cat)
            printf("The character 猫 found at position %td\n", cat-arr);
        else
            puts("The character 猫 not found");
     
        if(dog)
            printf("The character 犬 found at position %td\n", dog-arr);
        else
            puts("The character 犬 not found");
    }
```

Saída:
```
    The character 猫 found at position 1
    The character 犬 not found
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    * 7.29.4.5.1 A função wcschr (p: 435)

  * Padrão C99 (ISO/IEC 9899:1999):

    * 7.24.4.5.1 A função wcschr (p: 381)

### Veja também

[ wcsrchr](<#/doc/string/wide/wcsrchr>)(C95) | encontra a última ocorrência de um caractere largo em uma string larga
(função)
[ wcspbrk](<#/doc/string/wide/wcspbrk>)(C95) | encontra a primeira localização de qualquer caractere largo em uma string larga, em outra string larga
(função)
[Documentação C++](<#/>) para wcschr