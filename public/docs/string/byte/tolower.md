# tolower

Definido no cabeçalho [`<ctype.h>`](<#/doc/string/byte>)

```c
int tolower( int ch );
```

  
Converte o caractere fornecido para minúscula de acordo com as regras de conversão de caracteres definidas pela localidade C atualmente instalada.

Na localidade "C" padrão, as seguintes letras maiúsculas `ABCDEFGHIJKLMNOPQRSTUVWXYZ` são substituídas pelas respectivas letras minúsculas `abcdefghijklmnopqrstuvwxyz`.

### Parâmetros

ch  |  \-  |  caractere a ser convertido. Se o valor de `ch` não for representável como unsigned char e não for igual a [EOF](<#/doc/io>), o comportamento é indefinido.   
  
### Valor de retorno

Versão minúscula de `ch` ou `ch` inalterado se nenhuma versão minúscula estiver listada na localidade C atual.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <ctype.h>
    #include <locale.h>
    #include <limits.h>
    
    int main(void)
    {
        /* In the default locale: */
        for (unsigned char u = 0; u < UCHAR_MAX; u++) {
            unsigned char l = tolower(u);
            if (l != u) printf("%c%c ", u, l);
        }
        printf("\n\n");
    
        unsigned char c = '\xb4'; // the character Ž in ISO-8859-15
                                  // but ´ (acute accent) in ISO-8859-1
        setlocale(LC_ALL, "en_US.iso88591");
        printf("in iso8859-1, tolower('0x%x') gives 0x%x\n", c, tolower(c));
        setlocale(LC_ALL, "en_US.iso885915");
        printf("in iso8859-15, tolower('0x%x') gives 0x%x\n", c, tolower(c));
    }
```

Saída possível:
```
    Aa Bb Cc Dd Ee Ff Gg Hh Ii Jj Kk Ll Mm Nn Oo Pp Qq Rr Ss Tt Uu Vv Wx Xx Yy Zz
    
    in iso8859-1, tolower('0xb4') gives 0xb4
    in iso8859-15, tolower('0xb4') gives 0xb8
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.4.2.1 A função tolower (p: 147) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.4.2.1 A função tolower (p: 203) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.4.2.1 A função tolower (p: 184) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.3.2.1 A função tolower 

### Veja também

[ toupper](<#/doc/string/byte/toupper>) | converte um caractere para maiúscula   
(função)  
[ towlower](<#/doc/string/wide/towlower>)(C95) | converte um caractere largo para minúscula   
(função)  
[Documentação C++](<#/>) para tolower