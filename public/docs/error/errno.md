# errno

Definido no cabeçalho [`<errno.h>`](<#/doc/error>)

```c
#define errno /* implementation-defined */
```

`errno` é uma macro de pré-processador (mas veja a nota abaixo) que se expande para um lvalue modificável do tipo `int`, local à thread (desde C11). Várias funções da biblioteca padrão indicam erros escrevendo inteiros positivos em `errno`. Tipicamente, o valor de `errno` é definido para um dos códigos de erro listados em [`<errno.h>`](<#/doc/error>) como constantes de macro começando com a letra `E` seguida por letras maiúsculas ou dígitos.

O valor de `errno` é ​0​ na inicialização do programa, e embora as funções da biblioteca possam escrever inteiros positivos em `errno` independentemente de um erro ter ocorrido ou não, as funções da biblioteca nunca armazenam ​0​ em `errno`.

As funções da biblioteca [perror](<#/doc/io/perror>) e [strerror](<#/doc/string/byte/strerror>) podem ser usadas para obter descrições textuais das condições de erro que correspondem ao valor atual de `errno`.

Nota: Até C11, os padrões C tinham requisitos contraditórios, pois afirmavam que `errno` é uma macro, mas _também_ que "é não especificado se `errno` é uma macro ou um identificador declarado com ligação externa". C11 corrige isso, exigindo que seja definida como uma macro (veja também WG14 [N1338](<https://open-std.org/JTC1/SC22/WG14/www/docs/n1338.htm>)).

### Exemplo

Execute este código
```c
    #include <errno.h>
    #include <math.h>
    #include <stdio.h>
    
    void show_errno(void)
    {
        const char *err_info = "unknown error";
        switch (errno)
        {
            case EDOM:
                err_info = "domain error";
                break;
            case EILSEQ:
                err_info = "illegal sequence";
                break;
            case ERANGE:
                err_info = "pole or range error";
                break;
            case 0:
                err_info = "no error";
        }
        fputs(err_info, stdout);
        puts(" occurred");
    }
    
    int main(void)
    {
        fputs("MATH_ERRNO is ", stdout);
        puts(math_errhandling & MATH_ERRNO ? "set" : "not set");
    
        errno = 0;
        (void)(1.0 / 0.0);
        show_errno();
    
        errno = 0;
        (void)acos(+1.1);
        show_errno();
    
        errno = 0;
        (void)log(0.0);
        show_errno();
    
        errno = 0;
        (void)sin(0.0);
        show_errno();
    }
```

Saída possível:
```
    MATH_ERRNO is set
    no error occurred
    domain error occurred
    pole or range error occurred
    no error occurred
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.5 Erros <errno.h> (p: TBD)

    

  * K.3.1.3 Uso de errno (p: TBD)

    

  * K.3.2 Erros <errno.h> (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.5 Erros <errno.h> (p: TBD)

    

  * K.3.1.3 Uso de errno (p: TBD)

    

  * K.3.2 Erros <errno.h> (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.5 Erros <errno.h> (p: 205)

    

  * K.3.1.3 Uso de errno (p: 584)

    

  * K.3.2 Erros <errno.h> (p: 585)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.5 Erros <errno.h> (p: 186)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.1.3 Erros <errno.h>

### Veja também

[ E2BIG, EACCES, ..., EXDEV](<#/doc/error/errno_macros>) | macros para condições de erro padrão compatíveis com POSIX
(constante de macro)
[ perror](<#/doc/io/perror>) | exibe uma string de caracteres correspondente ao erro atual em [stderr](<#/doc/io/std_streams>)
(função)
[ strerrorstrerror_sstrerrorlen_s](<#/doc/string/byte/strerror>)(C11)(C11) | retorna uma versão textual de um dado código de erro
(função)
[ math_errhandlingMATH_ERRNOMATH_ERREXCEPT](<#/doc/numeric/math/math_errhandling>)(C99)(C99)(C99) | define o mecanismo de tratamento de erros usado pelas funções matemáticas comuns
(constante de macro)
[Documentação C++](<#/>) para errno