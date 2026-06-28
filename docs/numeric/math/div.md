# div, ldiv, lldiv, imaxdiv

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
div_t div( int x, int y );
ldiv_t ldiv( long x, long y );
lldiv_t lldiv( long long x, long long y );  // desde C99
Definido no cabeçalho ``<inttypes.h>``
imaxdiv_t imaxdiv( intmax_t x, intmax_t y );  // desde C99
```

  
Calcula tanto o quociente quanto o resto da divisão do numerador `x` pelo denominador `y`. 

Calcula o quociente e o resto simultaneamente. O quociente é o quociente algébrico com qualquer parte fracionária descartada (truncada em direção a zero). O resto é tal que quot * y + rem == x.  | (até C99)  
Calcula o quociente (o resultado da expressão x / y) e o resto (o resultado da expressão x % y) simultaneamente.  | (desde C99)  
  
### Parâmetros

x, y  |  \-  |  valores inteiros   
  
### Valor de retorno

Se tanto o resto quanto o quociente puderem ser representados como objetos do tipo correspondente (int, long, long long, [intmax_t](<#/doc/types/integer>), respectivamente), retorna ambos como um objeto do tipo `div_t`, `ldiv_t`, `lldiv_t`, `imaxdiv_t` definidos como segue: 

## div_t
```c
    struct div_t { int quot; int rem; };
```

ou 
```c
    struct div_t { int rem; int quot; };
```

## ldiv_t
```c
    struct ldiv_t { long quot; long rem; };
```

ou 
```c
    struct ldiv_t { long rem; long quot; };
```

## lldiv_t
```c
    struct lldiv_t { long long quot; long long rem; };
```

ou 
```c
    struct lldiv_t { long long rem; long long quot; };
```

## imaxdiv_t
```c
    struct imaxdiv_t { intmax_t quot; intmax_t rem; };
```

ou 
```c
    struct imaxdiv_t { intmax_t rem; intmax_t quot; };
```

Se o resto ou o quociente não puderem ser representados, o comportamento é indefinido. 

### Notas

Até C99, a direção de arredondamento do quociente e o sinal do resto nos operadores de divisão e resto embutidos eram definidos pela implementação se qualquer um dos operandos fosse negativo, mas eram bem definidos em `div` e `ldiv`. 

Em muitas plataformas, uma única instrução da CPU obtém tanto o quociente quanto o resto, e esta função pode aproveitar isso, embora os compiladores geralmente sejam capazes de mesclar operadores / e % próximos onde apropriado. 

### Exemplo

Execute este código
```c
    #include <assert.h>
    #include <limits.h>
    #include <math.h>
    #include <stdio.h>
    #include <stdlib.h>
    
    void reverse(char* first, char* last)
    {
        for (--last; first < last; ++first, --last)
        {
            char c = *last;
            *last = *first;
            *first = c;
        }
    }
    
    // returns empty buffer in case of buffer overflow
    char* itoa(int n, int base, char* buf, size_t buf_size)
    {
        assert(2 <= base && base <= 16 && buf && buf_size);
        div_t dv = {.quot = n};
        char* p = buf;
        do
        {
            if (!--buf_size)
                return (*buf = '\0'), buf;
            dv = div(dv.quot, base);
            *p++ = "0123456789abcdef"[abs(dv.rem)];
        }
        while(dv.quot);
        if (n < 0)
            *p++ = '-';
        *p = '\0';
        reverse(buf, p);
        return buf;
    }
    
    int main(void)
    {
        char buf[16];
        printf("%s\n", itoa(0, 2, buf, sizeof buf));
        printf("%s\n", itoa(007, 3, buf, sizeof buf));
        printf("%s\n", itoa(12346, 10, buf, sizeof buf));
        printf("%s\n", itoa(-12346, 10, buf, sizeof buf));
        printf("%s\n", itoa(-42, 2, buf, sizeof buf));
        printf("%s\n", itoa(INT_MAX, 16, buf, sizeof buf));
        printf("%s\n", itoa(INT_MIN, 16, buf, sizeof buf));
    }
```

Saída possível: 
```
    0
    21
    12346
    -12346
    -101010
    7fffffff
    -80000000
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.8.2.2 A função imaxdiv (p: TBD) 

    

  * 7.22.6.2 As funções div, ldiv e lldiv (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.8.2.2 A função imaxdiv (p: 159) 

    

  * 7.22.6.2 As funções div, ldiv e lldiv (p: 259) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.8.2.2 A função imaxdiv (p: 219) 

    

  * 7.22.6.2 As funções div, ldiv e lldiv (p: 356) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.8.2.2 A função imaxdiv (p: 200) 

    

  * 7.20.6.2 As funções div, ldiv e lldiv (p: 320) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.10 div_t, ldiv_t 

    

  * 4.10.6.2 A função div 

    

  * 4.10.6.4 A função ldiv 

### Veja também

[ fmodfmodffmodl](<#/doc/numeric/math/fmod>)(C99)(C99) |  calcula o resto da operação de divisão de ponto flutuante   
(função)  
[ remainderremainderfremainderl](<#/doc/numeric/math/remainder>)(C99)(C99)(C99) |  calcula o resto com sinal da operação de divisão de ponto flutuante   
(função)  
[ remquoremquofremquol](<#/doc/numeric/math/remquo>)(C99)(C99)(C99) |  calcula o resto com sinal, bem como os três últimos bits da operação de divisão   
(função)  
[Documentação C++](<#/>) para div  
  
### Links externos

1\.  | [Divisão euclidiana](<https://en.wikipedia.org/wiki/Euclidean_division> "enwiki:Euclidean division") — Da Wikipédia.   
2\.  | [Módulo (e divisão truncada)](<https://en.wikipedia.org/wiki/Modulo> "enwiki:Modulo") — Da Wikipédia.