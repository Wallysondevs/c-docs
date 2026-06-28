# getenv, getenv_s

Definido no cabeçalho [`<stdlib.h>`](<#/doc/program>)

```c
char *getenv( const char *name );
errno_t getenv_s( size_t *restrict len, char *restrict value,
rsize_t valuesz, const char *restrict name );  // desde C11
```

  
1) Procura por uma variável de ambiente com o nome name na lista de ambiente especificada pelo host e retorna um ponteiro para a string associada à variável de ambiente correspondente. O conjunto de variáveis de ambiente e os métodos para alterá-las são definidos pela implementação.

Esta função não é obrigada a ser thread-safe. Outra chamada a `getenv`, bem como uma chamada às funções POSIX [`setenv()`](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/setenv.html>), [`unsetenv()`](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/unsetenv.html>), e [`putenv()`](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/putenv.html>) podem invalidar o ponteiro retornado por uma chamada anterior ou modificar a string obtida de uma chamada anterior.

Modificar a string retornada por `getenv` invoca comportamento indefinido.

2) O mesmo que (1), exceto que os valores da variável de ambiente são escritos no buffer fornecido pelo usuário value (a menos que seja nulo) e o número de bytes escritos é armazenado no local fornecido pelo usuário *len (a menos que seja nulo). Se a variável de ambiente não estiver definida no ambiente, zero é escrito em *len (a menos que seja nulo) e '\0' é escrito em value[0] (a menos que seja nulo). Além disso, os seguintes erros são detectados em tempo de execução e chamam a função [manipulador de restrição](<#/doc/error/set_constraint_handler_s>) atualmente instalada: 

    

  * name é um ponteiro nulo 
  * valuesz é maior que RSIZE_MAX
  * value é um ponteiro nulo e valuesz não é zero 

    Assim como todas as funções com verificação de limites, `getenv_s` só é garantida como disponível se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir [`<stdlib.h>`](<#/doc/program>).

### Parâmetros

name  |  \-  |  string de caracteres terminada em nulo identificando o nome da variável de ambiente a ser procurada   
len  |  \-  |  ponteiro para um local fornecido pelo usuário onde `getenv_s` armazenará o comprimento da variável de ambiente   
value  |  \-  |  ponteiro para um array de caracteres fornecido pelo usuário onde `getenv_s` armazenará o conteúdo da variável de ambiente   
valuesz  |  \-  |  número máximo de caracteres que `getenv_s` tem permissão para escrever em `dest` (tamanho do buffer)   
  
### Valor de retorno

1) string de caracteres identificando o valor da variável de ambiente ou ponteiro nulo se tal variável não for encontrada.

2) zero se a variável de ambiente foi encontrada, diferente de zero se não foi encontrada ou se ocorreu uma violação de restrição em tempo de execução. Em qualquer erro, escreve zero em *len (a menos que len seja um ponteiro nulo).

### Observações

Em sistemas POSIX, as [variáveis de ambiente](<https://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap08.html#tag_08>) também são acessíveis através da variável global `environ`, declarada como extern char **environ; em `<unistd.h>`, e através do terceiro argumento opcional, `envp`, da [função main](<#/doc/language/main_function>). 

A chamada a `getenv_s` com um ponteiro nulo para value e zero para valuesz é usada para determinar o tamanho do buffer necessário para armazenar o resultado completo. 

### Exemplo

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(void)
    {
        const char *name = "PATH";
        const char *env_p = getenv(name);
        if (env_p)
            printf("Your %s is %s\n", name, env_p);
    }
```

Saída possível: 
```
    Your PATH is /home/gamer/.local/bin:/usr/local/bin:/usr/bin:/bin:/usr/share/games
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.22.4.6 A função getenv (p: TBD) 

    

  * K.3.6.2.1 A função getenv_s (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.22.4.6 A função getenv (p: 256-257) 

    

  * K.3.6.2.1 A função getenv_s (p: 440-441) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.22.4.6 A função getenv (p: 352-353) 

    

  * K.3.6.2.1 A função getenv_s (p: 606-607) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.20.4.5 A função getenv (p: 317) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.10.4.4 A função getenv 

### Veja também

[Documentação C++](<#/>) para getenv  
---