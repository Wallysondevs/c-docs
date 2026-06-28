# memchr

Definido no cabeçalho [`<string.h>`](<#/doc/string/byte>)

```c
void* memchr( const void* ptr, int ch, size_t count );
/*QVoid*/ *memchr( /*QVoid*/ *ptr, int ch, size_t count );  // desde C23
```

1) Encontra a primeira ocorrência de (unsigned char)ch nos primeiros count bytes (cada um interpretado como unsigned char) do objeto apontado por ptr.

2) Função genérica em tipo equivalente a (1). Seja `T` um tipo de objeto não qualificado (incluindo void).

    * Se `ptr` for do tipo const T*, o tipo de retorno é const void*.
    * Caso contrário, se `ptr` for do tipo T*, o tipo de retorno é void*.
    * Caso contrário, o comportamento é indefinido.

Se uma definição de macro de cada uma dessas funções genéricas for suprimida para acessar uma função real (por exemplo, se (memchr) ou um ponteiro de função for usado), a declaração de função real (1) se torna visível.

O comportamento é indefinido se o acesso ocorrer além do final do array pesquisado. O comportamento é indefinido se ptr for um ponteiro nulo.

Esta função se comporta como se lesse os bytes sequencialmente e parasse assim que um byte correspondente fosse encontrado: se o array apontado por ptr for menor que count, mas a correspondência for encontrada dentro do array, o comportamento é bem definido. | (desde C11)

### Parâmetros

- **ptr** — ponteiro para o objeto a ser examinado
- **ch** — byte a ser procurado
- **count** — número máximo de bytes a serem examinados

### Valor de retorno

Ponteiro para a localização do byte, ou um ponteiro nulo se nenhum byte for encontrado.

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <string.h>
    
    int main(void)
    {
        const char str[] = "ABCDEFG";
        const int chars[] = {'D', 'd'};
        for (size_t i = 0; i < sizeof chars / (sizeof chars[0]); ++i)
        {
            const int c = chars[i];
            const char *ps = memchr(str, c, strlen(str));
            ps ? printf ("character '%c'(%i) found: %s\n", c, c, ps)
               : printf ("character '%c'(%i) not found\n", c, c);
        }
        return 0;
    }
```

Saída possível:
```
    character 'D'(68) found: DEFG
    character 'd'(100) not found
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    * 7.24.5.1 A função memchr (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    * 7.24.5.1 A função memchr (p: 267-268)

  * Padrão C11 (ISO/IEC 9899:2011):

    * 7.24.5.1 A função memchr (p: 367)

  * Padrão C99 (ISO/IEC 9899:1999):

    * 7.21.5.1 A função memchr (p: 330)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    * 4.11.5.1 A função memchr

### Veja também

[ strchr](<#/doc/string/byte/strchr>) | encontra a primeira ocorrência de um caractere
(função)
[Documentação C++](<#/>) para memchr