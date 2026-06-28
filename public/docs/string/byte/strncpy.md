# strncpy, strncpy_s

Definido no cabeçalho [`<string.h>`](<#/doc/string/byte>)

```c
char *strncpy( char *dest, const char *src, size_t count );  // até C99
char *strncpy( char *restrict dest, const char *restrict src, size_t count );  // desde C99
errno_t strncpy_s( char *restrict dest, rsize_t destsz,
const char *restrict src, rsize_t count );  // desde C11
```

1) Copia no máximo `count` caracteres do array de caracteres apontado por `src` (incluindo o caractere nulo terminador, mas não nenhum dos caracteres que seguem o caractere nulo) para o array de caracteres apontado por `dest`.

Se `count` for atingido antes que todo o array `src` seja copiado, o array de caracteres resultante não será terminado em nulo.

Se, após copiar o caractere nulo terminador de `src`, `count` não for atingido, caracteres nulos adicionais são escritos em `dest` até que um total de `count` caracteres tenha sido escrito.

O comportamento é indefinido se os arrays de caracteres se sobrepõem, se `dest` ou `src` não é um ponteiro para um array de caracteres (incluindo se `dest` ou `src` é um ponteiro nulo), se o tamanho do array apontado por `dest` é menor que `count`, ou se o tamanho do array apontado por `src` é menor que `count` e ele não contém um caractere nulo.

2) O mesmo que (1), exceto que a função não continua escrevendo zeros no array de destino para preencher até `count`, ela para após escrever o caractere nulo terminador (se não houver nulo na origem, ela escreve um em dest[count] e então para). Além disso, os seguintes erros são detectados em tempo de execução e chamam a função [manipulador de restrição](<#/doc/error/set_constraint_handler_s>) atualmente instalada:

  * `src` ou `dest` é um ponteiro nulo
  * `destsz` é zero ou maior que RSIZE_MAX
  * `count` é maior que RSIZE_MAX
  * `count` é maior ou igual a `destsz`, mas `destsz` é menor ou igual a strnlen_s(src, count), em outras palavras, ocorreria truncamento
  * ocorreria sobreposição entre as strings de origem e destino

O comportamento é indefinido se o tamanho do array de caracteres apontado por `dest` < strnlen_s(src, destsz) <= `destsz`; em outras palavras, um valor errôneo de `destsz` não expõe o iminente estouro de buffer. O comportamento é indefinido se o tamanho do array de caracteres apontado por `src` < strnlen_s(src, count) < `destsz`; em outras palavras, um valor errôneo de `count` não expõe o iminente estouro de buffer.

Assim como todas as funções com verificação de limites, `strncpy_s` tem sua disponibilidade garantida apenas se `__STDC_LIB_EXT1__` for definido pela implementação e se o usuário definir `__STDC_WANT_LIB_EXT1__` para a constante inteira 1 antes de incluir [`<string.h>`](<#/doc/string/byte>).

### Parâmetros

- **dest** — ponteiro para o array de caracteres para o qual copiar
- **src** — ponteiro para o array de caracteres do qual copiar
- **count** — número máximo de caracteres a copiar
- **destsz** — o tamanho do buffer de destino

### Valor de retorno

1) retorna uma cópia de `dest`

2) retorna zero em caso de sucesso, retorna um valor diferente de zero em caso de erro. Além disso, em caso de erro, escreve zero em dest[0] (a menos que `dest` seja um ponteiro nulo ou `destsz` seja zero ou maior que RSIZE_MAX) e pode sobrescrever o restante do array de destino com valores não especificados.

### Notas

