# memccpy

Definido no cabeçalho [`<string.h>`](<#/doc/string/byte>)

```c
void* memccpy( void* restrict dest, const void* restrict src, int c, size_t count );  // desde C23
```

Copia bytes do objeto apontado por src para o objeto apontado por dest, parando após _qualquer_ das duas condições seguintes ser satisfeita:

*   count bytes são copiados
*   o byte (unsigned char)c é encontrado (e copiado).

Os objetos src e dest são interpretados como arrays de unsigned char.

O comportamento é indefinido se _qualquer_ condição for atendida:

*   o acesso ocorre além do final do array dest;
*   os objetos se sobrepõem (o que é uma violação do contrato [`restrict`](<#/doc/language/restrict>))
*   dest ou src é um ponteiro inválido ou nulo

### Parâmetros

- **dest** — ponteiro para o objeto para o qual copiar
- **src** — ponteiro para o objeto do qual copiar
- **c** — byte de terminação, convertido para unsigned char inicialmente
- **count** — número de bytes a copiar

### Valor de retorno

Se o byte (unsigned char)c foi encontrado, `memccpy` retorna um ponteiro para o próximo byte em dest após (unsigned char)c. Caso contrário, retorna um ponteiro nulo.

### Observações

A função é idêntica à [POSIX `memccpy`](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/memccpy.html>).

memccpy(dest, src, 0, count) se comporta de forma similar a [strncpy](<#/doc/string/byte/strncpy>)(dest, src, count), exceto que a primeira retorna um ponteiro para o _final_ do buffer escrito, e não preenche com zeros o array de destino. Assim, `memccpy` é útil para concatenar eficientemente múltiplas strings.
```c
    char bigString[1000];
    char* end = bigString + sizeof bigString;
    
    char* p = memccpy(bigString, "John, ", '\0', sizeof bigString - 1);
    if (p)
        p = memccpy(p - 1, "Paul, ", '\0', end - p);
    if (p)
        p = memccpy(p - 1, "George, ", '\0', end - p);
    if (p)
        p = memccpy(p - 1, "Joel ", '\0', end - p);
    if (!p)
        end[-1] = '\0';
    
    puts(bigString); // John, Paul, George, Joel
```

### Exemplo

Execute este código
```c
    #include <ctype.h>
    #include <stdio.h>
    #include <string.h>
    
    int main(void)
    {
        const char src[] = "Stars: Altair, Sun, Vega.";
        const char terminal[] = {':', ' ', ',', '.', '!'};
        char dest[sizeof src];
        const char alt = '@';
    
        for (size_t i = 0; i != sizeof terminal; ++i)
        {
            void* to = memccpy(dest, src, terminal[i], sizeof dest);
    
            printf("Terminal '%c' (%s):\t\"", terminal[i], to ? "found" : "absent");
    
            // if `terminal` character was not found - print the whole `dest`
            to = to ? to : dest + sizeof dest;
    
            for (char* from = dest; from != to; ++from)
                putchar(isprint(*from) ? *from : alt);
    
            puts("\"");
        }
    
    
        puts("\n" "Separate star names from distances (ly):");
        const char *star_distance[] = {
            "Arcturus : 37", "Vega : 25", "Capella : 43", "Rigel : 860", "Procyon : 11"
        };
        char names_only[64];
        char *first = names_only;
        char *last = names_only + sizeof names_only;
    
        for (size_t t = 0; t != (sizeof star_distance) / (sizeof star_distance[0]); ++t)
        {
            if (first)
                first = memccpy(first, star_distance[t], ' ', last - first);
            else
                break;
        }
    
        if (first)
        {
            *first = '\0';
            puts(names_only);
        }
        else
            puts("Buffer is too small.");
    }
```

Saída:
```
    Terminal ':' (found):   "Stars:"
    Terminal ' ' (found):   "Stars: "
    Terminal ',' (found):   "Stars: Altair,"
    Terminal '.' (found):   "Stars: Altair, Sun, Vega."
    Terminal '!' (absent):  "Stars: Altair, Sun, Vega.@"
    
    Separate star names from distances (ly):
    Arcturus Vega Capella Rigel Procyon
```

### Veja também

[ memcpymemcpy_s](<#/doc/string/byte/memcpy>)(C11) | copia um buffer para outro
(função)
[ wmemcpywmemcpy_s](<#/doc/string/wide/wmemcpy>)(C95)(C11) | copia uma certa quantidade de caracteres largos entre dois arrays não sobrepostos
(função)
[ memmovememmove_s](<#/doc/string/byte/memmove>)(C11) | move um buffer para outro
(função)
[ strcpystrcpy_s](<#/doc/string/byte/strcpy>)(C11) | copia uma string para outra
(função)
[ strcatstrcat_s](<#/doc/string/byte/strcat>)(C11) | concatena duas strings
(função)