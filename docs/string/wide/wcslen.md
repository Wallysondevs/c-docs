# wcslen, wcsnlen_s

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
size_t wcslen( const wchar_t *str );  // desde C95
size_t wcsnlen_s(const wchar_t *str, size_t strsz);  // desde C11
```

1) Retorna o comprimento de uma string larga (wide string), ou seja, o número de caracteres largos não nulos que precedem o caractere largo nulo terminador.

2) O mesmo que (1), exceto que a função retorna zero se `str` for um ponteiro nulo e retorna `strsz` se o caractere largo nulo não for encontrado nos primeiros `strsz` caracteres largos de `src`.

    Assim como todas as funções com verificação de limites (bounds-checked functions), `wcslen_s` tem sua disponibilidade garantida apenas se `__STDC_LIB_EXT1__` for definido pela implementação e se o usuário definir `__STDC_WANT_LIB_EXT1__` para a constante inteira 1 antes de incluir `[`<stdio.h>`](<#/doc/io>)`.

### Parâmetros

- **str** — ponteiro para a string larga terminada em nulo a ser examinada
- **strsz** — número máximo de caracteres largos a serem examinados

### Valor de retorno

1) O comprimento da string larga terminada em nulo `str`.

2) O comprimento da string larga terminada em nulo `str` em caso de sucesso, zero se `str` for um ponteiro nulo, `strsz` se o caractere largo nulo não for encontrado.

### Observações

`strnlen_s` e `wcsnlen_s` são as únicas [funções com verificação de limites](<#/doc/error>) que não invocam o manipulador de restrições de tempo de execução. Elas são funções de utilidade pura usadas para fornecer suporte limitado para strings não terminadas em nulo.

### Exemplo

Execute este código
```c
    #include <wchar.h>
    #include <stdio.h>
    
    int main(void)
    {
        wchar_t str[] = L"How many wide characters does this string contain?";
    
        printf("without null character: %zu\n", wcslen(str));
        printf("with null character: %zu\n", sizeof str / sizeof *str);
    }
```

Saída:
```
    without null character: 50
    with null character: 51
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.29.4.6.1 A função wcslen (p: 439)

    

  * K.3.9.2.4.1 A função wcsnlen_s (p: 646-647)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.24.4.6.1 A função wcslen (p: 385)

### Veja também

[ strlenstrnlen_s](<#/doc/string/byte/strlen>)(C11) | retorna o comprimento de uma dada string
(função)
[Documentação C++](<#/>) para wcslen