# asprintf, aswprintf, vasprintf, vaswprintf

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
int asprintf( char **restrict strp, const char *restrict fmt, ... );
int aswprintf( wchar_t **restrict strp, const wchar_t *restrict fmt, ... );
int vasprintf( char **restrict strp, const char *restrict fmt,
va_list arg );
int vaswprintf( wchar_t **restrict strp, const wchar_t *restrict fmt,
va_list arg );
```

  
1) Análogo a [sprintf](<#/doc/io/fprintf>), exceto que ele aloca um armazenamento grande o suficiente para conter a saída, incluindo o caractere nulo terminador, como se por uma chamada a [malloc](<#/doc/memory/malloc>), e retorna um ponteiro para esse armazenamento através do primeiro argumento. Este ponteiro deve ser passado para [free](<#/doc/memory/free>) para liberar o armazenamento alocado quando ele não for mais necessário.

2) O mesmo que (1), exceto que funciona com caracteres largos wchar_t (por analogia com [swprintf](<#/doc/io/fwprintf>)). 

3) O mesmo que (1), com a lista de argumentos variáveis substituída por `arg`, que deve ser inicializada pela macro va_start (e possivelmente chamadas subsequentes de va_arg).

4) O mesmo que (3), exceto que funciona com caracteres largos wchar_t.

### Parâmetros

strp  |  \-  |  Um ponteiro para um char* ou wchar_t* que conterá a saída formatada   
fmt  |  \-  |  Uma string de formato como em [printf](<#/doc/io/fprintf>)/[wprintf](<#/doc/io/fwprintf>) e funções relacionadas   
arg  |  \-  |  Quaisquer argumentos extras são usados como em [vsprintf](<#/doc/io/vfprintf>) e [vswprintf](<#/doc/io/vfwprintf>)  
  
### Valor de retorno

O número de caracteres escritos, assim como [sprintf](<#/doc/io/fprintf>) (1), [swprintf](<#/doc/io/fwprintf>) (2), [vsprintf](<#/doc/io/vfprintf>) (3), ou [vswprintf](<#/doc/io/vfwprintf>) (4), respectivamente. Se a alocação de memória não for possível, ou ocorrer algum outro erro, essas funções retornarão -1, e o conteúdo de `strp` é comportamento indefinido. 

### Notas

Essas funções são extensões GNU, não presentes em C ou POSIX. Elas também estão disponíveis sob *BSD. A implementação do FreeBSD define `strp` como `NULL` em caso de erro. 

As funções `vasprintf` e `vaswprintf` não invocam a macro va_end. 

### Exemplo

Pode ser testado com clang (C11)

Execute este código
```c
    #include <stdio.h>
    #include <stdlib.h>
    #include <stdarg.h>
    
    void test(const char *fmt, ...)
    {
        char* dyn_buf;
    
        printf("Demo asprintf:\n");
        const int written_1 = asprintf(&dyn_buf, "%s", fmt);
        printf("dyn_buf: \"%s\"; %i chars were written\n", dyn_buf, written_1);
        free(dyn_buf);
    
        printf("Demo vasprintf:\n");
        va_list args;
        va_start(args, fmt);
        const int written_2 = vasprintf(&dyn_buf, fmt, args);
        va_end(args);
        printf("dyn_buf: \"%s\"; %i chars were written\n", dyn_buf, written_2);
        free(dyn_buf);
    }
    
    int main(void)
    {
        test("Testing... %d, %d, %d", 1, 2, 3);
    }
```

Saída: 
```
    Demo asprintf:
    dyn_buf: "Testing... %d, %d, %d"; 21 chars were written
    Demo vasprintf:
    dyn_buf: "Testing... 1, 2, 3"; 18 chars were written
```