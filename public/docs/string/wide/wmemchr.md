# wmemchr

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
wchar_t *wmemchr( const wchar_t *ptr, wchar_t ch, size_t count );  // desde C95
/*QWchar_t*/ *wmemchr( /*Qwchar_t*/ *ptr, wchar_t ch, size_t count );  // desde C23
```

1) Localiza a primeira ocorrência do caractere largo ch nos primeiros count caracteres largos do array de caracteres largos ou array de inteiros de tipo compatível, apontado por ptr.

2) Função genérica por tipo equivalente a (1). Seja `T` um tipo de objeto de caractere largo não qualificado.

    * Se `ptr` for do tipo const T*, o tipo de retorno é const wchar_t*.
    * Caso contrário, se `ptr` for do tipo T*, o tipo de retorno é wchar_t*.
    * Caso contrário, o comportamento é indefinido.

Se uma definição de macro de cada uma dessas funções genéricas for suprimida para acessar uma função real (por exemplo, se (wmemchr) ou um ponteiro de função for usado), a declaração de função real (1) se torna visível.

Se count for zero, a função retorna um ponteiro nulo.

### Parâmetros

- **ptr** — ponteiro para o array de caracteres largos a ser examinado
- **ch** — caractere largo a ser procurado
- **count** — número de caracteres largos a serem examinados

### Valor de retorno

Ponteiro para a localização do caractere largo, ou um ponteiro nulo se nenhum caractere for encontrado.

### Exemplo

Execute este código
```c
    #include <locale.h>
    #include <stdio.h>
    #include <wchar.h>
    
    int main(void)
    {
        wchar_t str[] = L"诺不轻信，故人不负我\0诺不轻许，故我不负人。";
        size_t sz = sizeof str / sizeof *str;
    
        wchar_t target = L'许';
        wchar_t* result = wmemchr(str, target, sz);
    
        if (result)
        {
            setlocale(LC_ALL, "en_US.utf8");
            printf("Found '%lc' at position %td\n",target, result - str);
        }
    }
```

Saída possível:
```
    Found '许' at position 14
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    * 7.29.4.5.8 A função wmemchr (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    * 7.29.4.5.8 A função wmemchr (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    * 7.29.4.5.8 A função wmemchr (p: 438)

  * Padrão C99 (ISO/IEC 9899:1999):

    * 7.24.4.5.8 A função wmemchr (p: 384)

### Veja também

[ memchr](<#/doc/string/byte/memchr>) | procura em um array a primeira ocorrência de um caractere
(função)
[ wcschr](<#/doc/string/wide/wcschr>)(C95) | encontra a primeira ocorrência de um caractere largo em uma string larga
(função)
[Documentação C++](<#/>) para wmemchr