Conforme corrigido pelo DR 468 pós-C11, `strncpy_s`, ao contrário de [strcpy_s](<#/doc/string/byte/strcpy>), só tem permissão para sobrescrever o restante do array de destino se ocorrer um erro.

Ao contrário de `strncpy`, `strncpy_s` não preenche o array de destino com zeros. Esta é uma fonte comum de erros ao converter código existente para a versão com verificação de limites.

Embora o truncamento para caber no buffer de destino seja um risco de segurança e, portanto, uma violação das restrições de tempo de execução para `strncpy_s`, é possível obter o comportamento de truncamento especificando `count` igual ao tamanho do array de destino menos um: ele copiará os primeiros `count` bytes e anexará o terminador nulo como sempre: strncpy_s(dst, sizeof dst, src, (sizeof dst)-1);

### Exemplo

Run this code
```c
    #define __STDC_WANT_LIB_EXT1__ 1
    #include <string.h>
    #include <stdio.h>
    #include <stdlib.h>
    #include <errno.h>
     
    int main(void)
    {
        char src[] = "hi";
        char dest[6] = "abcdef"; // no null terminator
        strncpy(dest, src, 5); // writes five characters 'h', 'i', '\0', '\0', '\0' to dest
        printf("strncpy(dest, src, 5) to a 6-byte dest gives : ");
        for (size_t n = 0; n < sizeof dest; ++n) {
            char c = dest[n];
            c ? printf("'%c' ", c) : printf("'\\0' ");
        }
     
        printf("\nstrncpy(dest2, src, 2) to a 2-byte dst gives : ");
        char dest2[2];
        strncpy(dest2, src, 2); // truncation: writes two characters 'h', 'i', to dest2
        for (size_t n = 0; n < sizeof dest2; ++n) {
            char c = dest2[n];
            c ? printf("'%c' ", c) : printf("'\\0' ");
        }
        printf("\n");
     
    #ifdef __STDC_LIB_EXT1__
        set_constraint_handler_s(ignore_handler_s);
        char dst1[6], src1[100] = "hello";
        errno_t r1 = strncpy_s(dst1, 6, src1, 100);  // writes 0 to r1, 6 characters to dst1
        printf("dst1 = \"%s\", r1 = %d\n", dst1,r1); // 'h','e','l','l','o','\0' to dst1
     
        char dst2[5], src2[7] = {'g','o','o','d','b','y','e'};
        errno_t r2 = strncpy_s(dst2, 5, src2, 7);    // copy overflows the destination array
        printf("dst2 = \"%s\", r2 = %d\n", dst2,r2); // writes nonzero to r2,'\0' to dst2[0]
     
        char dst3[5];
        errno_t r3 = strncpy_s(dst3, 5, src2, 4);    // writes 0 to r3, 5 characters to dst3
        printf("dst3 = \"%s\", r3 = %d\n", dst3,r3); // 'g', 'o', 'o', 'd', '\0' to dst3
    #endif
    }
```

Possible output:
```
    strncpy(dest, src, 5) to a 6-byte dst gives : 'h' 'i' '\0' '\0' '\0' 'f'
    strncpy(dest2, src, 2) to a 2-byte dst gives : 'h' 'i'
    dst1 = "hello", r1 = 0
    dst2 = "", r2 = 22
    dst3 = "good", r3 = 0
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    * 7.24.2.4 A função strncpy (p: 265)

    * K.3.7.1.4 A função strncpy_s (p: 447-448)

  * Padrão C11 (ISO/IEC 9899:2011):

    * 7.24.2.4 A função strncpy (p: 363-364)

    * K.3.7.1.4 A função strncpy_s (p: 616-617)

  * Padrão C99 (ISO/IEC 9899:1999):

    * 7.21.2.4 A função strncpy (p: 326-327)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    * 4.11.2.4 A função strncpy

### Veja também

[ strcpystrcpy_s](<#/doc/string/byte/strcpy>)(C11) | copia uma string para outra
(função)
[ memcpymemcpy_s](<#/doc/string/byte/memcpy>)(C11) | copia um buffer para outro
(função)
[ strndup](<#/doc/experimental/dynamic/strndup>)(TR de memória dinâmica) | aloca uma cópia de uma string até um tamanho especificado
(função)
[Documentação C++](<#/>) para strncpy