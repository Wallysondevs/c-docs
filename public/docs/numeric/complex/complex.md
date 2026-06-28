# complex

Definido no cabeçalho [`<complex.h>`](<#/doc/numeric/complex>)

```c
#define complex _Complex  // desde C99
```

  
Esta macro se expande para um especificador de tipo usado para identificar [tipos complexos](<#/doc/language/arithmetic_types>). 

Um programa pode indefinir e talvez redefinir a macro `complex`. 

### Exemplo

Execute este código
```c
    #include <complex.h>
    #include <math.h>
    #include <stdio.h>
     
    void print_complex(const char* note, complex z)
    {
        printf("%s %f%+f*i\n", note, creal(z), cimag(z));
    }
     
    int main(void)
    {
        double complex z = -1.0 + 2.0*I;
        print_complex("z  =", z);
        print_complex("z\u00B2 =", z * z);
        double complex z2 = ccos(2.0 * carg(z)) + csin(2.0 * carg(z))*I;
        print_complex("z\u00B2 =", cabs(z) * cabs(z) * z2);
    }
```

Saída: 
```
    z  = -1.000000+2.000000*i
    z² = -3.000000-4.000000*i
    z² = -3.000000-4.000000*i
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.3.1/4 complex (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.3.1/4 complex (p: 136) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.3.1/4 complex (p: 188) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.3.1/2 complex (p: 170) 

### Veja também

[ imaginary](<#/doc/numeric/complex/imaginary>)(C99) | macro de tipo imaginário   
(macro de palavra-chave)  