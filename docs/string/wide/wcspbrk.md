# wcspbrk

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
wchar_t *wcspbrk( const wchar_t *dest, const wchar_t *str );  // desde C95
/*QWchar_t*/ *wcspbrk( /*QWchar_t*/ *dest, const wchar_t *str );  // desde C23
```

1) Encontra o primeiro caractere na string larga apontada por `dest` que também está na string larga apontada por `str`.

2) Função genérica de tipo equivalente a (1). Seja `T` um tipo de objeto de caractere largo não qualificado.

    * Se `dest` for do tipo const T*, o tipo de retorno é const wchar_t*.
    * Caso contrário, se `dest` for do tipo T*, o tipo de retorno é wchar_t*.
    * Caso contrário, o comportamento é indefinido.

Se uma definição de macro de cada uma dessas funções genéricas for suprimida para acessar uma função real (por exemplo, se (wcspbrk) ou um ponteiro de função for usado), a declaração de função real (1) se torna visível.

### Parâmetros

- **dest** — ponteiro para a string larga terminada em nulo a ser analisada
- **str** — ponteiro para a string larga terminada em nulo que contém os caracteres a serem procurados

### Valor de retorno

Ponteiro para o primeiro caractere em `dest` que também está em `str`, ou um ponteiro nulo se nenhum caractere desse tipo existir.

### Observações

O nome significa "wide character string pointer break" (quebra de ponteiro de string de caractere largo), porque ele retorna um ponteiro para o primeiro dos caracteres separadores ("break").

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <wchar.h>
    
    int main(void)
    {
        const wchar_t* str = L"Hello world, friend of mine!";
        const wchar_t* sep = L" ,!";
    
        unsigned int cnt = 0;
        do {
           str = wcspbrk(str, sep); // encontra o separador
           if (str) str += wcsspn(str, sep); // pula o separador
           ++cnt; // incrementa a contagem de palavras
        } while (str && *str);
    
        wprintf(L"There are %u words.\n", cnt);
    }
```

Saída:
```
    There are 5 words.
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    * 7.29.4.5.3 A função wcspbrk (p: 436)

  * Padrão C99 (ISO/IEC 9899:1999):

    * 7.24.4.5.3 A função wcspbrk (p: 382)

### Veja também

[ wcscspn](<#/doc/string/wide/wcscspn>)(C95) | retorna o comprimento do segmento inicial máximo que consiste
apenas nos caracteres largos _não_ encontrados em outra string larga
(função)
[ wcschr](<#/doc/string/wide/wcschr>)(C95) | encontra a primeira ocorrência de um caractere largo em uma string larga
(função)
[ strpbrk](<#/doc/string/byte/strpbrk>) | encontra a primeira ocorrência de qualquer caractere de uma string em outra string
(função)
[Documentação C++](<#/>) para wcspbrk