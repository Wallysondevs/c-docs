# strxfrm

Definido no cabeçalho [`<string.h>`](<#/doc/string/byte>)

```c
size_t strxfrm( char *dest, const char *src, size_t count );  // até C99
size_t strxfrm( char *restrict dest, const char *restrict src, size_t count );  // desde C99
```

Transforma a string de bytes terminada em nulo apontada por `src` para a forma definida pela implementação, de modo que comparar duas strings transformadas com [strcmp](<#/doc/string/byte/strcmp>) produza o mesmo resultado que comparar as strings originais com [strcoll](<#/doc/string/byte/strcoll>), na localidade C atual.

Os primeiros `count` caracteres da string transformada são escritos no destino, incluindo o caractere nulo terminador, e o comprimento da string transformada completa é retornado, excluindo o caractere nulo terminador.

O comportamento é indefinido se o array `dest` não for grande o suficiente. O comportamento é indefinido se `dest` e `src` se sobrepuserem.

Se `count` for ​0​, então `dest` pode ser um ponteiro nulo.

### Notas

O comprimento correto do buffer que pode receber a string transformada inteira é 1+strxfrm([NULL](<#/doc/types/NULL>), src, 0)

Esta função é usada ao fazer múltiplas comparações dependentes da localidade usando a mesma string ou conjunto de strings, porque é mais eficiente usar `strxfrm` para transformar todas as strings apenas uma vez e, subsequentemente, comparar as strings transformadas com [strcmp](<#/doc/string/byte/strcmp>).

### Parâmetros

- **dest** — ponteiro para o primeiro elemento do array onde a string transformada será escrita
- **src** — ponteiro para o primeiro caractere de uma string de bytes terminada em nulo a ser transformada
- **count** — número máximo de caracteres a serem escritos

### Valor de retorno

O comprimento da string transformada, não incluindo o caractere nulo terminador.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <string.h>
    #include <locale.h>
    
    int main(void)
    {
        setlocale(LC_COLLATE, "cs_CZ.iso88592");
    
        const char *in1 = "hrnec";
        char out11+strxfrm([NULL, in1, 0)];
        strxfrm(out1, in1, sizeof out1);
    
        const char *in2 = "chrt";
        char out21+strxfrm([NULL, in2, 0)];
        strxfrm(out2, in2, sizeof out2);
    
        printf("In the Czech locale: ");
        if(strcmp(out1, out2) < 0)
             printf("%s before %s\n",in1, in2);
        else
             printf("%s before %s\n",in2, in1);
    
        printf("In lexicographical comparison: ");
        if(strcmp(in1, in2)<0)
             printf("%s before %s\n",in1, in2);
        else
             printf("%s before %s\n",in2, in1);
    
    }
```

Saída possível:
```
    In the Czech locale: hrnec before chrt
    In lexicographical comparison: chrt before hrnec
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.24.4.5 A função strxfrm (p: 267)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.24.4.5 A função strxfrm (p: 366-367)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.21.4.5 A função strxfrm (p: 329-330)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.11.4.5 A função strxfrm

### Veja também

[ strcoll](<#/doc/string/byte/strcoll>) | compara duas strings de acordo com a localidade atual
(função)
[ wcscoll](<#/doc/string/wide/wcscoll>)(C95) | compara duas wide strings de acordo com a localidade atual
(função)
[ strcmp](<#/doc/string/byte/strcmp>) | compara duas strings
(função)
[ wcsxfrm](<#/doc/string/wide/wcsxfrm>)(C95) | transforma uma wide string para que wcscmp produza o mesmo resultado que wcscoll
(função)
[Documentação C++](<#/>) para strxfrm