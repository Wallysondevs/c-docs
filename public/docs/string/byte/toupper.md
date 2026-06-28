# toupper

Definido no cabeçalho [`<ctype.h>`](<#/doc/string/byte>)

```c
int toupper( int ch );
```

  
Converte o caractere fornecido para maiúscula de acordo com as regras de conversão de caracteres definidas pela localidade C atualmente instalada.

Na localidade "C" padrão, as seguintes letras minúsculas `abcdefghijklmnopqrstuvwxyz` são substituídas pelas respectivas letras maiúsculas `ABCDEFGHIJKLMNOPQRSTUVWXYZ`.

### Parâmetros

ch  |  \-  |  caractere a ser convertido. Se o valor de ch não for representável como unsigned char e não for igual a [EOF](<#/doc/io>), o comportamento é indefinido.   
  
### Valor de retorno

Versão maiúscula de ch ou ch não modificado se nenhuma versão maiúscula estiver listada na localidade C atual.

### Exemplo

Execute este código
```c
    #include <ctype.h>
    #include <limits.h>
    #include <locale.h>
    #include <stdio.h>
     
    int main(void)
    {
        // in the default locale:
        for (unsigned char l = 0, u; l != UCHAR_MAX; ++l)
            if ((u = toupper(l)) != l)
                printf("%c%c ", l, u);
        printf("\n\n");
     
        unsigned char c = '\xb8'; // the character ž in ISO-8859-15
                                  // but ¸ (cedilla) in ISO-8859-1
        setlocale(LC_ALL, "en_US.iso88591");
        printf("in iso8859-1, toupper('0x%x') gives 0x%x\n", c, toupper(c));
        setlocale(LC_ALL, "en_US.iso885915");
        printf("in iso8859-15, toupper('0x%x') gives 0x%x\n", c, toupper(c));
    }
```

Saída possível:
```
    aA bB cC dD eE fF gG hH iI jJ kK lL mM nN oO pP qQ rR sS tT uU vV wW xX yY zZ
     
    in iso8859-1, toupper('0xb8') gives 0xb8
    in iso8859-15, toupper('0xb8') gives 0xb4
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.4.2.2 A função toupper (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.4.2.2 A função toupper (p: 147-148) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.4.2.2 A função toupper (p: 204) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.4.2.2 A função toupper (p: 185) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.3.2.2 A função toupper 

### Veja também

[ tolower](<#/doc/string/byte/tolower>) |  converte um caractere para minúscula   
(função)  
[ towupper](<#/doc/string/wide/towupper>)(C95) |  converte um caractere largo para maiúscula   
(função)  
[documentação C++](<#/>) para toupper