# fdim, fdimf, fdiml

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float fdimf( float x, float y );  // desde C99
double fdim( double x, double y );  // desde C99
long double fdiml( long double x, long double y );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define fdim( x, y )  // desde C99
```

  
1-3) Retorna a diferença positiva entre x e y, ou seja, se x>y, retorna x-y, caso contrário (se x≤y), retorna +0.

4) Macro de tipo genérico: Se qualquer argumento tiver o tipo long double, `fdiml` é chamada. Caso contrário, se qualquer argumento tiver um tipo inteiro ou o tipo double, `fdim` é chamada. Caso contrário, `fdimf` é chamada.

### Parâmetros

x, y  |  \-  |  valor de ponto flutuante   
  
### Valor de retorno

Em caso de sucesso, retorna a diferença positiva entre x e y.

Se ocorrer um erro de intervalo devido a overflow, `+HUGE_VAL`, `+HUGE_VALF`, ou `+HUGE_VALL` é retornado.

Se ocorrer um erro de intervalo devido a underflow, o valor correto (após arredondamento) é retornado.

### Tratamento de erros

Os erros são reportados conforme especificado em [Template:rllpt](<https://en.cppreference.com/mwiki/index.php?title=Template:rllpt&action=edit&redlink=1> "Template:rllpt \(page does not exist\)").

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559),

  * Se qualquer um dos argumentos for NaN, NaN é retornado.

### Notas

Equivalente a [fmax](<#/doc/numeric/math/fmax>)(x-y, 0), exceto pelos requisitos de tratamento de NaN.

### Exemplo

Execute este código
```c
    #include <errno.h>
    #include <fenv.h>
    #include <math.h>
    #include <stdio.h>
    // #pragma STDC FENV_ACCESS ON
    
    int main(void)
    {
        printf("fdim(4, 1) = %f, fdim(1, 4)=%f\n", fdim(4,1), fdim(1,4));
        printf("fdim(4,-1) = %f, fdim(1,-4)=%f\n", fdim(4,-1), fdim(1,-4));
        //error handling
        errno = 0; feclearexcept(FE_ALL_EXCEPT);
        printf("fdim(1e308, -1e308) = %f\n", fdim(1e308, -1e308));
        if (errno == ERANGE)
            perror("    errno == ERANGE");
        if (fetestexcept(FE_OVERFLOW))
            puts("    FE_OVERFLOW raised");
    }
```

Saída possível:
```
    fdim(4, 1) = 3.000000, fdim(1, 4)=0.000000
    fdim(4,-1) = 5.000000, fdim(1,-4)=5.000000
    fdim(1e308, -1e308) = inf
        errno == ERANGE: Numerical result out of range
        FE_OVERFLOW raised
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.12.12.1 As funções fdim (p: TBD) 

    

  * 7.25 Matemática de tipo genérico <tgmath.h> (p: TBD) 

    

  * F.10.9.1 As funções fdim (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.12.12.1 As funções fdim (p: 187-188) 

    

  * 7.25 Matemática de tipo genérico <tgmath.h> (p: 272-273) 

    

  * F.10.9.1 As funções fdim (p: 386) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.12.12.1 As funções fdim (p: 257) 

    

  * 7.25 Matemática de tipo genérico <tgmath.h> (p: 373-375) 

    

  * F.10.9.1 As funções fdim (p: 530) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.12.12.1 As funções fdim (p: 238) 

    

  * 7.22 Matemática de tipo genérico <tgmath.h> (p: 335-337) 

    

  * F.9.9.1 As funções fdim (p: 466) 

### Ver também

[ abslabsllabs](<#/doc/numeric/math/abs>)(C99) |  calcula o valor absoluto de um valor inteiro (\\(\small{|x|}\\)|x|)   
(função)  
[ fmaxfmaxffmaxl](<#/doc/numeric/math/fmax>)(C99)(C99)(C99) |  determina o maior de dois valores de ponto flutuante   
(função)  
[Documentação C++](<#/>) para fdim