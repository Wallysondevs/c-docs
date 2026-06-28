# Constantes Booleanas Predefinidas (desde C23)

### Sintaxe
  
---  
`true` |  (1)  |  (desde C23)  
`false` |  (2)  |  (desde C23)  
  
### Explicação

As palavras-chave true e false representam constantes predefinidas. Elas são [não-lvalues](<#/doc/language/value_category>) do tipo [`bool`](<#/doc/language/types>).

### Notas

Veja [conversões integrais](<#/doc/language/conversion>) para conversões implícitas de bool para outros tipos e [conversões booleanas](<#/doc/language/conversion>) para as conversões implícitas de outros tipos para bool.

Até C23, true e false eram implementadas como macros fornecidas em [`<stdbool.h>`](<#/doc/types>). Uma implementação também pode definir bool, true e false como macros predefinidas em C23 para compatibilidade.

### Exemplo

Execute este código
```
    #include <assert.h>
     
    int main()
    {
        assert(true == 1 && 0 == false);
    }
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 6.4.4.6 Constantes predefinidas (p: 66) 

### Veja também

[Documentação C++](<#/>) para literais Booleanos  
---