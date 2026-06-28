# wcscpy, wcscpy_s

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
wchar_t* wcscpy( wchar_t* dest, const wchar_t* src );  // desde C95
(até C99)  // até C99
wchar_t* wcscpy( wchar_t* restrict dest, const wchar_t* restrict src );  // desde C99
errno_t wcscpy_s( wchar_t* restrict dest, rsize_t destsz,
const wchar_t* restrict src );  // desde C11
```

1) Copia a string larga apontada por src (incluindo o caractere largo nulo terminador) para o array de caracteres largos apontado por dest. O comportamento é indefinido se o array dest não for grande o suficiente. O comportamento é indefinido se as strings se sobrepuserem.

2) O mesmo que (1), exceto que pode sobrescrever o restante do array de destino com valores não especificados e que os seguintes erros são detectados em tempo de execução e chamam a função [manipulador de restrição](<#/doc/error/set_constraint_handler_s>) atualmente instalada:

  * src ou dest é um ponteiro nulo
  * destsz é zero ou maior que RSIZE_MAX / sizeof(wchar_t)
  * destsz é menor ou igual a wcsnlen_s(src, destsz), em outras palavras, ocorreria truncamento
  * ocorreria sobreposição entre as strings de origem e de destino

Assim como todas as funções com verificação de limites, `wcscpy_s` é garantida como disponível apenas se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir [`<wchar.h>`](<#/doc/string/wide>).

### Parâmetros

- **dest** — ponteiro para o array de caracteres largos para o qual copiar
- **src** — ponteiro para a string larga terminada em nulo da qual copiar
- **destsz** — número máximo de caracteres a serem escritos, tipicamente o tamanho do buffer de destino

### Valor de retorno

1) retorna uma cópia de dest

2) retorna zero em caso de sucesso, retorna um valor diferente de zero em caso de erro. Além disso, em caso de erro, escreve L'\0' em dest[0] (a menos que dest seja um ponteiro nulo ou destsz seja zero ou maior que RMAX_SIZE / sizeof(wchar_t)).

### Exemplo

Execute este código
```c
    #include <locale.h>
    #include <stdio.h>
    #include <wchar.h>
    
    int main(void)
    {
        wchar_t* src = L"犬 means dog";
    //  src[0] = L'狗' ; // this would be undefined behavior
        wchar_t dst[wcslen(src) + 1]; // +1 for the null terminator
        wcscpy(dst, src);
        dst[0] = L'狗'; // OK
    
        setlocale(LC_ALL, "en_US.utf8");
        printf("src = %ls\ndst = %ls\n", src, dst);
    }
```

Saída:
```
    src = 犬 means dog
    dst = 狗 means dog
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.29.4.1.2 A função wcscpy (p: TBD)

    

  * K.3.9.2.1.1 A função wcscpy_s (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.29.4.1.2 A função wcscpy (p: TBD)

    

  * K.3.9.2.1.1 A função wcscpy_s (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.29.4.1.2 A função wcscpy (p: 430)

    

  * K.3.9.2.1.1 A função wcscpy_s (p: 639)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.24.4.1.2 A função wcscpy (p: 376)

### Veja também

[ wcsncpywcsncpy_s](<#/doc/string/wide/wcsncpy>)(C95)(C11) | copia uma certa quantidade de caracteres largos de uma string para outra
(função)
[ wmemcpywmemcpy_s](<#/doc/string/wide/wmemcpy>)(C95)(C11) | copia uma certa quantidade de caracteres largos entre dois arrays não sobrepostos
(função)
[ strcpystrcpy_s](<#/doc/string/byte/strcpy>)(C11) | copia uma string para outra
(função)
[Documentação C++](<#/>) para wcscpy