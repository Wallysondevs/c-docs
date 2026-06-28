# nan, nanf, nanl, nand32, nand64, nand128

Definido no cabeçalho [`<math.h>`](<#/doc/numeric/math>)

```c
float nanf( const char* arg );  // desde C99
double nan( const char* arg );  // desde C99
long double nanl( const char* arg );  // desde C99
_Decimal32 nand32( const char* arg );  // desde C23
_Decimal64 nand64( const char* arg );  // desde C23
_Decimal128 nand128( const char* arg );  // desde C23
```

  
Converte a string de caracteres `arg` definida pela implementação no valor NaN silencioso correspondente, como se chamasse a função de análise apropriada `_strtoX_`, da seguinte forma: 

  * A chamada nan("n-char-sequence"), onde n-char-sequence é uma sequência de dígitos, letras latinas e underscores, é equivalente à chamada /*strtoX*/("NAN(n-char-sequence)", (char**)[NULL](<#/doc/types/NULL>));. 
  * A chamada nan("") é equivalente à chamada /*strtoX*/("NAN()", (char**)[NULL](<#/doc/types/NULL>));. 
  * A chamada nan("string"), onde string não é nem uma n-char-sequence nem uma string vazia, é equivalente à chamada /*strtoX*/("NAN", (char**)[NULL](<#/doc/types/NULL>));. 

1) A função de análise é [strtof](<#/doc/string/byte/strtof>).

2) A função de análise é [strtod](<#/doc/string/byte/strtof>).

3) A função de análise é [strtold](<#/doc/string/byte/strtof>).

4) A função de análise é strtod32.

5) A função de análise é strtod64.

6) A função de análise é strtod128.

As funções que retornam valores de ponto flutuante decimal são declaradas se e somente se a implementação predefinir `__STDC_IEC_60559_DFP__` (ou seja, a implementação suporta números de ponto flutuante decimais). | (desde C23)  
  
### Parâmetros

arg  |  \-  |  string de caracteres estreitos que identifica o conteúdo de um NaN   
  
### Valor de retorno

O valor NaN silencioso que corresponde à string de identificação `arg` ou zero se a implementação não suportar NaNs silenciosos. 

Se a implementação suportar aritmética de ponto flutuante IEEE (IEC 60559), ela também suportará NaNs silenciosos. 

### Tratamento de erros

Esta função não está sujeita a nenhuma das condições de erro especificadas em [`math_errhandling`](<#/doc/numeric/math/math_errhandling>). 

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <math.h>
    #include <stdint.h>
    #include <inttypes.h>
    #include <string.h>
    
    int main(void)
    {
        double f1 = nan("1");
        uint64_t f1n; memcpy(&f1n, &f1, sizeof f1);
        printf("nan(\"1\")   = %f (%" PRIx64 ")\n", f1, f1n);
    
        double f2 = nan("2");
        uint64_t f2n; memcpy(&f2n, &f2, sizeof f2);
        printf("nan(\"2\")   = %f (%" PRIx64 ")\n", f2, f2n);
    
        double f3 = nan("0xF");
        uint64_t f3n; memcpy(&f3n, &f3, sizeof f3);
        printf("nan(\"0xF\") = %f (%" PRIx64 ")\n", f3, f3n);
    }
```

Saída possível: 
```
    nan("1")   = nan (7ff8000000000001)
    nan("2")   = nan (7ff8000000000002)
    nan("0xF") = nan (7ff800000000000f)
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.12.11.2 As funções nan (p: 186-187) 

    

  * F.10.8.2 As funções nan (p: 386) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.12.11.2 As funções nan (p: 256) 

    

  * F.10.8.2 As funções nan (p: 529) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.12.11.2 As funções nan (p: 237) 

    

  * F.9.8.2 As funções fabs (p: 465) 

### Veja também

[ isnan](<#/doc/numeric/math/isnan>)(C99) | verifica se o número dado é NaN   
(macro de função)  
[ NAN](<#/doc/numeric/math/NAN>)(C99) | avalia para um NaN silencioso do tipo float   
(constante macro)  
[Documentação C++](<#/>) para nanf, nan, nanl