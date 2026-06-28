# btowc

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
wint_t btowc( int c );  // desde C95
```

  
Amplia um caractere de byte único `c` (reinterpretado como `unsigned char`) para seu equivalente de caractere largo.

A maioria das codificações de caracteres multibyte usa códigos de byte único para representar os caracteres do conjunto de caracteres ASCII. Esta função pode ser usada para converter tais caracteres para `wchar_t`.

### Parâmetros

c  |  \-  |  caractere de byte único a ser ampliado   
  
### Valor de retorno

`WEOF` se `c` for [EOF](<#/doc/io>)

representação de caractere largo de `c` se `(unsigned char)c` for um caractere de byte único válido no estado de mudança inicial, `WEOF` caso contrário.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <wchar.h>
    #include <locale.h>
    #include <assert.h>
    
    void try_widen(unsigned char c)
    {
        wint_t w = btowc(c);
        if(w != WEOF)
            printf("The single-byte character %#x widens to %#x\n", c, w);
        else
            printf("The single-byte character %#x failed to widen\n", c);
    }
    
    int main(void)
    {
        char *loc = setlocale(LC_ALL, "lt_LT.iso88594");
        assert(loc);
        printf("In Lithuanian ISO-8859-4 locale:\n");
        try_widen('A');
        try_widen('\xdf'); // German letter ß (U+00df) in ISO-8859-4
        try_widen('\xf9'); // Lithuanian letter ų (U+0173) in ISO-8859-4
    
        setlocale(LC_ALL, "lt_LT.utf8");
        printf("In Lithuanian UTF-8 locale:\n");
        try_widen('A');
        try_widen('\xdf');
        try_widen('\xf9');
    }
```

Saída possível: 
```
    In Lithuanian ISO-8859-4 locale:
    The single-byte character 0x41 widens to 0x41
    The single-byte character 0xdf widens to 0xdf
    The single-byte character 0xf9 widens to 0x173
    In Lithuanian UTF-8 locale:
    The single-byte character 0x41 widens to 0x41
    The single-byte character 0xdf failed to widen
    The single-byte character 0xf9 failed to widen
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.29.6.1.1 A função btowc (p: 441) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.24.6.1.1 A função btowc (p: 387) 

### Veja também

[ wctob](<#/doc/string/multibyte/wctob>)(C95) | restringe um caractere largo para um caractere estreito de byte único, se possível   
(função)  
[Documentação C++](<#/>) para btowc