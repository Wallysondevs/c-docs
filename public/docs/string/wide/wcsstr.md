# wcsstr

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
wchar_t *wcsstr( const wchar_t *dest, const wchar_t *src );  // desde C95
/*QWchar_t*/ *wcsstr( /*QWchar_t*/ *dest, const wchar_t *src );  // desde C23
```

1) Encontra a primeira ocorrência da string larga `src` na string larga apontada por `dest`. Os caracteres nulos terminadores não são comparados.

2) Função genérica por tipo equivalente a (1). Seja `T` um tipo de objeto de caractere largo não qualificado.

  * Se `dest` for do tipo const T*, o tipo de retorno é const wchar_t*.
  * Caso contrário, se `dest` for do tipo T*, o tipo de retorno é wchar_t*.
  * Caso contrário, o comportamento é indefinido.

Se uma definição de macro de cada uma dessas funções genéricas for suprimida para acessar uma função real (por exemplo, se (wcsstr) ou um ponteiro de função for usado), a declaração de função real (1) se torna visível.

### Parâmetros

- **dest** — ponteiro para a string larga terminada em nulo a ser examinada
- **src** — ponteiro para a string larga terminada em nulo a ser procurada

### Valor de retorno

Ponteiro para o primeiro caractere da subcadeia encontrada em `dest`, ou um ponteiro nulo se nenhuma subcadeia for encontrada. Se `src` apontar para uma string vazia, `dest` é retornado.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <locale.h>
    #include <wchar.h>
     
    int main(void)
    {
        setlocale(LC_ALL, "ru_RU.UTF-8");
     
        wchar_t str[5][64] = {
            L"Строка, где есть подстрока 'но'.",
            L"Строка, где такой подстроки нет.",
            L"Он здесь.",
            L"Здесь он.",
            L"Его нет."
        };
     
        for (size_t i = 0; i < 5; ++i) {
            if (wcsstr(str[i], L"но")) {
                wprintf(L"%ls\n", str[i]);
            }
        }
    }
```

Saída:
```
    Строка, где есть подстрока 'но'.
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.29.4.5.6 A função wcsstr (p: 437)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.24.4.5.6 A função wcsstr (p: 383)

### Veja também

[ wcschr](<#/doc/string/wide/wcschr>)(C95) | encontra a primeira ocorrência de um caractere largo em uma string larga
(função)
[ wcsrchr](<#/doc/string/wide/wcsrchr>)(C95) | encontra a última ocorrência de um caractere largo em uma string larga
(função)
[Documentação C++](<#/>) para wcsstr