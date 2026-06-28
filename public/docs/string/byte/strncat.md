# strncat, strncat_s

Definido no cabeçalho [`<string.h>`](<#/doc/string/byte>)

```c
char *strncat( char *dest, const char *src, size_t count );  // até C99
char *strncat( char *restrict dest, const char *restrict src, size_t count );  // desde C99
errno_t strncat_s( char *restrict dest, rsize_t destsz,
const char *restrict src, rsize_t count );  // desde C11
```

1) Anexa no máximo `count` caracteres do array de caracteres apontado por `src`, parando se o caractere nulo for encontrado, ao final da string de bytes terminada em nulo apontada por `dest`. O caractere src[0] substitui o terminador nulo no final de `dest`. O caractere nulo de terminação é sempre anexado no final (portanto, o número máximo de bytes que a função pode escrever é count+1).

O comportamento é indefinido se o array de destino não tiver espaço suficiente para o conteúdo de `dest` e os primeiros `count` caracteres de `src`, mais o caractere nulo de terminação. O comportamento é indefinido se os objetos de origem e destino se sobrepuserem. O comportamento é indefinido se `dest` não for um ponteiro para uma string de bytes terminada em nulo ou se `src` não for um ponteiro para um array de caracteres.

2) O mesmo que (1), exceto que esta função pode sobrescrever o restante do array de destino (do último byte escrito até `destsz`) e que os seguintes erros são detectados em tempo de execução e chamam a função [constraint handler](<#/doc/error/set_constraint_handler_s>) atualmente instalada:

  * `src` ou `dest` é um ponteiro nulo
  * `destsz` ou `count` é zero ou maior que RSIZE_MAX
  * não há caractere nulo nos primeiros `destsz` bytes de `dest`
  * ocorreria truncamento: `count` ou o comprimento de `src`, o que for menor, excede o espaço disponível entre o terminador nulo de `dest` e `destsz`.
  * ocorreria sobreposição entre as strings de origem e destino

O comportamento é indefinido se o tamanho do array de caracteres apontado por `dest` < strnlen(dest,destsz)+strnlen(src,count)+1 < `destsz`; em outras palavras, um valor errôneo de `destsz` não expõe o iminente estouro de buffer. O comportamento é indefinido se o tamanho do array de caracteres apontado por `src` < strnlen(src,count) < `destsz`; em outras palavras, um valor errôneo de `count` não expõe o iminente estouro de buffer.

Assim como todas as funções com verificação de limites, `strncat_s` só é garantida como disponível se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir [`<string.h>`](<#/doc/string/byte>).

### Parâmetros

- **dest** — ponteiro para a string de bytes terminada em nulo à qual anexar
- **src** — ponteiro para o array de caracteres do qual copiar
- **count** — número máximo de caracteres a copiar
- **destsz** — o tamanho do buffer de destino

### Valor de retorno

1) retorna uma cópia de `dest`

2) retorna zero em caso de sucesso, retorna um valor diferente de zero em caso de erro. Além disso, em caso de erro, escreve zero em dest[0] (a menos que `dest` seja um ponteiro nulo ou `destsz` seja zero ou maior que RSIZE_MAX).

### Notas

Como `strncat` precisa procurar o final de `dest` em cada chamada, é ineficiente concatenar muitas strings em uma usando `strncat`.

Embora o truncamento para caber no buffer de destino seja um risco de segurança e, portanto, uma violação das restrições de tempo de execução para `strncat_s`, é possível obter o comportamento de truncamento especificando `count` igual ao tamanho do array de destino menos um: ele copiará os primeiros `count` bytes e anexará o terminador nulo como sempre: strncat_s(dst, sizeof dst, src, (sizeof dst)-strnlen_s(dst, sizeof dst)-1);

### Exemplo

Execute este código
```c
    #define __STDC_WANT_LIB_EXT1__ 1
    #include <string.h>
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(void)
    {
        char str[50] = "Hello ";
        char str2[50] = "World!";
        strcat(str, str2);
        strncat(str, " Goodbye World!", 3);
        puts(str);
    
    #ifdef __STDC_LIB_EXT1__
        set_constraint_handler_s(ignore_handler_s);
        char s1[100] = "good";
        char s5[1000] = "bye";
        int r1 = strncat_s(s1, 100, s5, 1000); // r1 is 0, s1 holds "goodbye\0"
        printf("s1 = %s, r1 = %d\n", s1, r1);
        char s2[6] = "hello";
        int r2 = strncat_s(s2, 6, "", 1); // r2 is 0, s2 holds "hello\0"
        printf("s2 = %s, r2 = %d\n", s2, r2);
        char s3[6] = "hello";
        int r3 = strncat_s(s3, 6, "X", 2); // r3 is non-zero, s3 holds "\0"
        printf("s3 = %s, r3 = %d\n", s3, r3);
        // the strncat_s truncation idiom:
        char s4[7] = "abc";
        int r4 = strncat_s(s4, 7, "defghijklmn", 3); // r4 is 0, s4 holds "abcdef\0"
        printf("s4 = %s, r4 = %d\n", s4, r4);
    #endif
    }
```

Saída possível:
```
    Hello World! Go
    s1 = goodbye, r1 = 0
    s2 = hello, r2 = 0
    s3 = , r3 = 22
    s4 = abcdef, r4 = 0
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    * 7.26.3.2 A função strncat (p: 379)

    * K.3.7.2.2 A função strncat_s (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    * 7.24.3.2 A função strncat (p: 265-266)

    * K.3.7.2.2 A função strncat_s (p: 449-450)

  * Padrão C11 (ISO/IEC 9899:2011):

    * 7.24.3.2 A função strncat (p: 364-365)

    * K.3.7.2.2 A função strncat_s (p: 618-620)

  * Padrão C99 (ISO/IEC 9899:1999):

    * 7.21.3.2 A função strncat (p: 327-328)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    * 4.11.3.2 A função strncat

### Veja também

[ strcatstrcat_s](<#/doc/string/byte/strcat>)(C11) | concatena duas strings
(função)
[ strcpystrcpy_s](<#/doc/string/byte/strcpy>)(C11) | copia uma string para outra
(função)
[ memccpy](<#/doc/string/byte/memccpy>)(C23) | copia um buffer para outro, parando após o delimitador especificado
(função)
[Documentação C++](<#/>) para strncat