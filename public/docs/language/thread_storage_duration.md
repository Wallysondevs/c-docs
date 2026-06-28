# Duração de armazenamento de thread

Um objeto cujo identificador é declarado com o especificador de classe de armazenamento _Thread_local (desde C11) possui duração de armazenamento de thread. Sua vida útil é a execução completa da thread para a qual ele é criado, e seu valor armazenado é inicializado quando a thread é iniciada. Existe um objeto distinto por thread, e o uso do nome declarado em uma expressão se refere ao objeto associado à thread que está avaliando a expressão. O resultado de tentar acessar indiretamente um objeto com duração de armazenamento de thread a partir de uma thread diferente daquela à qual o objeto está associado é definido pela implementação.

### Exemplo

Execute este código
```c
    const double PI = 3.14159;         /* const variable is global to all threads  */
    _Thread_local unsigned int seed;   /* seed is a thread-specific variable       */
    
    int main(void)
    {
        return 0;
    }
```

Saída possível:
```
    (none)
```