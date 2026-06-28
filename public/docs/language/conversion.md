# Conversões implícitas

Quando uma expressão é usada em um contexto onde um valor de um tipo diferente é esperado, uma _conversão_ pode ocorrer:
```c
    int n = 1L; // expression 1L has type long, int is expected
    n = 2.1; // expression 2.1 has type double, int is expected
    char *p = malloc(10); // expression malloc(10) has type void*, char* is expected
```

As conversões ocorrem nas seguintes situações:

### Conversão como se por atribuição

  * No operador de [atribuição](<#/doc/language/operator_assignment>), o valor do operando do lado direito é convertido para o tipo não qualificado do operando do lado esquerdo.
  * Na [inicialização escalar](<#/doc/language/scalar_initialization>), o valor da expressão inicializadora é convertido para o tipo não qualificado do objeto sendo inicializado.
  * Em uma [expressão de chamada de função](<#/doc/language/operator_other>), para uma função que possui um protótipo, o valor de cada expressão de argumento é convertido para o tipo dos tipos declarados não qualificados do parâmetro correspondente.
  * Em uma [instrução return](<#/doc/language/return>), o valor do operando de `return` é convertido para um objeto que possui o tipo de retorno da função.

Note que a atribuição real, além da conversão, também remove faixa e precisão extras de tipos de ponto flutuante e proíbe sobreposições; essas características não se aplicam à conversão como se por atribuição.

### Promoções de argumento padrão

Em uma [expressão de chamada de função](<#/doc/language/operator_other>) quando a chamada é feita para

1) uma [função sem protótipo](<#/doc/language/function_declaration>) (até C23)

2) uma [função variádica](<#/doc/language/variadic>), onde a expressão do argumento é um dos argumentos finais que são correspondidos ao parâmetro de reticências

Cada argumento de tipo inteiro passa por _promoção de inteiro_ (veja abaixo), e cada argumento do tipo float é implicitamente convertido para o tipo double.
```c
    int add_nums(int count, ...);
    int sum = add_nums(2, 'c', true); // add_nums is called with three ints: (2, 99, 1)
```

Note que float [complex](<#/doc/numeric/complex/complex>) e float [imaginary](<#/doc/numeric/complex/imaginary>) não são promovidos para double [complex](<#/doc/numeric/complex/complex>) e double [imaginary](<#/doc/numeric/complex/imaginary>) neste contexto. | (desde C99)

### Conversões aritméticas usuais

Os argumentos dos seguintes operadores aritméticos passam por conversões implícitas com o propósito de obter o _tipo real comum_, que é o tipo no qual o cálculo é realizado:

  * [aritméticos binários](<#/doc/language/operator_arithmetic>) *, /, %, +, -
  * [operadores relacionais](<#/doc/language/operator_comparison>) <, >, <=, >=, ==, !=
  * [aritméticos bit a bit binários](<#/doc/language/operator_arithmetic>) &, ^, |
  * o [operador condicional](<#/doc/language/operator_other>) ?:

1) Se um operando tem tipo de ponto flutuante decimal, o outro operando não deve ter tipo de ponto flutuante padrão, complexo ou imaginário.

  * Primeiro, se o tipo de qualquer um dos operandos for _Decimal128, o outro operando é convertido para _Decimal128.
  * Caso contrário, se o tipo de qualquer um dos operandos for _Decimal64, o outro operando é convertido para _Decimal64.
  * Caso contrário, se o tipo de qualquer um dos operandos for _Decimal32, o outro operando é convertido para _Decimal32.

| (desde C23)

2) Caso contrário, se um operando é long double, long double [complex](<#/doc/numeric/complex/complex>), ou long double [imaginary](<#/doc/numeric/complex/imaginary>) (desde C99), o outro operando é implicitamente convertido da seguinte forma:

  * tipo inteiro ou ponto flutuante real para long double

  * tipo complexo para long double [complex](<#/doc/numeric/complex/complex>)
  * tipo imaginário para long double [imaginary](<#/doc/numeric/complex/imaginary>)

| (desde C99)

3) Caso contrário, se um operando é double, double [complex](<#/doc/numeric/complex/complex>), ou double [imaginary](<#/doc/numeric/complex/imaginary>) (desde C99), o outro operando é implicitamente convertido da seguinte forma:

  * tipo inteiro ou ponto flutuante real para double

  * tipo complexo para double [complex](<#/doc/numeric/complex/complex>)
  * tipo imaginário para double [imaginary](<#/doc/numeric/complex/imaginary>)

| (desde C99)

4) Caso contrário, se um operando é float, float [complex](<#/doc/numeric/complex/complex>), ou float [imaginary](<#/doc/numeric/complex/imaginary>) (desde C99), o outro operando é implicitamente convertido da seguinte forma:

  * tipo inteiro para float (o único tipo real possível é float, que permanece como está)

  * tipo complexo permanece float [complex](<#/doc/numeric/complex/complex>)
  * tipo imaginário permanece float [imaginary](<#/doc/numeric/complex/imaginary>)

| (desde C99)

5) Caso contrário, ambos os operandos são inteiros. Ambos os operandos passam por _promoções de inteiro_ (veja abaixo); então, após a promoção de inteiro, um dos seguintes casos se aplica:

  * Se os tipos são os mesmos, esse tipo é o tipo comum.
  * Caso contrário, os tipos são diferentes:
    * Se os tipos têm a mesma característica de sinal (ambos com sinal ou ambos sem sinal), o operando cujo tipo tem o menor _rank de conversão_ 1 é implicitamente convertido2 para o outro tipo.
    * Caso contrário, os operandos têm características de sinal diferentes:
      * Se o tipo sem sinal tem _rank de conversão_ maior ou igual ao rank do tipo com sinal, então o operando com o tipo com sinal é implicitamente convertido para o tipo sem sinal.
      * Caso contrário, o tipo sem sinal tem _rank de conversão_ menor que o tipo com sinal:
        * Se o tipo com sinal pode representar todos os valores do tipo sem sinal, então o operando com o tipo sem sinal é implicitamente convertido para o tipo com sinal.
        * Caso contrário, ambos os operandos passam por conversão implícita para o tipo sem sinal correspondente ao tipo do operando com sinal.

* * *

    1. Consulte "promoções de inteiro" abaixo para as regras de classificação.
    2. Consulte "conversões de inteiro" em "semântica de conversão implícita" abaixo.
```c
    1.f + 20000001; // int is converted to float, giving 20000000.00
                    // addition and then rounding to float gives 20000000.00
    
    (char)'a' + 1L; // first, char 'a', which is 97, is promoted to int
                    // different types: int and long
                    // same signedness: both signed
                    // different rank: long is of greater rank than int
                    // therefore, int 97 is converted to long 97
                    // the result is 97 + 1 = 98 of type signed long
    
    2u - 10; // different types: unsigned int and signed int
             // different signedness
             // same rank
             // therefore, signed int 10 is converted to unsigned int 10
             // since the arithmetic operation is performed for unsigned integers
             // (see "Arithmetic operators" topic), the calculation performed is (2 - 10)
             // modulo (2 raised to n), where n is the number of value bits of unsigned int
             // if unsigned int is 32-bit long and there is no padding bits in its object
             // representation, then the result is (-8) modulo (2 raised to 32) = 4294967288
             // of type unsigned int
    
    5UL - 2ULL; // different types: unsigned long and unsigned long long
                // same signedness
                // different rank: rank of unsigned long long is greater
                // therefore, unsigned long 5 is converted to unsigned long long 5
                // since the arithmetic operation is performed for unsigned integers
                // (see "Arithmetic operators" topic),
                // if unsigned long long is 64-bit long, then
                // the result is (5 - 2) modulo (2 raised to 64) = 3 of type
                // unsigned long long
    
    0UL - 1LL; // different types: unsigned long and signed long long
               // different signedness
               // different rank: rank of signed long long is greater.
               // if ULONG_MAX > LLONG_MAX, then signed long long cannot represent all
               // unsigned long therefore, this is the last case: both operands are converted
               // to unsigned long long unsigned long 0 is converted to unsigned long long 0
               // long long 1 is converted to unsigned long long 1 since the arithmetic
               // operation is performed for unsigned integers
               // (see "Arithmetic operators" topic),
               // if unsigned long long is 64-bit long, then  
               // the calculation is (0 - 1) modulo (2 raised to 64)
               // thus, the result is 18446744073709551615 (ULLONG_MAX) of type
               // unsigned long long
```

O tipo do resultado é determinado da seguinte forma:

  * se ambos os operandos são complexos, o tipo do resultado é complexo
  * se ambos os operandos são imaginários, o tipo do resultado é imaginário
  * se ambos os operandos são reais, o tipo do resultado é real
  * se os dois operandos de ponto flutuante têm domínios de tipo diferentes (complexo vs. real, complexo vs. imaginário, ou imaginário vs. real), o tipo do resultado é complexo

```c
    double complex z = 1 + 2*I;
    double f = 3.0;
    z + f; // z remains as-is, f is converted to double, the result is double complex
```

| (desde C99)

Como sempre, o resultado de um operador de ponto flutuante pode ter uma faixa e precisão maiores do que o indicado por seu tipo (veja [FLT_EVAL_METHOD](<#/doc/types/limits/FLT_EVAL_METHOD>)).

Nota: operandos reais e imaginários não são implicitamente convertidos para complexos porque isso exigiria computação extra, enquanto produziria resultados indesejáveis em certos casos envolvendo infinitos, NaNs e zeros com sinal. Por exemplo, se reais fossem convertidos para complexos, 2.0×(3.0+i∞) seria avaliado como (2.0+i0.0)×(3.0+i∞) ⇒ (2.0×3.0–0.0×∞) + i(2.0×∞+0.0×3.0) ⇒ NaN+i∞ em vez do correto 6.0+i∞. Se imaginários fossem convertidos para complexos, i2.0×(∞+i3.0) seria avaliado como (0.0+i2.0) × (∞+i3.0) ⇒ (0.0×∞ – 2.0×3.0) + i(0.0×3.0 + 2.0×∞) ⇒ NaN + i∞ em vez de –6.0 + i∞. | (desde C99)

Nota: independentemente das conversões aritméticas usuais, o cálculo pode sempre ser realizado em um tipo mais estreito do que o especificado por estas regras sob a [regra "as-if"](<#/doc/language/as_if>).

### Transformações de valor

#### Conversão de lvalue

Qualquer [expressão lvalue](<#/doc/language/value_category>) de qualquer tipo não-array, quando usada em qualquer contexto diferente de

  * como operando do [operador address-of](<#/doc/language/operator_member_access>) (se permitido)
  * como operando dos [operadores de incremento e decremento](<#/doc/language/operator_incdec>) pré/pós.
  * como operando do lado esquerdo do [operador de acesso a membro](<#/doc/language/operator_member_access>) (ponto).
  * como operando do lado esquerdo dos [operadores de atribuição e atribuição composta](<#/doc/language/operator_assignment>).
  * como operando de [sizeof](<#/doc/language/sizeof>)

passa por _conversão de lvalue_: o tipo permanece o mesmo, mas perde os qualificadores [const](<#/doc/language/const>)/[volatile](<#/doc/language/volatile>)/[restrict](<#/doc/language/restrict>) e propriedades [atomic](<#/doc/language/atomic>), se houver. O valor permanece o mesmo, mas perde suas propriedades de lvalue (o endereço pode não ser mais obtido).

Se o lvalue tem tipo incompleto, o comportamento é indefinido.

Se o lvalue designa um objeto com duração de armazenamento automática cujo endereço nunca foi obtido e se esse objeto não foi inicializado (não declarado com um inicializador e nenhuma atribuição a ele foi realizada antes do uso), o comportamento é indefinido.

Esta conversão modela o carregamento da memória do valor do objeto de sua localização.
```c
    volatile int n = 1;
    int x = n;            // lvalue conversion on n reads the value of n
    volatile int* p = &n; // no lvalue conversion: does not read the value of n
```

#### Conversão de array para ponteiro

Qualquer [expressão lvalue](<#/doc/language/value_category>) de [tipo array](<#/doc/language/array>), quando usada em qualquer contexto diferente de

  * como operando do [operador address-of](<#/doc/language/operator_member_access>)
  * como operando de [sizeof](<#/doc/language/sizeof>)
  * como operando de [typeof](<#/doc/language/typeof_unqual>) e [typeof_unqual](<#/doc/language/typeof_unqual>) (desde C23)
  * como o literal de string usado para [inicialização de array](<#/doc/language/array_initialization>)

passa por uma conversão para o ponteiro não-lvalue para seu primeiro elemento.

Se o array foi declarado [register](<#/doc/language/storage_duration>), o comportamento é indefinido.
```c
    int a[3], b[3][4];
    int* p = a;      // conversion to &a[0]
    int (*q)[4] = b; // conversion to &b[0]
```

#### Conversão de função para ponteiro

Qualquer expressão designadora de função, quando usada em qualquer contexto diferente de

  * como operando do [operador address-of](<#/doc/language/operator_member_access>)
  * como operando de [sizeof](<#/doc/language/sizeof>)
  * como operando de [typeof](<#/doc/language/typeof_unqual>) e [typeof_unqual](<#/doc/language/typeof_unqual>) (desde C23)

passa por uma conversão para o ponteiro não-lvalue para a função designada pela expressão.
```c
    int f(int);
    int (*p)(int) = f; // conversion to &f
    (***p)(1); // repeated dereference to f and conversion back to &f
```

### Semântica de conversão implícita

A conversão implícita, seja _como se por atribuição_ ou uma _conversão aritmética usual_, consiste em duas etapas:

1) transformação de valor (se aplicável)

2) uma das conversões listadas abaixo (se puder produzir o tipo de destino)

#### Tipos compatíveis

A conversão de um valor de qualquer tipo para qualquer [tipo compatível](<#/doc/language/types>) é sempre uma operação nula (no-op) e não altera a representação.
```c
    uint8_t (*a)[10];         // if uint8_t is a typedef to unsigned char
    unsigned char (*b)[] = a; // then these pointer types are compatible
```

#### Promoções de inteiro

Promoção de inteiro é a conversão implícita de um valor de qualquer tipo inteiro com _rank_ menor ou igual ao _rank_ de int ou de um [campo de bits](<#/doc/language/bit_field>) do tipo _Bool(até C23)bool(desde C23), int, signed int, unsigned int, para o valor do tipo int ou unsigned int.

Se int pode representar toda a faixa de valores do tipo original (ou a faixa de valores do campo de bits original), o valor é convertido para o tipo int. Caso contrário, o valor é convertido para unsigned int.

O valor de um campo de bits de um tipo inteiro bit-preciso é convertido para o tipo inteiro bit-preciso correspondente. Caso contrário, os tipos inteiros bit-precisos estão isentos das regras de promoção de inteiro. | (desde C23)

As promoções de inteiro preservam o valor, incluindo o sinal:
```c
    int main(void)
    {
        void f(); // old-style function declaration
                  // since C23, void f(...) has the same behavior wrt promotions
        char x = 'a'; // integer conversion from int to char
        f(x); // integer promotion from char back to int
    }
    
    void f(x) int x; {} // the function expects int
```

_rank_ acima é uma propriedade de todo [tipo inteiro](<#/doc/language/compatible_type>) e é definido da seguinte forma:

1) os ranks de todos os tipos inteiros com sinal são diferentes e aumentam com sua precisão: rank de signed char < rank de short < rank de int < rank de long int < rank de long long int

2) os ranks de todos os tipos inteiros com sinal são iguais aos ranks dos tipos inteiros sem sinal correspondentes

3) o rank de qualquer tipo inteiro padrão é maior que o rank de qualquer tipo inteiro estendido ou tipo inteiro bit-preciso(desde C23) do mesmo tamanho (ou seja, rank de __int64 < rank de long long int, mas rank de long long < rank de __int128 devido à regra (1))

4) rank de char é igual ao rank de signed char e rank de unsigned char

5) o rank de _Bool(até C23)bool(desde C23) é menor que o rank de qualquer outro tipo inteiro padrão

6) o rank de qualquer tipo enumerado é igual ao rank de seu tipo inteiro compatível

7) a classificação é transitiva: se rank de T1 < rank de T2 e rank de T2 < rank de T3 então rank de T1 < rank de T3

8) o rank de um tipo inteiro com sinal bit-preciso deve ser maior que o rank de qualquer tipo inteiro padrão com menor largura ou qualquer tipo inteiro bit-preciso com menor largura. 9) o rank de qualquer tipo inteiro bit-preciso em relação a um tipo inteiro estendido da mesma largura é definido pela implementação. | (desde C23)

10) quaisquer aspectos da classificação relativa de tipos inteiros estendidos não cobertos acima são definidos pela implementação.

Nota: as promoções de inteiro são aplicadas apenas

  * como parte das _conversões aritméticas usuais_ (veja acima)
  * como parte das _promoções de argumento padrão_ (veja acima)
  * ao operando dos operadores aritméticos unários + e -
  * ao operando do operador bit a bit unário ~
  * a ambos os operandos dos operadores de deslocamento << e >>

#### Conversão booleana

Um valor de qualquer tipo escalar pode ser implicitamente convertido para _Bool(até C23)bool(desde C23). Os valores que se comparam iguais a uma expressão constante inteira de valor zero(até C23)são um zero (para tipos aritméticos), nulo (para tipos de ponteiro) ou têm um tipo de [nullptr_t](<#/doc/types/nullptr_t>)(desde C23) são convertidos para ​0​(até C23)false(desde C23), todos os outros valores são convertidos para 1(até C23)true(desde C23).
```c
    bool b1 = 0.5;              // b1 == 1 (0.5 converted to int would be zero)
    bool b2 = 2.0*_Imaginary_I; // b2 == 1 (but converted to int would be zero)
    bool b3 = 0.0 + 3.0*I;      // b3 == 1 (but converted to int would be zero)
    bool b4 = 0.0/0.0;          // b4 == 1 (NaN does not compare equal to zero)
    bool b5 = nullptr;          // b5 == 0 (since C23: nullptr is converted to false)
```

| (desde C99)

#### Conversões de inteiro

Um valor de qualquer tipo inteiro pode ser implicitamente convertido para qualquer outro tipo inteiro. Exceto onde coberto por promoções e conversões booleanas acima, as regras são:

  * se o tipo de destino pode representar o valor, o valor permanece inalterado
  * caso contrário, se o tipo de destino é sem sinal, o valor 2b
, onde b é o número de bits de valor no tipo de destino, é repetidamente subtraído ou adicionado ao valor de origem até que o resultado se encaixe no tipo de destino. Em outras palavras, inteiros sem sinal implementam aritmética modular.
  * caso contrário, se o tipo de destino é com sinal, o comportamento é definido pela implementação (o que pode incluir o levantamento de um sinal)

```c
    char x = 'a'; // int -> char, result unchanged
    unsigned char n = -123456; // target is unsigned, result is 192 (that is, -123456+483*256)
    signed char m = 123456;    // target is signed, result is implementation-defined
    assert(sizeof(int) > -1);  // assert fails:
                               // operator > requests conversion of -1 to size_t,
                               // target is unsigned, result is SIZE_MAX
```

#### Conversões de ponto flutuante real para inteiro

Um valor finito de qualquer tipo de ponto flutuante real pode ser implicitamente convertido para qualquer tipo inteiro. Exceto onde coberto pela conversão booleana acima, as regras são:

  * A parte fracionária é descartada (truncada em direção a zero).

  * Se o valor resultante pode ser representado pelo tipo de destino, esse valor é usado.
  * caso contrário, o comportamento é indefinido

```c
    int n = 3.14; // n == 3
    int x = 1e10; // undefined behavior for 32-bit int
```

Um valor de qualquer tipo inteiro pode ser implicitamente convertido para qualquer tipo de ponto flutuante real.

  * se o valor pode ser representado exatamente pelo tipo de destino, ele permanece inalterado
  * se o valor pode ser representado, mas não pode ser representado exatamente, o resultado é uma escolha definida pela implementação entre o valor mais próximo superior ou mais próximo inferior, embora se a aritmética IEEE for suportada, o arredondamento é para o mais próximo. Não é especificado se [FE_INEXACT](<#/doc/numeric/fenv/FE_exceptions>) é levantado neste caso.
  * se o valor não pode ser representado, o comportamento é indefinido, embora se a aritmética IEEE for suportada, [FE_INVALID](<#/doc/numeric/fenv/FE_exceptions>) é levantado e o valor resultante é não especificado.

O resultado desta conversão pode ter uma faixa e precisão maiores do que o indicado por seu tipo (veja [FLT_EVAL_METHOD](<#/doc/types/limits/FLT_EVAL_METHOD>)).

Se o controle sobre [FE_INEXACT](<#/doc/numeric/fenv/FE_exceptions>) for necessário em conversões de ponto flutuante para inteiro, [rint](<#/doc/numeric/math/rint>) e [nearbyint](<#/doc/numeric/math/nearbyint>) podem ser usados.
```c
    double d = 10; // d = 10.00
    float f = 20000001; // f = 20000000.00 (FE_INEXACT)
    float x = 1+(long long)FLT_MAX; // undefined behavior
```

#### Conversões de ponto flutuante real

Um valor de qualquer tipo de ponto flutuante real pode ser implicitamente convertido para qualquer outro tipo de ponto flutuante real.

  * Se o valor pode ser representado pelo tipo de destino exatamente, ele permanece inalterado
  * se o valor pode ser representado, mas não pode ser representado exatamente, o resultado é o valor mais próximo superior ou o mais próximo inferior (em outras palavras, a direção de arredondamento é definida pela implementação), embora se a aritmética IEEE for suportada, o arredondamento é para o mais próximo
  * se o valor não pode ser representado, o comportamento é indefinido | Esta seção está incompleta
Razão: verificar IEEE se infinito com sinal apropriado é necessário

O resultado desta conversão pode ter uma faixa e precisão maiores do que o indicado por seu tipo (veja [FLT_EVAL_METHOD](<#/doc/types/limits/FLT_EVAL_METHOD>)).
```c
    double d = 0.1; // d = 0.1000000000000000055511151231257827021181583404541015625
    float f = d;    // f = 0.100000001490116119384765625
    float x = 2*(double)FLT_MAX; // undefined
```

#### Conversões de tipo complexo

Um valor de qualquer tipo complexo pode ser implicitamente convertido para qualquer outro tipo complexo. A parte real e a parte imaginária seguem individualmente as regras de conversão para os tipos de ponto flutuante real.
```c
    double complex d = 0.1 + 0.1*I;
    float complex f = d; // f is (0.100000001490116119384765625, 0.100000001490116119384765625)
```

#### Conversões de tipo imaginário

Um valor de qualquer tipo imaginário pode ser implicitamente convertido para qualquer outro tipo imaginário. A parte imaginária segue as regras de conversão para os tipos de ponto flutuante real.
```c
    double imaginary d = 0.1*_Imaginary_I;
    float imaginary f = d; // f is 0.100000001490116119384765625*I
```

#### Conversões real-complexo

Um valor de qualquer tipo de ponto flutuante real pode ser implicitamente convertido para qualquer tipo complexo.

  * A parte real do resultado é determinada pelas regras de conversão para os tipos de ponto flutuante real
  * A parte imaginária do resultado é zero positivo (ou zero sem sinal em sistemas não-IEEE)

Um valor de qualquer tipo complexo pode ser implicitamente convertido para qualquer tipo de ponto flutuante real

  * A parte real é convertida seguindo as regras para os tipos de ponto flutuante real
  * A parte imaginária é descartada

Nota: na conversão de complexo para real, um NaN na parte imaginária não se propagará para o resultado real.
```c
    double complex z = 0.5 + 3*I;
    float f = z;  // the imaginary part is discarded, f is set to 0.5
    z = f;        // sets z to 0.5 + 0*I
```

#### Conversões real-imaginário

Um valor de qualquer tipo imaginário pode ser implicitamente convertido para qualquer tipo real (inteiro ou ponto flutuante). O resultado é sempre um zero positivo (ou sem sinal), exceto quando o tipo de destino é _Bool(até C23)bool(desde C23), caso em que as regras de conversão booleana se aplicam. Um valor de qualquer tipo real pode ser implicitamente convertido para qualquer tipo imaginário. O resultado é sempre um zero imaginário positivo.
```c
    double imaginary z = 3*I;
    bool b = z;  // Boolean conversion: sets b to true 
    float f = z; // Real-imaginary conversion: sets f to 0.0 
    z = 3.14;    // Imaginary-real conversion: sets z to 0*_Imaginary_I
```

#### Conversões complexo-imaginário

Um valor de qualquer tipo imaginário pode ser implicitamente convertido para qualquer tipo complexo.

  * A parte real do resultado é o zero positivo
  * A parte imaginária do resultado segue as regras de conversão para os tipos reais correspondentes

Um valor de qualquer tipo complexo pode ser implicitamente convertido para qualquer tipo imaginário

  * A parte real é descartada
  * A parte imaginária do resultado segue as regras de conversão para os tipos reais correspondentes

```c
    double imaginary z = I * (3*I); // the complex result -3.0+0i loses real part
                                    // sets z to 0*_Imaginary_I
```

| (desde C99)

#### Conversões de ponteiro

Um ponteiro para void pode ser implicitamente convertido de e para qualquer ponteiro para tipo de objeto com a seguinte semântica:

  * Se um ponteiro para objeto é convertido para um ponteiro para void e de volta, seu valor se compara igual ao ponteiro original.
  * Nenhuma outra garantia é oferecida

```c
    int* p = malloc(10 * sizeof(int)); // malloc returns void*
```

Um ponteiro para um tipo não qualificado pode ser implicitamente convertido para o ponteiro para a versão qualificada desse tipo (em outras palavras, qualificadores [const](<#/doc/language/const>), [volatile](<#/doc/language/volatile>) e [restrict](<#/doc/language/restrict>) podem ser adicionados). O ponteiro original e o resultado se comparam iguais.
```c
    int n;
    const int* p = &n; // &n has type int*
```

Qualquer [expressão constante](<#/doc/language/constant_expression>) inteira com valor ​0​, bem como expressão de ponteiro inteiro com valor zero convertida para o tipo void*, pode ser implicitamente convertida para qualquer tipo de ponteiro (tanto ponteiro para objeto quanto ponteiro para função). O resultado é o valor de ponteiro nulo de seu tipo, garantido para se comparar diferente de qualquer valor de ponteiro não nulo desse tipo. Esta expressão inteira ou void* é conhecida como _constante de ponteiro nulo_ e a biblioteca padrão fornece uma definição desta constante como a macro [NULL](<#/doc/types/NULL>).
```c
    int* p = 0;
    double* q = NULL;
```

### Notas

Embora o estouro de inteiro com sinal em qualquer operador aritmético seja comportamento indefinido, o estouro de um tipo inteiro com sinal em uma conversão de inteiro é meramente comportamento não especificado.

Por outro lado, embora o estouro de inteiro sem sinal em qualquer operador aritmético (e em conversão de inteiro) seja uma operação bem definida e siga as regras da aritmética modular, o estouro de um inteiro sem sinal em uma conversão de ponto flutuante para inteiro é comportamento indefinido: os valores de tipo de ponto flutuante real que podem ser convertidos para inteiro sem sinal são os valores do intervalo aberto (-1; Unnn_MAX+1).
```c
    unsigned int n = -1.0; // undefined behavior
```

Conversões entre ponteiros e inteiros (exceto de ponteiro para _Bool(até C23)bool(desde C23) e (desde C99)de expressão constante inteira com valor zero para ponteiro), entre ponteiros para objetos (exceto onde para ou de é um ponteiro para void) e conversões entre ponteiros para funções (exceto quando as funções têm tipos compatíveis) nunca são implícitas e exigem um [operador de cast](<#/doc/language/cast>).

Não há conversões (implícitas ou explícitas) entre ponteiros para funções e ponteiros para objetos (incluindo void*) ou inteiros.

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    * 6.3 Conversões (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    * 6.3 Conversões (p: 37-41)

  * Padrão C11 (ISO/IEC 9899:2011):

    * 6.3 Conversões (p: 50-56)

  * Padrão C99 (ISO/IEC 9899:1999):

    * 6.3 Conversões (p: 42-48)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    * 3.2 Conversões

### Veja também

[Documentação C++](<#/>) para Conversões implícitas
---