# strcpy, strcpy_s

Definido no cabeçalho [`<string.h>`](<#/doc/string/byte>)

```c
char *strcpy( char *dest, const char *src );  // até C99
char *strcpy( char *restrict dest, const char *restrict src );  // desde C99
errno_t strcpy_s( char *restrict dest, rsize_t destsz, const char *restrict src );  // desde C11
```

1) Copia a string de bytes terminada em nulo apontada por `src`, incluindo o terminador nulo, para o array de caracteres cujo primeiro elemento é apontado por `dest`.

O comportamento é indefinido se o array `dest` não for grande o suficiente. O comportamento é indefinido se as strings se sobrepuserem. O comportamento é indefinido se `dest` não for um ponteiro para um array de caracteres ou se `src` não for um ponteiro para uma string de bytes terminada em nulo.

2) O mesmo que (1), exceto que pode sobrescrever o restante do array de destino com valores não especificados e que os seguintes erros são detectados em tempo de execução e chamam a função [manipulador de restrição](<#/doc/error/set_constraint_handler_s>) atualmente instalada:

  * `src` ou `dest` é um ponteiro nulo
  * `destsz` é zero ou maior que RSIZE_MAX
  * `destsz` é menor ou igual a strnlen_s(src, destsz); em outras palavras, ocorreria truncamento
  * ocorreria sobreposição entre as strings de origem e destino

O comportamento é indefinido se o tamanho do array de caracteres apontado por `dest` <= strnlen_s(src, destsz) < `destsz`; em outras palavras, um valor errôneo de `destsz` não expõe o iminente estouro de buffer.

Assim como todas as funções com verificação de limites, `strcpy_s` tem sua disponibilidade garantida apenas se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir [`<string.h>`](<#/doc/string/byte>).

### Parâmetros

- **dest** — ponteiro para o array de caracteres onde escrever
- **src** — ponteiro para a string de bytes terminada em nulo de onde copiar
- **destsz** — número máximo de caracteres a serem escritos, tipicamente o tamanho do buffer de destino

### Valor de retorno

1) retorna uma cópia de `dest`

2) retorna zero em caso de sucesso, retorna um valor diferente de zero em caso de erro. Além disso, em caso de erro, escreve zero em dest[0] (a menos que `dest` seja um ponteiro nulo ou `destsz` seja zero ou maior que RSIZE_MAX).

### Observações

É permitido que `strcpy_s` sobrescreva o array de destino do último caractere escrito até `destsz` para melhorar a eficiência: ele pode copiar em blocos de múltiplos bytes e então verificar por bytes nulos.

A função `strcpy_s` é semelhante à função BSD `strlcpy`, exceto que

  * `strlcpy` trunca a string de origem para caber no destino (o que é um risco de segurança)
  * `strlcpy` não realiza todas as verificações em tempo de execução que `strcpy_s` faz
  * `strlcpy` não torna as falhas óbvias definindo o destino como uma string nula ou chamando um manipulador se a chamada falhar.

Embora `strcpy_s` proíba o truncamento devido a potenciais riscos de segurança, é possível truncar uma string usando [strncpy_s](<#/doc/string/byte/strncpy>) com verificação de limites.

### Exemplo

Execute este código
```c
    #define __STDC_WANT_LIB_EXT1__ 1
    #include <string.h>
    #include <stdio.h>
    #include <stdlib.h>
     
    int main(void)
    {
        const char *src = "Take the test.";
    //  src[0] = 'M' ; // this would be undefined behavior
        char dst[strlen(src) + 1]; // +1 to accommodate for the null terminator
        strcpy(dst, src);
        dst[0] = 'M'; // OK
        printf("src = %s\ndst = %s\n", src, dst);
     
    #ifdef __STDC_LIB_EXT1__
        set_constraint_handler_s(ignore_handler_s);
        int r = strcpy_s(dst, sizeof dst, src);
        printf("dst = \"%s\", r = %d\n", dst, r);
        r = strcpy_s(dst, sizeof dst, "Take even more tests.");
        printf("dst = \"%s\", r = %d\n", dst, r);
    #endif
    }
```

Saída possível:
```
    src = Take the test.
    dst = Make the test.
    dst = "Take the test.", r = 0
    dst = "", r = 22
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

  * 7.24.2.3 A função strcpy (p: 264-265)

  * K.3.7.1.3 A função strcpy_s (p: 447)

  * Padrão C11 (ISO/IEC 9899:2011):

  * 7.24.2.3 A função strcpy (p: 363)

  * K.3.7.1.3 A função strcpy_s (p: 615-616)

  * Padrão C99 (ISO/IEC 9899:1999):

  * 7.21.2.3 A função strcpy (p: 326)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

  * 4.11.2.3 A função strcpy

### Veja também

[ strncpystrncpy_s](<#/doc/string/byte/strncpy>)(C11) | copia uma certa quantidade de caracteres de uma string para outra
(função)
[ memcpymemcpy_s](<#/doc/string/byte/memcpy>)(C11) | copia um buffer para outro
(função)
[ wcscpywcscpy_s](<#/doc/string/wide/wcscpy>)(C95)(C11) | copia uma string larga para outra
(função)
[ strdup](<#/doc/experimental/dynamic/strdup>)(TR de memória dinâmica) | aloca uma cópia de uma string
(função)
[Documentação C++](<#/>) para strcpy