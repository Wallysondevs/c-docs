# memmove, memmove_s

Definido no cabeçalho [`<string.h>`](<#/doc/string/byte>)

```c
void* memmove( void* dest, const void* src, size_t count );
errno_t memmove_s(void* dest, rsize_t destsz, const void* src, rsize_t count);  // desde C11
```

1) Copia count caracteres do objeto apontado por src para o objeto apontado por dest. Ambos os objetos são interpretados como arrays de unsigned char. Os objetos podem se sobrepor: a cópia ocorre como se os caracteres fossem copiados para um array de caracteres temporário e então os caracteres fossem copiados do array para dest.

O comportamento é indefinido se o acesso ocorrer além do final do array dest. O comportamento é indefinido se dest ou src for um ponteiro inválido ou nulo.

2) O mesmo que (1), exceto que, ao detectar os seguintes erros em tempo de execução, ele zera todo o intervalo de destino [dest, dest + destsz) (se dest e destsz forem válidos) e chama a função [constraint handler](<#/doc/error/set_constraint_handler_s>) atualmente instalada:

  * dest ou src é um ponteiro nulo
  * destsz ou count é maior que RSIZE_MAX
  * count é maior que destsz (ocorreria um estouro de buffer)

O comportamento é indefinido se o tamanho do array de caracteres apontado por dest < count <= destsz; em outras palavras, um valor errôneo de destsz não expõe o iminente estouro de buffer.

Assim como todas as funções com verificação de limites, `memmove_s` tem sua disponibilidade garantida apenas se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir [`<string.h>`](<#/doc/string/byte>).

### Parâmetros

- **dest** — ponteiro para o objeto para o qual copiar
- **destsz** — número máximo de bytes a modificar no destino (tipicamente o tamanho do objeto de destino)
- **src** — ponteiro para o objeto do qual copiar
- **count** — número de bytes a copiar

### Valor de retorno

1) Retorna uma cópia de dest

2) Retorna zero em caso de sucesso e um valor diferente de zero em caso de erro. Também em caso de erro, se dest não for um ponteiro nulo e destsz for válido, escreve destsz bytes zero no array de destino.

### Notas

`memmove` pode ser usado para definir o [tipo efetivo](<#/doc/language/object>) de um objeto obtido por uma função de alocação.

Apesar de ser especificado "como se" um buffer temporário fosse usado, as implementações reais desta função não incorrem na sobrecarga ou cópia dupla ou memória extra. Uma abordagem comum (glibc e bsd libc) é copiar bytes para frente a partir do início do buffer se o destino começar antes da origem, e para trás a partir do final caso contrário, com um retorno para a mais eficiente [memcpy](<#/doc/string/byte/memcpy>) quando não há sobreposição alguma.

Onde o [aliasing estrito](<#/doc/language/object>) proíbe examinar a mesma memória como valores de dois tipos diferentes, `memmove` pode ser usado para converter os valores.

### Exemplo

Execute este código
```c
    #define __STDC_WANT_LIB_EXT1__ 1
    #include <inttypes.h>
    #include <stdint.h>
    #include <stdio.h>
    #include <stdlib.h>
    #include <string.h>
    
    int main(void)
    {
        char str[] = "1234567890";
        puts(str);
        memmove(str + 4, str + 3, 3); // copy from [4,5,6] to [5,6,7]
        puts(str);
    
        // setting effective type of allocated memory to be int
        int* p = malloc(3 * sizeof(int)); // allocated memory has no effective type
        int arr[3] = {1, 2, 3};
        memmove(p, arr, 3 * sizeof(int)); // allocated memory now has an effective type
    
        // reinterpreting data
        double d = 0.1;
        // int64_t n = *(int64_t*)(&d); // strict aliasing violation
        int64_t n;
        memmove(&n, &d, sizeof d); // OK
        printf("%a is %" PRIx64 " as an int64_t\n", d, n);
    
    #ifdef __STDC_LIB_EXT1__
        set_constraint_handler_s(ignore_handler_s);
        char src[] = "aaaaaaaaaa";
        char dst[] = "xyxyxyxyxy";
        int r = memmove_s(dst, sizeof dst, src, 5);
        printf("dst = \"%s\", r = %d\n", dst, r);
        r = memmove_s(dst, 5, src, 10); // count is greater than destsz
        printf("dst = \"");
        for (size_t ndx = 0; ndx < sizeof dst; ++ndx)
        {
            char c = dst[ndx];
            c ? printf("%c", c) : printf("\\0");
        }
        printf("\", r = %d\n", r);
    #endif
    }
```

Saída possível:
```
    1234567890
    1234456890
    0x1.999999999999ap-4 is 3fb999999999999a as an int64_t
    dst = "aaaaayxyxy", r = 0
    dst = "\0\0\0\0\0yxyxy", r = 22
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):
    * 7.24.2.2 A função memmove (p: TBD)
    * K.3.7.1.2 A função memmove_s (p: TBD)
  * Padrão C17 (ISO/IEC 9899:2018):
    * 7.24.2.2 A função memmove (p: 264)
    * K.3.7.1.2 A função memmove_s (p: 446)
  * Padrão C11 (ISO/IEC 9899:2011):
    * 7.24.2.2 A função memmove (p: 363)
    * K.3.7.1.2 A função memmove_s (p: 615)
  * Padrão C99 (ISO/IEC 9899:1999):
    * 7.21.2.2 A função memmove (p: 326)
  * Padrão C89/C90 (ISO/IEC 9899:1990):
    * 4.11.2.2 A função memmove

### Veja também

[ memcpymemcpy_s](<#/doc/string/byte/memcpy>)(C11) | copia um buffer para outro
(função)
[ wmemmovewmemmove_s](<#/doc/string/wide/wmemmove>)(C95)(C11) | copia uma certa quantidade de caracteres largos entre dois arrays, possivelmente sobrepostos
(função)
[Documentação C++](<#/>) para memmove