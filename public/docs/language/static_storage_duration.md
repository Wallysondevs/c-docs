# Duração de armazenamento estática

Um objeto cujo identificador é declarado sem o especificador de classe de armazenamento `_Thread_local`, e com [ligação](<#/doc/language/storage_duration>) externa ou interna, ou com o especificador de classe de armazenamento `static`, tem duração de armazenamento estática. Sua vida útil é a execução completa do programa e seu valor armazenado é inicializado apenas uma vez, antes do início do programa.

### Observações

Como seu valor armazenado é inicializado apenas uma vez, um objeto com duração de armazenamento estática pode registrar as invocações de uma função.

O outro uso da palavra-chave `static` é [escopo de arquivo](<#/doc/language/file_scope>).

### Exemplo

Execute este código
```
    #include <stdio.h>
    
    void f (void)
    {
        static int count = 0;   // variável estática
        int i = 0;              // variável automática
        printf("%d %d\n", i++, count++);
    }
    
    int main(void)
    {
        for (int ndx=0; ndx<10; ++ndx)
            f();
    }
```

Saída:
```
    0 0
    0 1
    0 2
    0 3
    0 4
    0 5
    0 6
    0 7
    0 8
    0 9
```