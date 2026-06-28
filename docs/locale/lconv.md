# lconv

Definido no cabeçalho [`<locale.h>`](<#/doc/locale>)

```c
struct lconv;
```

A struct `lconv` contém regras de formatação numérica e monetária conforme definidas por uma localidade C. Objetos desta struct podem ser obtidos com [localeconv](<#/doc/locale/localeconv>). Os membros de `lconv` são valores do tipo char e do tipo char*. Cada membro char*, exceto `decimal_point`, pode estar apontando para um caractere nulo (ou seja, para uma string C vazia). Os membros do tipo char são todos números não negativos, qualquer um dos quais pode ser [CHAR_MAX](<#/doc/types/limits>) se o valor correspondente não estiver disponível na localidade C atual.

### Membros

#### Parâmetros de formatação numérica não monetária

char* decimal_point | o caractere usado como separador decimal
(membro público)
char* thousands_sep | o caractere usado para separar grupos de dígitos antes do separador decimal
(membro público)
char* grouping | uma string cujos elementos indicam os tamanhos dos grupos de dígitos
(membro público)

#### Parâmetros de formatação numérica monetária

char* mon_decimal_point | o caractere usado como separador decimal
(membro público)
char* mon_thousands_sep | o caractere usado para separar grupos de dígitos antes do separador decimal
(membro público)
char* mon_grouping | uma string cujos elementos indicam os tamanhos dos grupos de dígitos
(membro público)
char* positive_sign | uma string usada para indicar quantidade monetária não negativa
(membro público)
char* negative_sign | uma string usada para indicar quantidade monetária negativa
(membro público)

#### Parâmetros de formatação numérica monetária local

char* currency_symbol | o símbolo usado para a moeda na localidade C atual
(membro público)
char frac_digits | o número de dígitos após o separador decimal a serem exibidos em uma quantidade monetária
(membro público)
char p_cs_precedes | 1 se currency_symbol for colocado antes do valor não negativo, ​0​ se depois
(membro público)
char n_cs_precedes | 1 se currency_symbol for colocado antes do valor negativo, ​0​ se depois
(membro público)
char p_sep_by_space | indica a separação de currency_symbol, positive_sign e o valor monetário não negativo
(membro público)
char n_sep_by_space | indica a separação de currency_symbol, negative_sign e o valor monetário negativo
(membro público)
char p_sign_posn | indica a posição de positive_sign em um valor monetário não negativo
(membro público)
char n_sign_posn | indica a posição de negative_sign em um valor monetário negativo
(membro público)

#### Parâmetros de formatação numérica monetária internacional

char* int_curr_symbol | a string usada como nome da moeda internacional na localidade C atual
(membro público)
char int_frac_digits | o número de dígitos após o separador decimal a serem exibidos em uma quantidade monetária internacional
(membro público)
char int_p_cs_precedes(C99) | 1 se int_curr_symbol for colocado antes do valor monetário internacional não negativo, ​0​ se depois
(membro público)
char int_n_cs_precedes(C99) | 1 se int_curr_symbol for colocado antes do valor monetário internacional negativo, ​0​ se depois
(membro público)
char int_p_sep_by_space(C99) | indica a separação de int_curr_symbol, positive_sign e o valor monetário internacional não negativo
(membro público)
char int_n_sep_by_space(C99) | indica a separação de int_curr_symbol, negative_sign e o valor monetário internacional negativo
(membro público)
char int_p_sign_posn(C99) | indica a posição de positive_sign em um valor monetário internacional não negativo
(membro público)
char int_n_sign_posn(C99) | indica a posição de negative_sign em um valor monetário internacional negativo
(membro público)

Os caracteres das strings C apontadas por grouping e mon_grouping são interpretados de acordo com seus valores numéricos. Quando o '\0' terminador é encontrado, o último valor visto é assumido como repetindo-se para o restante dos dígitos. Se [CHAR_MAX](<#/doc/types/limits>) for encontrado, nenhum dígito adicional é agrupado. O agrupamento típico de três dígitos por vez é "\003".

Os valores de p_sep_by_space, n_sep_by_space, int_p_sep_by_space, int_n_sep_by_space são interpretados da seguinte forma:

​0​ | nenhum espaço separa o símbolo da moeda e o valor
1 | o sinal adere ao símbolo da moeda, o valor é separado por um espaço
2 | o sinal adere ao valor. O símbolo da moeda é separado por um espaço

Os valores de p_sign_posn, n_sign_posn, int_p_sign_posn, int_n_sign_posn são interpretados da seguinte forma:

​0​ | parênteses ao redor do valor e do símbolo da moeda são usados para representar o sinal
1 | sinal antes do valor e do símbolo da moeda
2 | sinal depois do valor e do símbolo da moeda
3 | sinal antes do símbolo da moeda
4 | sinal depois do símbolo da moeda

### Exemplo

Execute este código
```c
    #include <locale.h>
    #include <stdio.h>
    
    int main(void)
    {
        setlocale(LC_ALL, "ja_JP.UTF-8");
        struct lconv* lc = localeconv();
        printf("Japanese currency symbol: %s(%s)\n", lc->currency_symbol, lc->int_curr_symbol);
    }
```

Saída possível:
```
    Japanese currency symbol: ￥(JPY )
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.11/2 Localização <locale.h> (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.11/2 Localização <locale.h> (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.11/2 Localização <locale.h> (p: 223)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.11/2 Localização <locale.h> (p: 204)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.4 LOCALIZAÇÃO <locale.h>

### Veja também

[ localeconv](<#/doc/locale/localeconv>) | consulta detalhes de formatação numérica e monetária da localidade atual
(função)
[Documentação C++](<#/>) para lconv