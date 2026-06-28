# Escopo de Arquivo

Se o declarador ou especificador de tipo que declara o identificador aparece fora de qualquer bloco ou lista de parâmetros, o identificador tem escopo de arquivo, que termina no final da unidade de tradução.

Assim, a colocação da declaração de um identificador (em um declarador ou especificador de tipo) fora de qualquer bloco ou lista de parâmetros significa que o identificador tem escopo de arquivo. O escopo de arquivo de um identificador estende-se da declaração até o final da unidade de tradução na qual a declaração aparece.

### Exemplo

Os identificadores a, b, f e g têm escopo de arquivo.

Execute este código
```c
    #include <stdio.h>
     
    int a = 1;
    static int b = 2;
     
    void f (void) {printf("from function f()\n");}
    static void g (void) {printf("from function g()\n");}
     
    int main(void)
    {
        f();
        g();
     
        return 0;
    }
    /* end of this translation unit, end of file scope */
```

Saída possível:
```
    from function f()
    from function g()
```