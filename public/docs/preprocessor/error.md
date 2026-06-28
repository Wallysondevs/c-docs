# Diretivas de diagnóstico

Exibe a mensagem de erro fornecida e torna o programa malformado, ou exibe a mensagem de aviso fornecida sem afetar a validade do programa (desde C23).

### Sintaxe

---
`#error` mensagem-de-diagnóstico | (1) |
`#warning` mensagem-de-diagnóstico | (2) | (desde C23)
---

### Explicação

1) Após encontrar a diretiva `#error`, uma implementação exibe a mensagem mensagem-de-diagnóstico e torna o programa malformado (a compilação é interrompida).

2) O mesmo que (1), exceto que a validade do programa não é afetada e a compilação continua.

mensagem-de-diagnóstico pode consistir em várias palavras, não necessariamente entre aspas.

### Notas

Antes de sua padronização em C23, `#warning` foi fornecido por muitos compiladores em todos os modos como uma extensão conforme.

### Exemplo

Execute este código
```
    #if __STDC__ != 1
    #  error "Not a standard compliant compiler"
    #endif
    
    #if __STDC_VERSION__ >= 202311L
    #  warning "Using #warning as a standard feature"
    #endif
    
    #include <stdio.h>
    
    int main (void)
    {
        printf("The compiler used conforms to the ISO C Standard !!");
    }
```

Saída possível:
```
    The compiler used conforms to the ISO C Standard !!
```

### Referências

* Padrão C23 (ISO/IEC 9899:2024):

  * 6.10.5 Diretiva de erro (p: TBD)

* Padrão C17 (ISO/IEC 9899:2018):

  * 6.10.5 Diretiva de erro (p: 126-127)

* Padrão C11 (ISO/IEC 9899:2011):

  * 6.10.5 Diretiva de erro (p: 174)

* Padrão C99 (ISO/IEC 9899:1999):

  * 6.10.5 Diretiva de erro (p: 159)

* Padrão C89/C90 (ISO/IEC 9899:1990):

  * 3.8.5 Diretiva de erro

### Veja também

[documentação C++](<#/>) para Diretivas de diagnóstico
---