# fegetround, fesetround

Definido no cabeçalho [`<fenv.h>`](<#/doc/numeric/fenv>)

```c
int fesetround( int round );  // desde C99
int fegetround();  // desde C99
```

1) Tenta estabelecer a direção de arredondamento de ponto flutuante igual ao argumento [round](<#/doc/numeric/math/round>), que se espera ser uma das [macros de arredondamento de ponto flutuante](<#/doc/numeric/fenv/FE_round>).

2) Retorna o valor da [macro de arredondamento de ponto flutuante](<#/doc/numeric/fenv/FE_round>) que corresponde à direção de arredondamento atual.

### Parâmetros

- **round** — direção de arredondamento, uma das [macros de arredondamento de ponto flutuante](<#/doc/numeric/fenv/FE_round>)

### Valor de retorno

1) ​0​ em caso de sucesso, diferente de zero caso contrário.

2) a [macro de arredondamento de ponto flutuante](<#/doc/numeric/fenv/FE_round>) que descreve a direção de arredondamento atual ou um valor negativo se a direção não puder ser determinada.

### Observações

O modo de arredondamento atual, refletindo os efeitos do `fesetround` mais recente, também pode ser consultado com [FLT_ROUNDS](<#/doc/types/limits/FLT_ROUNDS>).

### Exemplo

Execute este código
```c
    #include <fenv.h>
    #include <math.h>
    #include <stdio.h>
     
    // #pragma STDC FENV_ACCESS ON
     
    void show_fe_current_rounding_direction(void)
    {
        printf("current rounding direction:  ");
        switch (fegetround())
        {
               case FE_TONEAREST:  printf ("FE_TONEAREST");  break;
               case FE_DOWNWARD:   printf ("FE_DOWNWARD");   break;
               case FE_UPWARD:     printf ("FE_UPWARD");     break;
               case FE_TOWARDZERO: printf ("FE_TOWARDZERO"); break;
               default:            printf ("unknown");
        };
        printf("\n");
    }
     
    int main(void)
    {
        /* Direção de arredondamento padrão */
        show_fe_current_rounding_direction();
        printf("+11.5 -> %+4.1f\n", rint(+11.5)); /* no meio entre dois inteiros */
        printf("+12.5 -> %+4.1f\n", rint(+12.5)); /* no meio entre dois inteiros */
     
        /* Salva a direção de arredondamento atual. */
        int curr_direction = fegetround();
     
        /* Altera temporariamente a direção de arredondamento atual. */
        fesetround(FE_DOWNWARD);
        show_fe_current_rounding_direction();
        printf("+11.5 -> %+4.1f\n", rint(+11.5));
        printf("+12.5 -> %+4.1f\n", rint(+12.5));
     
        /* Restaura a direção de arredondamento padrão. */
        fesetround(curr_direction);
        show_fe_current_rounding_direction();
     
        return 0;
    }
```

Saída possível:
```
    current rounding direction:  FE_TONEAREST
    +11.5 -> +12.0
    +12.5 -> +12.0
    current rounding direction:  FE_DOWNWARD
    +11.5 -> +11.0
    +12.5 -> +12.0
    current rounding direction:  FE_TONEAREST
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.6.3.1 A função fegetround (p: TBD)

    

  * 7.6.3.2 A função fesetround (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.6.3.1 A função fegetround (p: TBD)

    

  * 7.6.3.2 A função fesetround (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.6.3.1 A função fegetround (p: 212)

    

  * 7.6.3.2 A função fesetround (p: 212-213)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.6.3.1 A função fegetround (p: 193)

    

  * 7.6.3.2 A função fesetround (p: 193-194)

### Veja também

[ nearbyintnearbyintfnearbyintl](<#/doc/numeric/math/nearbyint>)(C99)(C99)(C99) | arredonda para um inteiro usando o modo de arredondamento atual
(função)
[ rintrintfrintllrintlrintflrintlllrintllrintfllrintl](<#/doc/numeric/math/rint>)(C99)(C99)(C99)(C99)(C99)(C99)(C99)(C99)(C99) | arredonda para um inteiro usando o modo de arredondamento atual com exceção se o resultado for diferente
(função)
[Documentação C++](<#/>) para fegetround, fesetround