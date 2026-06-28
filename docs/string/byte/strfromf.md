# strfromf, strfromd, strfroml

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
int strfromf( char* restrict s, size_t n, const char* restrict format, float fp );  // desde C23
int strfromd( char* restrict s, size_t n, const char* restrict format, double fp );  // desde C23
int strfroml( char* restrict s, size_t n, const char* restrict format, long double fp );  // desde C23
```

  
Converte um valor de ponto flutuante para uma string de bytes.

As funções são equivalentes a [snprintf](<#/doc/io/fprintf>)(s, n, format, fp), exceto que a string de formato deve conter apenas o caractere %, uma precisão opcional que não contém um asterisco *, e um dos especificadores de conversão `a`, `A`, `e`, `E`, `f`, `F`, `g`, ou `G`, que se aplica ao tipo double, float, ou long double) indicado pelo sufixo da função (em vez de por um modificador de comprimento). O uso dessas funções com qualquer outra string de formato resulta em comportamento indefinido.

### Parâmetros

s  |  \-  |  ponteiro para uma string de caracteres para escrever   
n  |  \-  |  até n - 1 caracteres podem ser escritos, mais o terminador nulo   
format  |  \-  |  ponteiro para uma string de bytes terminada em nulo especificando como interpretar os dados   
fp  |  \-  |  valor de ponto flutuante a ser convertido   
  
### Valor de retorno

O número de caracteres que teriam sido escritos se n fosse suficientemente grande, sem contar o caractere nulo de terminação. Assim, a saída terminada em nulo foi completamente escrita se e somente se o valor retornado for não negativo e menor que n.

### Exemplo

Run this code
```c
    #include <stdio.h>
    #include <stdlib.h>
    
    int main()
    {
        char buffer[32];
        int written;
        const char* format[] = {"%a", "%A", "%e", "%E", "%f", "%F", "%g", "%G"};
    
        for (size_t fmt = 0; fmt != sizeof format / sizeof format[0]; ++fmt)
        {
            written = strfromf(buffer, sizeof buffer, format[fmt], 3.1415f);
            printf("strfromf(... %s ...) = %2i, buffer: \"%s\"\n",
                   format[fmt], written, buffer);
        }
        puts("");
    
        for (size_t fmt = 0; fmt != sizeof format / sizeof format[0]; ++fmt)
        {
            written = strfromd(buffer, sizeof buffer, format[fmt], 3.1415);
            printf("strfromd(... %s ...) = %2i, buffer: \"%s\"\n",
                   format[fmt], written, buffer);
        }
        puts("");
    
        for (size_t fmt = 0; fmt != sizeof format / sizeof format[0]; ++fmt)
        {
            written = strfroml(buffer, sizeof buffer, format[fmt], 3.1415);
            printf("strfroml(... %s ...) = %2i, buffer: \"%s\"\n",
                   format[fmt], written, buffer);
        }
    }
```

Output: 
```
    strfromf(... %a ...) = 13, buffer: "0x1.921cacp+1"
    strfromf(... %A ...) = 13, buffer: "0X1.921CACP+1"
    strfromf(... %e ...) = 12, buffer: "3.141500e+00"
    strfromf(... %E ...) = 12, buffer: "3.141500E+00"
    strfromf(... %f ...) =  8, buffer: "3.141500"
    strfromf(... %F ...) =  8, buffer: "3.141500"
    strfromf(... %g ...) =  6, buffer: "3.1415"
    strfromf(... %G ...) =  6, buffer: "3.1415"
    
    strfromd(... %a ...) = 20, buffer: "0x1.921cac083126fp+1"
    strfromd(... %A ...) = 20, buffer: "0X1.921CAC083126FP+1"
    strfromd(... %e ...) = 12, buffer: "3.141500e+00"
    strfromd(... %E ...) = 12, buffer: "3.141500E+00"
    strfromd(... %f ...) =  8, buffer: "3.141500"
    strfromd(... %F ...) =  8, buffer: "3.141500"
    strfromd(... %g ...) =  6, buffer: "3.1415"
    strfromd(... %G ...) =  6, buffer: "3.1415"
    
    strfroml(... %a ...) = 20, buffer: "0xc.90e5604189378p-2"
    strfroml(... %A ...) = 20, buffer: "0XC.90E5604189378P-2"
    strfroml(... %e ...) = 12, buffer: "3.141500e+00"
    strfroml(... %E ...) = 12, buffer: "3.141500E+00"
    strfroml(... %f ...) =  8, buffer: "3.141500"
    strfroml(... %F ...) =  8, buffer: "3.141500"
    strfroml(... %g ...) =  6, buffer: "3.1415"
    strfroml(... %G ...) =  6, buffer: "3.1415"
```

### Referência

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.24.1.3 As funções strfromd, strfromf e strfroml 

### Veja também

[ printffprintfsprintfsnprintfprintf_sfprintf_ssprintf_ssnprintf_s](<#/doc/io/fprintf>)(C99)(C11)(C11)(C11)(C11) | imprime saída formatada para [stdout](<#/doc/io/std_streams>), um fluxo de arquivo ou um buffer   
(função)  
[ strtofstrtodstrtold](<#/doc/string/byte/strtof>)(C99)(C99) | converte uma string de bytes para um valor de ponto flutuante   
(função)