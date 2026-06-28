# instrução goto

Transfere o controle incondicionalmente para o local desejado.
Usado quando, de outra forma, é impossível transferir o controle para o local desejado usando construções convencionais.

### Sintaxe

---
attr-spec-seq(optional) `goto` label `;`
- **label** — [rótulo](<#/doc/language/statements>) alvo para a instrução `goto`
- **attr-spec-seq** — (C23)lista opcional de [atributos](<#/doc/language/attributes>), aplicada à instrução `goto`

### Explicação

A instrução `goto` causa um salto incondicional (transferência de controle) para a instrução prefixada pelo rótulo nomeado (que deve aparecer na mesma função que a instrução goto), exceto quando este salto entraria no escopo de um [array de tamanho variável](<#/doc/language/array>) ou outro [tipo modificado variavelmente](<#/doc/language/declarations>). (desde C99)

Um rótulo é um identificador seguido por dois pontos (`:`) e uma instrução (até C23). Rótulos são os únicos identificadores que possuem _escopo de função_ : eles podem ser usados (em uma instrução goto) em qualquer lugar na mesma função em que aparecem. Pode haver múltiplos rótulos antes de qualquer instrução.

Entrar no escopo de uma variável não modificada variavelmente é permitido:
```c
    goto lab1; // OK: entrando no escopo de uma variável regular
        int n = 5;
    lab1:; // Nota, n não é inicializado, como se declarado por int n;
     
    //   goto lab2;   // Erro: entrando no escopo de dois tipos VM
         double a[n]; // um VLA
         int (*p)[n]; // um ponteiro VM
    lab2:
```

Se `goto` sair do escopo de um VLA, ele é desalocado (e pode ser realocado se sua inicialização for executada novamente):
```c
    {
       int n = 1;
    label:;
       int a[n]; // realocado 10 vezes, cada vez com um tamanho diferente
       if (n++ < 10) goto label; // saindo do escopo de um VM
    }
```

| (desde C99)

### Palavras-chave

[`goto`](<#/doc/keyword/goto>)

### Notas

Como declarações não são instruções, um rótulo antes de uma declaração deve usar uma instrução nula (um ponto e vírgula imediatamente após os dois pontos). O mesmo se aplica a um rótulo antes do final de um bloco. | (até C23)

C++ impõe limitações adicionais à instrução `goto`, mas permite rótulos antes de declarações (que são instruções em C++).

### Exemplo

Execute este código
```c
    #include <stdio.h>
     
    int main(void)
    {
        // goto pode ser usado para sair facilmente de um loop multi-nível
        for (int x = 0; x < 3; x++) {
            for (int y = 0; y < 3; y++) {
                printf("(%d;%d)\n",x,y);
                if (x + y >= 3) goto endloop;
            }
        }
    endloop:;
    }
```

Saída:
```
    (0;0)
    (0;1)
    (0;2)
    (1;0)
    (1;1)
    (1;2)
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 6.8.6.1 A instrução goto (p: 110-111)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 6.8.6.1 A instrução goto (p: 152-153)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 6.8.6.1 A instrução goto (p: 137-138)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 3.6.6.1 A instrução goto

### Veja também

[documentação C++](<#/>) para a instrução `goto`
---