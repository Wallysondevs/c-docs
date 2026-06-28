# Números de erro

Cada uma das macros definidas em [`<errno.h>`](<#/doc/error>) se expande para uma expressão constante inteira do tipo int e com um valor positivo único. As seguintes constantes são definidas pelo ISO C. A implementação pode definir mais, desde que comecem com 'E' seguido por dígitos ou letras maiúsculas.

Definido no cabeçalho `[`<errno.h>`](<#/doc/error>)`
---
EDOM | Argumento matemático fora do domínio da função
(constante de macro)
EILSEQ(C95) | Sequência de bytes ilegal
(constante de macro)
ERANGE | Resultado muito grande
(constante de macro)

### Notas

Muitas constantes errno adicionais são [definidas pelo POSIX](<https://pubs.opengroup.org/onlinepubs/9699919799/basedefs/errno.h.html>) e pela [biblioteca padrão C++](<#/>), e implementações individuais podem definir ainda mais, por exemplo, errno(3) no Linux ou intro(2) no BSD e OS X.

### Exemplo

Execute este código
```c
    #include <errno.h>
    #include <math.h>
    #include <stdio.h>
    #include <string.h>
    
    int main(void)
    {
        errno = 0;
        printf("log(-1.0) = %f\n", log(-1.0));
        printf("%s\n\n", strerror(errno));
    
        errno = 0;
        printf("log(0.0)  = %f\n", log(0.0));
        printf("%s\n", strerror(errno));
    }
```

Saída possível:
```
    log(-1.0) = nan
    Numerical argument out of domain
    
    log(0.0)  = -inf
    Numerical result out of range
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.5/2 Erros <errno.h> (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.5/2 Erros <errno.h> (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.5/2 Erros <errno.h> (p: 205)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.5/2 Erros <errno.h> (p: 186)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.1.3 Erros <errno.h>

### Veja também

[ errno](<#/doc/error/errno>) | macro que se expande para uma variável de número de erro thread-local compatível com POSIX
(variável de macro)
[ perror](<#/doc/io/perror>) | exibe uma string de caracteres correspondente ao erro atual para [stderr](<#/doc/io/std_streams>)
(função)
[ strerrorstrerror_sstrerrorlen_s](<#/doc/string/byte/strerror>)(C11)(C11) | retorna uma versão textual de um dado código de erro
(função)
[Documentação C++](<#/>) para Números de erro