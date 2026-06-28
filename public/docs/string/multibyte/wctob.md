# wctob

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
int wctob( wint_t c );  // desde C95
```

Restringe um caractere largo `c` se seu equivalente de caractere multibyte no estado de mudança inicial for um único byte.

Isso é tipicamente possível para os caracteres do conjunto de caracteres ASCII, já que a maioria das codificações multibyte (como UTF-8) usa bytes únicos para codificar esses caracteres.

### Parâmetros

- **c** — caractere largo a ser restringido

### Valor de retorno

[EOF](<#/doc/io>) se `c` não representar um caractere multibyte com comprimento 1 no estado de mudança inicial.

caso contrário, a representação de byte único de `c` como unsigned char convertido para int

### Exemplo

Execute este código
```c
    #include <locale.h>
    #include <wchar.h>
    #include <stdio.h>
    #include <assert.h>
    
    void try_narrowing(wchar_t c)
    {
        int cn = wctob(c);
        if(cn != EOF)
            printf("%#x narrowed to %#x\n", c, cn);
        else
            printf("%#x could not be narrowed\n", c);
    }
    
    int main(void)
    {
        char* utf_locale_present = setlocale(LC_ALL, "th_TH.utf8");
        assert(utf_locale_present);
        puts("In Thai UTF-8 locale:");
        try_narrowing(L'a');
        try_narrowing(L'๛');
    
        char* tis_locale_present = setlocale(LC_ALL, "th_TH.tis620");
        assert(tis_locale_present);
        puts("In Thai TIS-620 locale:");
        try_narrowing(L'a');
        try_narrowing(L'๛');
    }
```

Saída possível:
```
    In Thai UTF-8 locale:
    0x61 narrowed to 0x61
    0xe5b could not be narrowed
    In Thai TIS-620 locale:
    0x61 narrowed to 0x61
    0xe5b narrowed to 0xfb
```

### Referências

* Padrão C11 (ISO/IEC 9899:2011):

  * 7.29.6.1.2 A função wctob (p: 441)

* Padrão C99 (ISO/IEC 9899:1999):

  * 7.24.6.1.2 A função wctob (p: 387)

### Veja também

[ btowc](<#/doc/string/multibyte/btowc>)(C95) | expande um caractere estreito de byte único para caractere largo, se possível
(função)
[Documentação C++](<#/>) para wctob