# abs, labs, llabs, imaxabs

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
int abs( int n );
long labs( long n );
long long llabs( long long n );  // desde C99
Definido no cabeçalho ``<inttypes.h>``
intmax_t imaxabs( intmax_t n );  // desde C99
```

Calcula o valor absoluto de um número inteiro. O comportamento é indefinido se o resultado não puder ser representado pelo tipo de retorno.

### Parâmetros

- **n** — valor inteiro

### Valor de retorno

O valor absoluto de n (ou seja, `|n|`), se for representável.

### Notas

Em sistemas de complemento de dois, o valor absoluto do valor mais negativo está fora do intervalo, por exemplo, para o tipo int de 32 bits em complemento de dois, [INT_MIN](<#/doc/types/limits>) é -2147483648, mas o resultado esperado 2147483648 é maior que [INT_MAX](<#/doc/types/limits>), que é 2147483647.

### Exemplo

Execute este código
```c
    #include <limits.h>
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(void)
    {
        printf("abs(+3) = %d\n", abs(+3));
        printf("abs(-3) = %d\n", abs(-3));
    
    //  printf("%+d\n", abs(INT_MIN)); // undefined behavior on 2's complement systems
    }
```

Saída:
```
    abs(+3) = 3
    abs(-3) = 3
```

### Referências

* Padrão C23 (ISO/IEC 9899:2024):

  * 7.8.2.1 A função imaxabs (p: TBD)

  * 7.22.6.1 As funções abs, labs e llabs (p: TBD)

* Padrão C17 (ISO/IEC 9899:2018):

  * 7.8.2.1 A função imaxabs (p: 159)

  * 7.22.6.1 As funções abs, labs e llabs (p: 259)

* Padrão C11 (ISO/IEC 9899:2011):

  * 7.8.2.1 A função imaxabs (p: 218)

  * 7.22.6.1 As funções abs, labs e llabs (p: 356)

* Padrão C99 (ISO/IEC 9899:1999):

  * 7.8.2.1 A função imaxabs (p: 199-200)

  * 7.20.6.1 As funções abs, labs e llabs (p: 320)

* Padrão C89/C90 (ISO/IEC 9899:1990):

  * 4.10.6.1 A função abs

  * 4.10.6.3 A função labs

### Veja também

[ fabsfabsffabsl](<#/doc/numeric/math/fabs>)(C99)(C99) | calcula o valor absoluto de um valor de ponto flutuante (\\(\small{|x|}\\)|x|)
(função)
[ cabscabsfcabsl](<#/doc/numeric/complex/cabs>)(C99)(C99)(C99) | calcula a magnitude de um número complexo
(função)
[Documentação C++](<#/>) para abs