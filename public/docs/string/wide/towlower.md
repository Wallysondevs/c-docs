# towlower

Definido no cabeçalho [`<wctype.h>`](<#/doc/string/wide>)

```c
wint_t towlower( wint_t wc );  // desde C95
```

Converte o caractere largo fornecido para minúscula, se possível.

### Parâmetros

- **wc** — caractere largo a ser convertido

### Valor de retorno

Versão em minúscula de wc ou wc inalterado se nenhuma versão em minúscula estiver listada no locale C atual.

### Notas

Apenas mapeamento de caracteres 1:1 pode ser realizado por esta função, por exemplo, a letra maiúscula grega 'Σ' tem duas formas minúsculas, dependendo da posição na palavra: 'σ' e 'ς'. Uma chamada para `towlower` não pode ser usada para obter a forma minúscula correta neste caso.

[ISO 30112](<http://www.open-std.org/JTC1/SC35/WG5/docs/30112d10.pdf>) especifica quais pares de caracteres Unicode estão incluídos neste mapeamento.

### Exemplo

Execute este código
```c
    #include <locale.h>
    #include <stdio.h>
    #include <wchar.h>
    #include <wctype.h>
     
    int main(void)
    {
        wchar_t wc = L'\u0190'; // Latin capital open E ('Ɛ')
        printf("in the default locale, towlower(%#x) = %#x\n", wc, towlower(wc));
        setlocale(LC_ALL, "en_US.utf8");
        printf("in Unicode locale, towlower(%#x) = %#x\n", wc, towlower(wc));
    }
```

Saída:
```
    in the default locale, towlower(0x190) = 0x190
    in Unicode locale, towlower(0x190) = 0x25b
```

### Referências

* C23 standard (ISO/IEC 9899:2024):

  * 7.30.3.1.1 The towlower function (p: TBD)

* C17 standard (ISO/IEC 9899:2018):

  * 7.30.3.1.1 The towlower function (p: TBD)

* C11 standard (ISO/IEC 9899:2011):

  * 7.30.3.1.1 The towlower function (p: 453)

* C99 standard (ISO/IEC 9899:1999):

  * 7.25.3.1.1 The towlower function (p: 399)

### Veja também

[ towupper](<#/doc/string/wide/towupper>)(C95) | converte um caractere largo para maiúscula
(função)
[ tolower](<#/doc/string/byte/tolower>) | converte um caractere para minúscula
(função)
[Documentação C++](<#/>) para towlower