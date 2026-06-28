# qualificador de tipo volatile

Cada tipo individual no [sistema de tipos](<#/doc/language/compatible_type>) do C possui várias versões _qualificadas_ desse tipo, correspondendo a um, dois ou todos os três qualificadores: [`const`](<#/doc/language/const>), `volatile` e, para ponteiros para tipos de objeto, [`restrict`](<#/doc/language/restrict>). Esta página descreve os efeitos do qualificador `volatile`.

Todo acesso (tanto de leitura quanto de escrita) feito através de uma expressão lvalue de tipo qualificado como volatile é considerado um efeito colateral observável para fins de otimização e é avaliado estritamente de acordo com as regras da máquina abstrata (ou seja, todas as escritas são concluídas em algum momento antes do próximo ponto de sequência). Isso significa que, dentro de um único thread de execução, um acesso volatile não pode ser otimizado ou reordenado em relação a outro efeito colateral visível que seja separado por um [ponto de sequência](<#/doc/language/eval_order>) do acesso volatile.

Uma conversão (cast) de um valor não-volatile para um tipo volatile não tem efeito. Para acessar um objeto não-volatile usando semântica volatile, seu endereço deve ser convertido para um ponteiro-para-volatile e então o acesso deve ser feito através desse ponteiro.

Qualquer tentativa de ler ou escrever em um objeto cujo tipo é qualificado como volatile através de um lvalue não-volatile resulta em comportamento indefinido:
```c
    volatile int n = 1; // object of volatile-qualified type
    int* p = (int*)&n;
    int val = *p; // undefined behavior
```

Um membro de uma estrutura ou tipo union qualificado como volatile adquire a qualificação do tipo ao qual pertence (tanto quando acessado usando o operador `.` quanto o operador `- >`):
```c
    struct s { int i; const int ci; } s;
    // the type of s.i is int, the type of s.ci is const int
    volatile struct s vs;
    // the types of vs.i and vs.ci are volatile int and const volatile int
```

| Se um tipo array é declarado com o qualificador de tipo volatile (através do uso de [`typedef`](<#/doc/language/typedef>)), o tipo array não é qualificado como volatile, mas seu tipo de elemento é. | (até C23) |
|---|---|
| Um tipo array e seu tipo de elemento são sempre considerados identicamente qualificados como volatile. | (desde C23) |
```c
    typedef int A[2][3];
    volatile A a = {{4, 5, 6}, {7, 8, 9}}; // array of array of volatile int
    int* pi = a[0]; // Error: a[0] has type volatile int*
    void *unqual_ptr = a; // OK until C23; error since C23
    // Notes: clang applies the rule in C++/C23 even in C89-C17 modes
```

Se um tipo de função é declarado com o qualificador de tipo volatile (através do uso de [`typedef`](<#/doc/language/typedef>)), o comportamento é indefinido.

Em uma declaração de função, a palavra-chave `volatile` pode aparecer dentro dos colchetes que são usados para declarar um tipo array de um parâmetro de função. Ela qualifica o tipo ponteiro para o qual o tipo array é transformado. As duas declarações a seguir declaram a mesma função:
```c
    void f(double x[volatile], const double y[volatile]);
    void f(double * volatile x, const double * volatile y);
```

| (desde C99) |
|---|

Um ponteiro para um tipo não-volatile pode ser implicitamente convertido para um ponteiro para a versão qualificada como volatile do mesmo tipo ou de um tipo [compatível](<#/doc/language/compatible_type>). A conversão inversa requer uma expressão de cast.
```c
    int* p = 0;
    volatile int* vp = p; // OK: adds qualifiers (int to volatile int)
    p = vp; // Error: discards qualifiers (volatile int to int)
    p = (int*)vp; // OK: cast
```

Note que ponteiro para ponteiro para `T` não é conversível para ponteiro para ponteiro para `volatile T`; para que dois tipos sejam compatíveis, suas qualificações devem ser idênticas:
```c
    char *p = 0;
    volatile char **vpp = &p; // Error: char* and volatile char* are not compatible types
    char * volatile *pvp = &p; // OK, adds qualifiers (char* to char*volatile)
```

### Usos de volatile

1) Objetos [`static`](<#/doc/language/static_storage_duration>) `volatile` modelam portas de E/S mapeadas em memória, e objetos `static` `const` `volatile` modelam portas de entrada mapeadas em memória, como um relógio de tempo real:
```c
    volatile short *ttyport = (volatile short*)TTYPORT_ADDR;
    for(int i = 0; i < N; ++i)
        *ttyport = a[i]; // *ttyport is an lvalue of type volatile short
```

2) Objetos `static` `volatile` do tipo [sig_atomic_t](<#/doc/program/sig_atomic_t>) são usados para comunicação com [manipuladores de sinal](<#/doc/program/signal>).

3) Variáveis `volatile` que são locais a uma função que contém uma invocação da macro [setjmp](<#/doc/program/setjmp>) são as únicas variáveis locais garantidas a reter seus valores após o retorno de [longjmp](<#/doc/program/longjmp>).

4) Além disso, variáveis volatile podem ser usadas para desabilitar certas formas de otimização, por exemplo, para desabilitar a eliminação de armazenamento morto (dead store elimination) ou o dobramento de constantes (constant folding) para micro-benchmarks.

Note que variáveis volatile não são adequadas para comunicação entre threads; elas não oferecem atomicidade, sincronização ou ordem de memória. Uma leitura de uma variável volatile que é modificada por outro thread sem sincronização ou modificação concorrente de dois threads não sincronizados é comportamento indefinido devido a uma data race.

### Palavras-chave

[`volatile`](<#/>)

### Exemplo

demonstra o uso de volatile para desabilitar otimizações

Execute este código
```c
    #include <stdio.h>
    #include <time.h>
    
    int main(void)
    {
        clock_t t = clock();
        double d = 0.0;
        for (int n = 0; n < 10000; ++n)
            for (int m = 0; m < 10000; ++m)
                d += d * n * m; // reads from and writes to a non-volatile 
        printf("Modified a non-volatile variable 100m times. "
               "Time used: %.2f seconds\n",
               (double)(clock() - t)/CLOCKS_PER_SEC);
    
        t = clock();
        volatile double vd = 0.0;
        for (int n = 0; n < 10000; ++n)
            for (int m = 0; m < 10000; ++m) {
                double prod = vd * n * m; // reads from a volatile
                vd += prod; // reads from and writes to a volatile
            } 
        printf("Modified a volatile variable 100m times. "
               "Time used: %.2f seconds\n",
               (double)(clock() - t)/CLOCKS_PER_SEC);
    }
```

Saída possível:
```
    Modified a non-volatile variable 100m times. Time used: 0.00 seconds
    Modified a volatile variable 100m times. Time used: 0.79 seconds
```

### Referências

  * C17 standard (ISO/IEC 9899:2018): 

    

  * 6.7.3 Type qualifiers (p: 87-90) 

  * C11 standard (ISO/IEC 9899:2011): 

    

  * 6.7.3 Type qualifiers (p: 121-123) 

  * C99 standard (ISO/IEC 9899:1999): 

    

  * 6.7.3 Type qualifiers (p: 108-110) 

  * C89/C90 standard (ISO/IEC 9899:1990): 

    

  * 6.5.3 Type qualifiers 

### Veja também

[documentação C++](<#/>) para qualificadores de tipo cv (`const` e `volatile`)
---