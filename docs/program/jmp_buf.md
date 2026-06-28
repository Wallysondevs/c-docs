# jmp_buf

Definido no cabeçalho [`<setjmp.h>`](<#/doc/program>)

```c
typedef /* unspecified */ jmp_buf;
```

  
O tipo `jmp_buf` é um tipo de array adequado para armazenar informações para restaurar um ambiente de chamada. A informação armazenada é suficiente para restaurar a execução no bloco correto do programa e a invocação desse bloco. O estado dos sinalizadores de status de ponto flutuante, ou arquivos abertos, ou quaisquer outros dados não é armazenado em um objeto do tipo `jmp_buf`. 

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.13/2 Saltos não locais <setjmp.h> (p: A definir) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.13/2 Saltos não locais <setjmp.h> (p: 191) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.13/2 Saltos não locais <setjmp.h> (p: 262) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.13/2 Saltos não locais <setjmp.h> (p: 243) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.6 SALTOS NÃO LOCAIS <setjmp.h>

### Veja também

[ setjmp](<#/doc/program/setjmp>) |  salva o contexto   
(macro de função)  
[ longjmp](<#/doc/program/longjmp>) |  salta para o local especificado   
(função)  
[Documentação C++](<#/>) para jmp_buf