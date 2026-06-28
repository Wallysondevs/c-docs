# wmemset

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
wchar_t* wmemset( wchar_t* dest, wchar_t ch, size_t count );  // desde C95
```

Copia o caractere largo ch para cada um dos primeiros count caracteres largos do array de caracteres largos (ou array de inteiros de tipo compatível) apontado por dest.

Se ocorrer estouro, o comportamento é indefinido.

Se count for zero, a função não faz nada.

### Parâmetros

- **dest** — ponteiro para o array de caracteres largos a ser preenchido
- **ch** — caractere largo de preenchimento
- **count** — número de caracteres largos a preencher

### Valor de retorno

Retorna uma cópia de dest

### Observações

Esta função não é sensível à localidade e não presta atenção aos valores dos objetos wchar_t que ela escreve: nulos, assim como caracteres largos inválidos, também são escritos.

### Exemplo

Execute este código
```c
    #include <locale.h>
    #include <stdio.h>
    #include <wchar.h>
     
    int main(void)
    {
        wchar_t ar[10] = L"1234567890"; // no trailing null in the array
        wmemset(ar, L'\U0001f34c', 5); // replaces [12345] with the 🍌 bananas
        wmemset(ar + 5, L'蕉', 5); // replaces [67890] with the 蕉 bananas
     
        setlocale(LC_ALL, "en_US.utf8");
        for (size_t n = 0; n < sizeof ar / sizeof *ar; ++n)
            putwchar(ar[n]);
        putwchar(L'\n');
    }
```

Saída:
```
    🍌🍌🍌🍌🍌蕉蕉蕉蕉蕉
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.29.4.6.2 A função wmemset (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.29.4.6.2 A função wmemset (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.29.4.6.2 A função wmemset (p: 439)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.24.4.6.2 A função wmemset (p: 385)

### Veja também

[ memsetmemset_explicitmemset_s](<#/doc/string/byte/memset>)(C23)(C11) | preenche um buffer com um caractere
(função)
[ wmemcpywmemcpy_s](<#/doc/string/wide/wmemcpy>)(C95)(C11) | copia uma certa quantidade de caracteres largos entre dois arrays não sobrepostos
(função)
[Documentação C++](<#/>) para wmemset