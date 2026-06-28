# system

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
int system( const char *command );
```

  
Chama o processador de comandos do ambiente hospedeiro com o parâmetro `command`. Retorna um valor definido pela implementação (geralmente o valor que o programa invocado retorna). 

Se `command` for um ponteiro nulo, verifica se o ambiente hospedeiro possui um processador de comandos e retorna um valor diferente de zero se e somente se o processador de comandos existir. 

### Parâmetros

command  |  \-  |  string de caracteres que identifica o comando a ser executado no processador de comandos. Se um ponteiro nulo for fornecido, a existência do processador de comandos é verificada   
  
### Valor de retorno

Valor definido pela implementação. Se `command` for um ponteiro nulo, retorna um valor diferente de zero se e somente se o processador de comandos existir. 

### Observações

Em sistemas POSIX, o valor de retorno pode ser decomposto usando [`WEXITSTATUS` e `WSTOPSIG`](<http://pubs.opengroup.org/onlinepubs/9699919799/functions/wait.html>). 

A função POSIX relacionada [popen](<http://pubs.opengroup.org/onlinepubs/9699919799/functions/popen.html>) torna a saída gerada por `command` disponível para o chamador. 

### Exemplo

Neste exemplo, há uma chamada de sistema do comando Unix **date +%A** e uma chamada de sistema para o compilador **gcc** (possivelmente instalado) com o argumento de linha de comando (_\--version_): 

Execute este código
```c
    #include <stdlib.h>
     
    int main(void) {
        system("date +%A");
        system("gcc --version");
    }
```

Saída possível: 
```
    Wednesday
    gcc (GCC) 11.2.0
    ...
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.22.4.8 A função system (p: 257) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.22.4.8 A função system (p: 353-354) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.20.4.6 A função system (p: 317) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.10.4.5 A função system 

### Veja também

[Documentação C++](<#/>) para system  
---