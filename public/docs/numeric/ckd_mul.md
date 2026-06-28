# ckd_mul

Definido no cabeçalho [`<stdckdint.h>`](<#/doc/numeric>)

```c
#define ckd_mul( result, a, b ) /* implementation-defined */
// interface exposta:
bool ckd_mul( type1* result, type2 a, type3 b );  // desde C23
```

Calcula a multiplicação x × y e armazena o resultado em *result. A multiplicação é realizada como se ambos os operandos fossem representados em um tipo inteiro assinado com faixa infinita, e o resultado fosse então convertido desse tipo inteiro para type1. Se o valor atribuído a *result representar corretamente o resultado matemático da operação, ele retorna false. Caso contrário, ele retorna true. Neste caso, o valor atribuído a *result é o resultado matemático da operação com *wrap-around* para a largura de *result.

### Parâmetros

- **a, b** — valores inteiros
- **result** — endereço onde o resultado deve ser armazenado

### Valor de retorno

false se o valor atribuído a *result representar corretamente o resultado matemático da multiplicação, true caso contrário.

### Nota

Ambos type2 e type3 devem ser qualquer tipo inteiro diferente de char "simples", bool, um tipo inteiro de precisão de bit, ou um tipo enumerado, e eles podem ser os mesmos. *result deve ser um lvalue modificável de qualquer tipo inteiro diferente de char "simples", bool, um tipo inteiro de precisão de bit, ou um tipo enumerado.

É recomendado produzir uma mensagem de diagnóstico se type2 ou type3 não forem tipos inteiros adequados, ou se *result não for um lvalue modificável de um tipo inteiro adequado.

### Exemplo

| Esta seção está incompleta
Razão: nenhum exemplo

### Referências

* Padrão C23 (ISO/IEC 9899:2024):

* 7.20.1 As macros de operação inteira verificada ckd_ (p: 311)

### Veja também

[ ckd_add](<#/doc/numeric/ckd_add>)(C23) | operação de adição verificada em dois inteiros
(macro de função genérica por tipo)
[ ckd_sub](<#/doc/numeric/ckd_sub>)(C23) | operação de subtração verificada em dois inteiros
(macro de função genérica por tipo)