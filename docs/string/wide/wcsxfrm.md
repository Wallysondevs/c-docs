# wcsxfrm

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
size_t wcsxfrm( wchar_t* dest, const wchar_t* src, size_t count );  // até C99
(desde C95)  // desde C95
size_t wcsxfrm( wchar_t* restrict dest, const wchar_t* restrict src, size_t count );  // desde C99
```

Transforma a string larga terminada em nulo apontada por `src` para a forma definida pela implementação, de modo que a comparação de duas strings transformadas com [wcscmp](<#/doc/string/wide/wcscmp>) produza o mesmo resultado que a comparação das strings originais com [wcscoll](<#/doc/string/wide/wcscoll>), na localidade C atual.

Os primeiros `count` caracteres da string transformada são escritos no destino, incluindo o caractere nulo terminador, e o comprimento da string transformada completa é retornado, excluindo o caractere nulo terminador.

Se `count` for ​0​, então `dest` pode ser um ponteiro nulo.

### Notas

O comprimento correto do buffer que pode receber a string transformada inteira é 1+wcsxfrm([NULL](<#/doc/types/NULL>), src, 0)

Esta função é usada ao fazer múltiplas comparações dependentes da localidade usando a mesma string larga ou conjunto de strings largas, porque é mais eficiente usar `wcsxfrm` para transformar todas as strings apenas uma vez e, subsequentemente, comparar as strings largas transformadas com [wcscmp](<#/doc/string/wide/wcscmp>).

### Parâmetros

- **dest** — ponteiro para o primeiro elemento de uma string larga terminada em nulo para onde a string transformada será escrita
- **src** — ponteiro para a string de caracteres largos terminada em nulo a ser transformada
- **count** — número máximo de caracteres a serem produzidos

### Valor de retorno

O comprimento da string larga transformada, não incluindo o caractere nulo terminador.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <wchar.h>
    #include <locale.h>
     
    int main(void)
    {
        setlocale(LC_ALL, "sv_SE.utf8");
     
        const wchar_t *in1 = L"\u00e5r";
        wchar_t out11+wcsxfrm([NULL, in1, 0)];
        wcsxfrm(out1, in1, sizeof out1/sizeof *out1);
     
        const wchar_t *in2 = L"\u00e4ngel";
        wchar_t out21+wcsxfrm([NULL, in2, 0)];
        wcsxfrm(out2, in2, sizeof out2/sizeof *out2);
     
        printf("In the Swedish locale: ");
        if(wcscmp(out1, out2) < 0)
             printf("%ls before %ls\n", in1, in2);
        else
             printf("%ls before %ls\n", in2, in1);
     
        printf("In lexicographical comparison: ");
        if(wcscmp(in1, in2) < 0)
             printf("%ls before %ls\n", in1, in2);
        else
             printf("%ls before %ls\n", in2, in1);
    }
```

Saída:
```
    In the Swedish locale: år before ängel
    In lexicographical comparison: ängel before år
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.29.4.4.4 A função wcsxfrm (p: 434-435)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.24.4.4.4 A função wcsxfrm (p: 380-381)

### Veja também

[ strcoll](<#/doc/string/byte/strcoll>) | compara duas strings de acordo com a localidade atual
(função)
[ wcscoll](<#/doc/string/wide/wcscoll>)(C95) | compara duas strings largas de acordo com a localidade atual
(função)
[ wcscmp](<#/doc/string/wide/wcscmp>)(C95) | compara duas strings largas
(função)
[ strxfrm](<#/doc/string/byte/strxfrm>) | transforma uma string para que strcmp produza o mesmo resultado que strcoll
(função)
[Documentação C++](<#/>) para wcsxfrm