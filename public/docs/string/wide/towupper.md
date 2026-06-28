# towupper

Definido no cabeçalho [`<wctype.h>`](<#/doc/string/wide>)

```c
wint_t towupper( wint_t wc );  // desde C95
```

Converte o caractere largo fornecido para maiúscula, se possível.

### Parâmetros

- **wc** — caractere largo a ser convertido

### Valor de retorno

Versão em maiúscula de `wc` ou `wc` inalterado se nenhuma versão em maiúscula estiver listada na localidade C atual.

### Notas

Apenas mapeamento de caracteres 1:1 pode ser realizado por esta função, por exemplo, a forma maiúscula de 'ß' é (com algumas exceções) a string de dois caracteres "SS", que não pode ser obtida por `towupper`.

[ISO 30112](<http://www.open-std.org/JTC1/SC35/WG5/docs/30112d10.pdf>) especifica quais pares de caracteres Unicode estão incluídos neste mapeamento.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <wchar.h>
    #include <wctype.h>
    #include <locale.h>
     
    int main(void)
    {
        wchar_t wc =  L'\u017f'; // Latin small letter Long S ('ſ')
        printf("in the default locale, towupper(%#x) = %#x\n", wc, towupper(wc));
        setlocale(LC_ALL, "en_US.utf8");
        printf("in Unicode locale, towupper(%#x) = %#x\n", wc, towupper(wc));
    }
```

Saída:
```
    in the default locale, towupper(0x17f) = 0x17f
    in Unicode locale, towupper(0x17f) = 0x53
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.30.3.1.2 A função towupper (p: 453)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.25.3.1.2 A função towupper (p: 399)

### Veja também

[ towlower](<#/doc/string/wide/towlower>)(C95) | converte um caractere largo para minúscula
(função)
[ toupper](<#/doc/string/byte/toupper>) | converte um caractere para maiúscula
(função)
[Documentação C++](<#/>) para towupper