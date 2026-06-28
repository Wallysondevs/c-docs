# remquo, remquof, remquol

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float remquof( float x, float y, int *quo );  // desde C99
double remquo( double x, double y, int *quo );  // desde C99
long double remquol( long double x, long double y, int *quo );  // desde C99
Definido no cabeçalho ``<tgmath.h>``
#define remquo( x, y, quo )  // desde C99
```

  
1-3) Calcula o resto de ponto flutuante da operação de divisão x/y como a função [remainder()](<#/doc/numeric/math/remainder>) faz. Adicionalmente, o sinal e pelo menos os três últimos bits de x/y serão armazenados em quo, o suficiente para determinar o octante do resultado dentro de um período.

4) Macro genérica de tipo: Se qualquer argumento não-ponteiro tiver o tipo long double, `remquol` é chamada. Caso contrário, se qualquer argumento não-ponteiro tiver um tipo inteiro ou o tipo double, `remquo` é chamada. Caso contrário, `remquof` é chamada.

### Parâmetros

x, y  |  \-  |  valores de ponto flutuante   
quo  |  \-  |  ponteiro para um valor inteiro para armazenar o sinal e alguns bits de x/y  
  
### Valor de retorno

Em caso de sucesso, retorna o resto de ponto flutuante da divisão x/y conforme definido em [remainder](<#/doc/numeric/math/remainder>), e armazena, em *quo, o sinal e pelo menos três dos bits menos significativos de x/y (formalmente, armazena um valor cujo sinal é o sinal de x/y e cuja magnitude é congruente módulo 2n  
à magnitude do quociente inteiro de x/y, onde n é um inteiro definido pela implementação maior ou igual a 3). 

Se y for zero, o valor armazenado em *quo é não especificado. 

Se ocorrer um erro de domínio, um valor definido pela implementação é retornado (NaN onde suportado). 

Se ocorrer um erro de faixa devido a underflow, o resultado correto é retornado se subnormais forem suportados. 

Se y for zero, mas o erro de domínio não ocorrer, zero é retornado. 

### Tratamento de erros

Erros são reportados conforme especificado em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>). 

Erro de domínio pode ocorrer se y for zero. 

Se a implementação suporta aritmética de ponto flutuante IEEE (IEC 60559), 

  * O [modo de arredondamento](<#/doc/numeric/fenv/FE_round>) atual não tem efeito. 
  * [FE_INEXACT](<#/doc/numeric/fenv/FE_exceptions>) nunca é levantado 
  * Se x for ±∞ e y não for NaN, NaN é retornado e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado 
  * Se y for ±0 e x não for NaN, NaN é retornado e [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado 
  * Se x ou y for NaN, NaN é retornado 

### Notas

[POSIX exige](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/remquo.html>) que um erro de domínio ocorra se x for infinito ou y for zero. 

Esta função é útil ao implementar funções periódicas com o período exatamente representável como um valor de ponto flutuante: ao calcular sin(πx) para um x muito grande, chamar [sin](<#/doc/numeric/math/sin>) diretamente pode resultar em um grande erro, mas se o argumento da função for primeiro reduzido com `remquo`, os bits de baixa ordem do quociente podem ser usados para determinar o sinal e o octante do resultado dentro do período, enquanto o resto pode ser usado para calcular o valor com alta precisão. 

Em algumas plataformas, esta operação é suportada por hardware (e, por exemplo, em CPUs Intel, `FPREM1` deixa exatamente 3 bits de precisão no quociente). 

### Exemplo

Run this code
```c
    #include <fenv.h>
    #include <math.h>
    #include <stdio.h>
     
    #ifndef __GNUC__
    #pragma STDC FENV_ACCESS ON
    #endif
     
    double cos_pi_x_naive(double x)
    {
        const double pi = acos(-1);
        return cos(pi * x);
    }
     
    // the period is 2, values are (0;0.5) positive, (0.5;1.5) negative, (1.5,2) positive
    double cos_pi_x_smart(double x)
    {
        const double pi = acos(-1);
        int extremum;
        double rem = remquo(x, 1, &extremum);
        extremum = (unsigned)extremum % 2; // keep 1 bit to determine nearest extremum
        return extremum ? -cos(pi * rem) : cos(pi * rem);
    }
     
    int main(void)
    {
        printf("cos(pi * 0.25) = %f\n", cos_pi_x_naive(0.25));
        printf("cos(pi * 1.25) = %f\n", cos_pi_x_naive(1.25));
        printf("cos(pi * 1000000000000.25) = %f\n", cos_pi_x_naive(1000000000000.25));
        printf("cos(pi * 1000000000001.25) = %f\n", cos_pi_x_naive(1000000000001.25));
        printf("cos(pi * 1000000000000.25) = %f\n", cos_pi_x_smart(1000000000000.25));
        printf("cos(pi * 1000000000001.25) = %f\n", cos_pi_x_smart(1000000000001.25));
     
        // error handling
        feclearexcept(FE_ALL_EXCEPT);
        int quo;
        printf("remquo(+Inf, 1) = %.1f\n", remquo(INFINITY, 1, &quo));
        if (fetestexcept(FE_INVALID))
            puts("    FE_INVALID raised");
    }
```

Saída possível: 
```
    cos(pi * 0.25) = 0.707107
    cos(pi * 1.25) = -0.707107
    cos(pi * 1000000000000.25) = 0.707123
    cos(pi * 1000000000001.25) = -0.707117
    cos(pi * 1000000000000.25) = 0.707107
    cos(pi * 1000000000001.25) = -0.707107 
    remquo(+Inf, 1) = -nan
        FE_INVALID raised
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.12.10.3 As funções remquo (p: TBD) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: TBD) 

    

  * F.10.7.3 As funções remquo (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.12.10.3 As funções remquo (p: 186) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 272-273) 

    

  * F.10.7.3 As funções remquo (p: 385) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.12.10.3 As funções remquo (p: 255) 

    

  * 7.25 Matemática genérica de tipo <tgmath.h> (p: 373-375) 

    

  * F.10.7.3 As funções remquo (p: 529) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.12.10.3 As funções remquo (p: 236) 

    

  * 7.22 Matemática genérica de tipo <tgmath.h> (p: 335-337) 

    

  * F.9.7.3 As funções remquo (p: 465) 

### Veja também

[ divldivlldiv](<#/doc/numeric/math/div>)(C99) |  calcula quociente e resto de divisão inteira   
(função)  
[ fmodfmodffmodl](<#/doc/numeric/math/fmod>)(C99)(C99) |  calcula o resto da operação de divisão de ponto flutuante   
(função)  
[ remainderremainderfremainderl](<#/doc/numeric/math/remainder>)(C99)(C99)(C99) |  calcula o resto com sinal da operação de divisão de ponto flutuante   
(função)  
[Documentação C++](<#/>) para remquo