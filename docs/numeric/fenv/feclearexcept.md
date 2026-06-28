# feclearexcept

Definido no cabeçalho [`<fenv.h>`](<#/doc/numeric/fenv>)

```c
int feclearexcept( int excepts );  // desde C99
```

Tenta limpar as exceções de ponto flutuante listadas no argumento de máscara de bits `excepts`, que é um OR bit a bit das [macros de exceção de ponto flutuante](<#/doc/numeric/fenv/FE_exceptions>).

### Parâmetros

- **excepts** — máscara de bits listando os sinalizadores de exceção a serem limpos

### Valor de retorno

`0` se todas as exceções indicadas foram limpas com sucesso ou se `excepts` for zero. Retorna um valor diferente de zero em caso de erro.

### Exemplo

Execute este código
```c
    #include <fenv.h>
    #include <stdio.h>
    #include <math.h>
    #include <float.h>
    
    /*
     * Uma possível implementação de hypot que faz uso de muitos recursos avançados
     * de ponto flutuante.
     */
    double hypot_demo(double a, double b) {
      const int range_problem = FE_OVERFLOW | FE_UNDERFLOW;
      feclearexcept(range_problem);
      // tenta um algoritmo rápido
      double result = sqrt(a * a + b * b);
      if (!fetestexcept(range_problem))  // sem estouro ou subfluxo
        return result;                   // retorna o resultado rápido
      // faz um cálculo mais complicado para evitar estouro ou subfluxo
      int a_exponent,b_exponent;
      frexp(a, &a_exponent);
      frexp(b, &b_exponent);
    
      if (a_exponent - b_exponent > DBL_MAX_EXP)
        return fabs(a) + fabs(b);        // podemos ignorar o valor menor
      // escala para que fabs(a) esteja perto de 1
      double a_scaled = scalbn(a, -a_exponent);
      double b_scaled = scalbn(b, -a_exponent);
      // estouro e subfluxo agora são impossíveis 
      result = sqrt(a_scaled * a_scaled + b_scaled * b_scaled);
      // desfaz a escala
      return scalbn(result, a_exponent);
    }
    
    int main(void)
    {
      // O caso normal segue o caminho rápido
      printf("hypot(%f, %f) = %f\n", 3.0, 4.0, hypot_demo(3.0, 4.0));
      // O caso extremo segue o caminho lento, mas mais preciso
      printf("hypot(%e, %e) = %e\n", DBL_MAX / 2.0, 
                                    DBL_MAX / 2.0, 
                                    hypot_demo(DBL_MAX / 2.0, DBL_MAX / 2.0));
    
      return 0;
    }
```

Output:
```
    hypot(3.000000, 4.000000) = 5.000000
    hypot(8.988466e+307, 8.988466e+307) = 1.271161e+308
```

### Referências

* Padrão C11 (ISO/IEC 9899:2011):

  * 7.6.2.1 A função feclearexcept (p: 209)

* Padrão C99 (ISO/IEC 9899:1999):

  * 7.6.2.1 A função feclearexcept (p: 190)

### Veja também

[ fetestexcept](<#/doc/numeric/fenv/fetestexcept>)(C99) | determina quais dos sinalizadores de status de ponto flutuante especificados estão definidos
(função)
[Documentação C++](<#/>) para feclearexcept