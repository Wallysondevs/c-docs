# memcmp

Definido no cabeçalho [`<string.h>`](<#/doc/string/byte>)

```c
int memcmp( const void* lhs, const void* rhs, size_t count );
```

Compara os primeiros count bytes dos objetos apontados por lhs e rhs. A comparação é feita lexicograficamente.

O sinal do resultado é o sinal da diferença entre os valores do primeiro par de bytes (ambos interpretados como unsigned char) que diferem nos objetos sendo comparados.

O comportamento é indefinido se o acesso ocorrer além do final de qualquer um dos objetos apontados por lhs e rhs. O comportamento é indefinido se lhs ou rhs for um ponteiro nulo.

### Parâmetros

- **lhs, rhs** — ponteiros para os objetos a serem comparados
- **count** — número de bytes a serem examinados

### Valor de retorno

Valor negativo se lhs aparecer antes de rhs na ordem lexicográfica.

Zero se lhs e rhs forem iguais na comparação, ou se count for zero.

Valor positivo se lhs aparecer depois de rhs na ordem lexicográfica.

### Notas

Esta função lê [representações de objeto](<#/doc/language/object>), não os valores do objeto, e é tipicamente significativa apenas para arrays de bytes: structs podem ter bytes de preenchimento cujos valores são indeterminados, os valores de quaisquer bytes além do último membro armazenado em uma union são indeterminados, e um tipo pode ter duas ou mais representações para o mesmo valor (codificações diferentes para +0 e -0 ou para +0.0 e –0.0, bits de preenchimento indeterminados dentro do tipo).

### Exemplo

Execute este código
```
    #include <stdio.h>
    #include <string.h>
    
    void demo(const char* lhs, const char* rhs, size_t sz)
    {
        for(size_t n = 0; n < sz; ++n)
            putchar(lhs[n]);
    
        int rc = memcmp(lhs, rhs, sz);
        const char *rel = rc < 0 ? " precedes " : rc > 0 ? " follows " : " compares equal ";
        fputs(rel, stdout);
    
        for(size_t n = 0; n < sz; ++n)
            putchar(rhs[n]);
        puts(" in lexicographical order");
    }
    
    int main(void)
    {
        char a1[] = {'a','b','c'};
        char a2[sizeof a1] = {'a','b','d'};
    
        demo(a1, a2, sizeof a1);
        demo(a2, a1, sizeof a1);
        demo(a1, a1, sizeof a1);
    }
```

Saída:
```
    abc precedes abd in lexicographical order
    abd follows abc in lexicographical order
    abc compares equal to abc in lexicographical order
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.24.4.1 A função memcmp (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.24.4.1 A função memcmp (p: 266)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.24.4.1 A função memcmp (p: 365)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.21.4.1 A função memcmp (p: 328)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.11.4.1 A função memcmp

### Veja também

[ strcmp](<#/doc/string/byte/strcmp>) | compara duas strings
(função)
[ strncmp](<#/doc/string/byte/strncmp>) | compara uma certa quantidade de caracteres de duas strings
(função)
[Documentação C++](<#/>) para memcmp