# memset, memset_explicit, memset_s

Definido no cabeçalho [`<string.h>`](<#/doc/string/byte>)

```c
void *memset( void *dest, int ch, size_t count );
void *memset_explicit( void *dest, int ch, size_t count );  // desde C23
errno_t memset_s( void *dest, rsize_t destsz, int ch, rsize_t count );  // desde C11
```

1) Copia o valor (unsigned char)ch para cada um dos primeiros `count` caracteres do objeto apontado por `dest`.

O comportamento é indefinido se o acesso ocorrer além do final do array `dest`. O comportamento é indefinido se `dest` for um ponteiro nulo.

2) O mesmo que (1), exceto que é seguro para informações sensíveis.

3) O mesmo que (1), exceto que os seguintes erros são detectados em tempo de execução e chamam a função [constraint handler](<#/doc/error/set_constraint_handler_s>) atualmente instalada após armazenar `ch` em cada local do intervalo de destino [dest, dest+destsz) se `dest` e `destsz` forem válidos:

  * `dest` é um ponteiro nulo
  * `destsz` ou `count` é maior que RSIZE_MAX
  * `count` é maior que `destsz` (ocorreria um estouro de buffer)

O comportamento é indefinido se o tamanho do array de caracteres apontado por `dest` < `count` <= `destsz`; em outras palavras, um valor errôneo de `destsz` não expõe o iminente estouro de buffer.

Assim como todas as funções com verificação de limites, `memset_s` só é garantida como disponível se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir `[`<string.h>`](<#/doc/string/byte>)`.

### Parâmetros

- **dest** — ponteiro para o objeto a ser preenchido
- **ch** — byte de preenchimento
- **count** — número de bytes a preencher
- **destsz** — tamanho do array de destino

### Valor de retorno

1,2) Uma cópia de `dest`

3) zero em caso de sucesso, diferente de zero em caso de erro. Também em caso de erro, se `dest` não for um ponteiro nulo e `destsz` for válido, escreve `destsz` bytes de preenchimento `ch` no array de destino.

### Notas

`memset` pode ser otimizada (sob as regras [as-if](<#/doc/language/as_if>)) se o objeto modificado por esta função não for acessado novamente pelo resto de sua vida útil (por exemplo, [bug 8537 do gcc](<https://gcc.gnu.org/bugzilla/show_bug.cgi?id=8537>)). Por essa razão, esta função não pode ser usada para limpar a memória (por exemplo, para preencher um array que armazenou uma senha com zeros).

Esta otimização é proibida para `memset_explicit` e `memset_s`: elas são garantidas para realizar a escrita na memória.

Soluções de terceiros para isso incluem [`explicit_bzero`](<https://www.freebsd.org/cgi/man.cgi?query=explicit_bzero>) do FreeBSD ou [`SecureZeroMemory`](<https://msdn.microsoft.com/en-us/library/windows/desktop/aa366877.aspx>) da Microsoft.

### Exemplo

Execute este código
```c
    #define __STDC_WANT_LIB_EXT1__ 1
    #include <stdio.h>
    #include <string.h>
    #include <stdlib.h>
    
    int main(void)
    {
        char str[] = "ghghghghghghghghghghgh";
        puts(str);
        memset(str,'a',5);
        puts(str);
    
    #ifdef __STDC_LIB_EXT1__
        set_constraint_handler_s(ignore_handler_s);
        int r = memset_s(str, sizeof str, 'b', 5);
        printf("str = \"%s\", r = %d\n", str, r);
        r = memset_s(str, 5, 'c', 10);   // count is greater than destsz  
        printf("str = \"%s\", r = %d\n", str, r);
    #endif
    }
```

Saída possível:
```
    ghghghghghghghghghghgh
    aaaaahghghghghghghghgh
    str = "bbbbbhghghghghghghghgh", r = 0
    str = "ccccchghghghghghghghgh", r = 22
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    * 7.24.6.1 A função memset (p: 270)

    * K.3.7.4.1 A função memset_s (p: 451)

  * Padrão C11 (ISO/IEC 9899:2011):

    * 7.24.6.1 A função memset (p: 371)

    * K.3.7.4.1 A função memset_s (p: 621-622)

  * Padrão C99 (ISO/IEC 9899:1999):

    * 7.21.6.1 A função memset (p: 333)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    * 4.11.6.1 A função memset

### Veja também

[ memcpymemcpy_s](<#/doc/string/byte/memcpy>)(C11) | copia um buffer para outro
(função)
[ wmemset](<#/doc/string/wide/wmemset>)(C95) | copia o caractere largo fornecido para cada posição em um array de caracteres largos
(função)
[documentação C++](<#/>) para memset