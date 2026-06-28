# strcat, strcat_s

Definido no cabeçalho [`<string.h>`](<#/doc/string/byte>)

```c
char *strcat( char *dest, const char *src );  // até C99
char *strcat( char *restrict dest, const char *restrict src );  // desde C99
errno_t strcat_s(char *restrict dest, rsize_t destsz, const char *restrict src);  // desde C11
```

  
1) Anexa uma cópia da string de bytes terminada em nulo apontada por `src` ao final da string de bytes terminada em nulo apontada por `dest`. O caractere `src[0]` substitui o terminador nulo no final de `dest`. A string de bytes resultante é terminada em nulo.

O comportamento é indefinido se o array de destino não for grande o suficiente para o conteúdo de `src` e `dest` e o caractere nulo terminador. O comportamento é indefinido se as strings se sobrepuserem. O comportamento é indefinido se `dest` ou `src` não for um ponteiro para uma string de bytes terminada em nulo.

2) O mesmo que (1), exceto que pode sobrescrever o restante do array de destino (do último caractere escrito até `destsz`) com valores não especificados e que os seguintes erros são detectados em tempo de execução e chamam a função [manipulador de restrição](<#/doc/error/set_constraint_handler_s>) atualmente instalada: 

    

  * `src` ou `dest` é um ponteiro nulo 
  * `destsz` é zero ou maior que RSIZE_MAX
  * não há terminador nulo nos primeiros `destsz` bytes de `dest`
  * ocorreria truncamento (o espaço disponível no final de `dest` não seria suficiente para todos os caracteres, incluindo o terminador nulo, de `src`) 
  * ocorreria sobreposição entre as strings de origem e de destino

O comportamento é indefinido se o tamanho do array de caracteres apontado por `dest` < [strlen](<#/doc/string/byte/strlen>)(dest)+[strlen](<#/doc/string/byte/strlen>)(src)+1 <= `destsz`; em outras palavras, um valor errôneo de `destsz` não expõe o iminente estouro de buffer. 

    Assim como todas as funções com verificação de limites, `strcat_s` tem sua disponibilidade garantida apenas se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir [`<string.h>`](<#/doc/string/byte>).

### Parâmetros

dest  |  \-  |  ponteiro para a string de bytes terminada em nulo à qual anexar   
src  |  \-  |  ponteiro para a string de bytes terminada em nulo da qual copiar   
destsz  |  \-  |  número máximo de caracteres a serem escritos, tipicamente o tamanho do buffer de destino   
  
### Valor de retorno

1) retorna uma cópia de `dest`

2) retorna zero em caso de sucesso, retorna um valor diferente de zero em caso de erro. Além disso, em caso de erro, escreve zero em dest[0] (a menos que `dest` seja um ponteiro nulo ou `destsz` seja zero ou maior que RSIZE_MAX).

### Notas

Como `strcat` precisa procurar o final de `dest` em cada chamada, é ineficiente concatenar muitas strings em uma usando `strcat`. 

`strcat_s` tem permissão para sobrescrever o array de destino do último caractere escrito até `destsz` a fim de melhorar a eficiência: ele pode copiar em blocos multibyte e então verificar por bytes nulos. 

A função `strcat_s` é similar à [função BSD `strlcat`](<https://www.freebsd.org/cgi/man.cgi?query=strlcat&sektion=3>), exceto que 

  * `strlcat` trunca a string de origem para caber no destino 
  * `strlcat` não realiza todas as verificações em tempo de execução que `strcat_s` realiza 
  * `strlcat` não torna as falhas óbvias definindo o destino como uma string nula ou chamando um manipulador se a chamada falhar. 

Embora `strcat_s` proíba o truncamento devido a potenciais riscos de segurança, é possível truncar uma string usando [strncat_s](<#/doc/string/byte/strncat>) com verificação de limites. 

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
        strcat(str, " ...");
        strcat(str, " Goodbye World!");
        puts(str);
    
    #ifdef __STDC_LIB_EXT1__
        set_constraint_handler_s(ignore_handler_s);
        int r = strcat_s(str, sizeof str, " ... ");
        printf("str = \"%s\", r = %d\n", str, r);
        r = strcat_s(str, sizeof str, " and this is too much");
        printf("str = \"%s\", r = %d\n", str, r);
    #endif
    }
```

Saída possível: 
```
    Hello World! ... Goodbye World!
    str = "Hello World! ... Goodbye World! ... ", r = 0
    str = "", r = 22
```

### Referências

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.24.3.1 A função strcat (p: 364) 

    

  * K.3.7.2.1 A função strcat_s (p: 617-618) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.21.3.1 A função strcat (p: 327) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.11.3.1 A função strcat 

### Veja também

[ strncatstrncat_s](<#/doc/string/byte/strncat>)(C11) |  concatena uma certa quantidade de caracteres de duas strings   
(função)  
[ strcpystrcpy_s](<#/doc/string/byte/strcpy>)(C11) |  copia uma string para outra   
(função)  
[ memccpy](<#/doc/string/byte/memccpy>)(C23) |  copia um buffer para outro, parando após o delimitador especificado   
(função)  
[Documentação C++](<#/>) para strcat