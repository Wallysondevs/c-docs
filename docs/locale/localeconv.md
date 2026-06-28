# localeconv

Definido no cabeçalho [`<locale.h>`](<#/doc/locale>)

```c
struct lconv* localeconv(void);
```

A função `localeconv` obtém um ponteiro para um objeto estático do tipo [lconv](<#/doc/locale/lconv>), que representa as regras de formatação numérica e monetária da localidade C atual.

### Parâmetros

(nenhum)

### Valor de retorno

ponteiro para o objeto [lconv](<#/doc/locale/lconv>) atual.

### Notas

Modificar as referências do objeto através do ponteiro retornado é comportamento indefinido.

`localeconv` modifica um objeto estático; chamá-la de diferentes threads sem sincronização é comportamento indefinido.

### Exemplo

Execute este código
```c
    #include <locale.h>
    #include <stdio.h>
    
    int main(void)
    {
        setlocale(LC_MONETARY, "en_IN.utf8");
        struct lconv* lc = localeconv();
        printf("Local Currency Symbol        : %s\n", lc->currency_symbol);
        printf("International Currency Symbol: %s\n", lc->int_curr_symbol);
    }
```

Saída:
```
    Local Currency Symbol        : ₹
    International Currency Symbol: INR
```

### Referências

*   Padrão C23 (ISO/IEC 9899:2024):

    *   7.11.2.1 A função localeconv (p: TBD)

*   Padrão C17 (ISO/IEC 9899:2018):

    *   7.11.2.1 A função localeconv (p: TBD)

*   Padrão C11 (ISO/IEC 9899:2011):

    *   7.11.2.1 A função localeconv (p: 225-230)

*   Padrão C99 (ISO/IEC 9899:1999):

    *   7.11.2.1 A função localeconv (p: 206-211)

*   Padrão C89/C90 (ISO/IEC 9899:1990):

    *   4.4.2.1 A função localeconv

### Veja também

[ setlocale](<#/doc/locale/setlocale>) | obtém e define a localidade C atual
(função)
[ lconv](<#/doc/locale/lconv>) | detalhes de formatação, retornado por **localeconv**
(struct)
[Documentação C++](<#/>) para localeconv