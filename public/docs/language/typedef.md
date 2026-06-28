# Declaração typedef

A _declaração typedef_ fornece uma maneira de declarar um identificador como um alias de tipo, a ser usado para substituir um [nome de tipo](<#/doc/language/compatible_type>) possivelmente complexo.

A palavra-chave typedef é usada em uma [declaração](<#/doc/language/declarations>), na posição gramatical de um [especificador de classe de armazenamento](<#/doc/language/storage_duration>), exceto que ela não afeta o armazenamento ou a ligação:
```c
    typedef int int_t; // declara int_t como um alias para o tipo int
    typedef char char_t, *char_p, (*fp)(void); // declara char_t como um alias para char
                                               // char_p como um alias para char*
                                               // fp como um alias para char(*)(void)
```

### Explicação

Se uma [declaração](<#/doc/language/declarations>) usa typedef como especificador de classe de armazenamento, cada declarador nela define um identificador como um alias para o tipo especificado. Como apenas um especificador de classe de armazenamento é permitido em uma declaração, a declaração typedef não pode ser [static ou extern](<#/doc/language/storage_duration>).

A declaração typedef não introduz um tipo distinto, ela apenas estabelece um sinônimo para um tipo existente, portanto, os nomes typedef são [compatíveis](<#/doc/language/compatible_type>) com os tipos aos quais eles são alias. Nomes typedef compartilham o [espaço de nomes](<#/doc/language/name_space>) com identificadores comuns, como enumeradores, variáveis e funções.

Um typedef para um VLA (Variable Length Array) só pode aparecer no escopo de bloco. O comprimento do array é avaliado cada vez que o fluxo de controle passa pela declaração typedef, em oposição à declaração do próprio array:
```c
    void copyt(int n)
    {
        typedef int B[n]; // B é um VLA, seu tamanho é n, avaliado agora
        n += 1;
        B a; // o tamanho de a é n de antes de +=1
        int b[n]; // a e b têm tamanhos diferentes
        for (int i = 1; i < n; i++)
            a[i-1] = b[i];
    }
```

| (desde C99)

### Notas

Um nome typedef pode ser um [tipo incompleto](<#/doc/language/compatible_type>), que pode ser completado como de costume:
```c
    typedef int A[]; // A é int[]
    A a = {1, 2}, b = {3,4,5}; // o tipo de a é int[2], o tipo de b é int[3]
```

Declarações typedef são frequentemente usadas para injetar nomes do [espaço de nomes](<#/doc/language/name_space>) de tags no espaço de nomes comum:
```c
    typedef struct tnode tnode; // tnode no espaço de nomes comum
                                // é um alias para tnode no espaço de nomes de tags
    struct tnode {
        int count;
        tnode *left, *right; // o mesmo que struct tnode *left, *right;
    }; // agora tnode também é um tipo completo
    tnode s, *sp; // o mesmo que struct tnode s, *sp;
```

Eles podem até evitar o uso do espaço de nomes de tags completamente:
```c
    typedef struct { double hi, lo; } range;
    range z, *zp;
```

Nomes typedef também são comumente usados para simplificar a sintaxe de declarações complexas:
```c
    // array de 5 ponteiros para funções que retornam ponteiros para arrays de 3 ints
    int (*(*callbacks[5])(void))[3];
     
    // o mesmo com typedefs
    typedef int arr_t[3]; // arr_t é um array de 3 int
    typedef arr_t* (*fp)(void); // ponteiro para função que retorna arr_t*
    fp callbacks[5];
```

Bibliotecas frequentemente expõem tipos dependentes do sistema ou da configuração como nomes typedef, para apresentar uma interface consistente aos usuários ou a outros componentes da biblioteca:
```c
    #if defined(_LP64)
    typedef int     wchar_t;
    #else
    typedef long    wchar_t;
    #endif
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 6.7.8 Type definitions (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 6.7.8 Type definitions (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 6.7.8 Type definitions (p: 137-138)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 6.7.7 Type definitions (p: 123-124)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 3.5.6 Type definitions

### Palavras-chave

[`typedef`](<#/doc/keyword/typedef>)

### Veja também

[Documentação C++](<#/>) para a declaração `typedef`
---