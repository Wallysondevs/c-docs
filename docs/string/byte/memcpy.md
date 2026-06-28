# memcpy, memcpy_s

Definido no cabeçalho [`<string.h>`](<#/doc/string/byte>)

```c
void* memcpy( void *dest, const void *src, size_t count );  // até C99
void* memcpy( void *restrict dest, const void *restrict src, size_t count );  // desde C99
errno_t memcpy_s( void *restrict dest, rsize_t destsz,
const void *restrict src, rsize_t count );  // desde C11
```

1) Copia `count` caracteres do objeto apontado por `src` para o objeto apontado por `dest`. Ambos os objetos são interpretados como arrays de unsigned char.

O comportamento é indefinido se o acesso ocorrer além do final do array `dest`. Se os objetos se sobrepõem (o que é uma violação do contrato [`restrict`](<#/doc/language/restrict>))(desde C99), o comportamento é indefinido. O comportamento é indefinido se `dest` ou `src` for um ponteiro inválido ou nulo.

2) O mesmo que (1), exceto que os seguintes erros são detectados em tempo de execução e fazem com que todo o intervalo de destino [dest, dest+destsz) seja preenchido com zeros (se `dest` e `destsz` forem válidos), além de chamar a função [constraint handler](<#/doc/error/set_constraint_handler_s>) atualmente instalada:

  * `dest` ou `src` é um ponteiro nulo
  * `destsz` ou `count` é maior que RSIZE_MAX
  * `count` é maior que `destsz` (ocorreria um estouro de buffer)
  * os objetos de origem e destino se sobrepõem

O comportamento é indefinido se o tamanho do array de caracteres apontado por `dest` < `count` <= `destsz`; em outras palavras, um valor errôneo de `destsz` não expõe o iminente estouro de buffer.

Assim como todas as funções com verificação de limites, `memcpy_s` tem sua disponibilidade garantida apenas se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir [`<string.h>`](<#/doc/string/byte>).

### Parâmetros

- **dest** — ponteiro para o objeto a ser copiado
- **destsz** — número máximo de bytes a serem modificados no destino (tipicamente o tamanho do objeto de destino)
- **src** — ponteiro para o objeto a ser copiado de
- **count** — número de bytes a serem copiados

### Valor de retorno

1) Retorna uma cópia de `dest`

2) Retorna zero em caso de sucesso e um valor diferente de zero em caso de erro. Também em caso de erro, se `dest` não for um ponteiro nulo e `destsz` for válido, escreve `destsz` bytes zero no array de destino.

### Observações

`memcpy` pode ser usado para definir o [tipo efetivo](<#/doc/language/object>) de um objeto obtido por uma função de alocação.

`memcpy` é a rotina de biblioteca mais rápida para cópia de memória para memória. Geralmente é mais eficiente que [strcpy](<#/doc/string/byte/strcpy>), que deve escanear os dados que copia, ou [memmove](<#/doc/string/byte/memmove>), que deve tomar precauções para lidar com entradas sobrepostas.

Vários compiladores C transformam loops de cópia de memória adequados em chamadas `memcpy`.

Onde o [aliasing estrito](<#/doc/language/object>) proíbe examinar a mesma memória como valores de dois tipos diferentes, `memcpy` pode ser usado para converter os valores.

### Exemplo

Execute este código
```c
    #define __STDC_WANT_LIB_EXT1__ 1
    #include <stdio.h>
    #include <stdint.h>
    #include <inttypes.h>
    #include <string.h>
    #include <stdlib.h>
    
    int main(void)
    {
        // simple usage
        char source[] = "once upon a midnight dreary...", dest[4];
        memcpy(dest, source, sizeof dest);
        for(size_t n = 0; n < sizeof dest; ++n)
            putchar(dest[n]);
    
        // setting effective type of allocated memory to be int
        int *p = malloc(3*sizeof(int));   // allocated memory has no effective type
        int arr[3] = {1,2,3};
        memcpy(p,arr,3*sizeof(int));      // allocated memory now has an effective type
    
        // reinterpreting data
        double d = 0.1;
    //    int64_t n = *(int64_t*)(&d); // strict aliasing violation
        int64_t n;
        memcpy(&n, &d, sizeof d); // OK
        printf("\n%a is %" PRIx64 " as an int64_t\n", d, n);
    
    #ifdef __STDC_LIB_EXT1__
        set_constraint_handler_s(ignore_handler_s);
        char src[] = "aaaaaaaaaa";
        char dst[] = "xyxyxyxyxy";
        int r = memcpy_s(dst,sizeof dst,src,5);
        printf("dst = \"%s\", r = %d\n", dst,r);
        r = memcpy_s(dst,5,src,10);            //  count is greater than destsz  
        printf("dst = \"");
        for(size_t ndx=0; ndx<sizeof dst; ++ndx) {
            char c = dst[ndx];
            c ? printf("%c", c) : printf("\\0");
        }
        printf("\", r = %d\n", r);
    #endif
    }
```

Saída possível:
```
    once
    0x1.999999999999ap-4 is 3fb999999999999a as an int64_t
    dst = "aaaaayxyxy", r = 0
    dst = "\0\0\0\0\0yxyxy", r = 22
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011):

    * 7.24.2.1 A função memcpy (p: 362)

    * K.3.7.1.1 A função memcpy_s (p: 614)

  * Padrão C99 (ISO/IEC 9899:1999):

    * 7.21.2.1 A função memcpy (p: 325)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    * 4.11.2.1 A função memcpy

### Veja também

[ memccpy](<#/doc/string/byte/memccpy>)(C23) | copia um buffer para outro, parando após o delimitador especificado
(função)
[ memmovememmove_s](<#/doc/string/byte/memmove>)(C11) | move um buffer para outro
(função)
[ wmemcpywmemcpy_s](<#/doc/string/wide/wmemcpy>)(C95)(C11) | copia uma certa quantidade de caracteres largos entre dois arrays não sobrepostos
(função)
[documentação C++](<#/>) para memcpy