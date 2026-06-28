# thrd_equal

Definido no cabeçalho [`<threads.h>`](<#/doc/thread>)

```c
int thrd_equal( thrd_t lhs, thrd_t rhs );  // desde C11
```

  
Verifica se `lhs` e `rhs` se referem à mesma thread.

### Parâmetros

lhs, rhs  |  \-  |  threads para comparar   
  
### Valor de retorno

Valor diferente de zero se `lhs` e `rhs` se referirem ao mesmo valor, ​0​ caso contrário.

### Referências

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.26.5.4 A função thrd_equal (p: 280) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.26.5.4 A função thrd_equal (p: 384) 

### Veja também

[Documentação C++](<#/>) para operator_cmp  
---