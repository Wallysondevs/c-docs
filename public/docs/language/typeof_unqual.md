# Operadores typeof (desde C23)

Determina o tipo de um objeto.

### Sintaxe

---
`typeof(` type `)` | (1) |
`typeof(` expression `)` | (2) |
`typeof_unqual(` type `)` | (3) |
`typeof_unqual(` expression `)` | (4) |

### Explicação

1) produz o nome do tipo com qualquer especificador typeof aninhado avaliado

2) resulta no nome do tipo que representa o tipo de seu operando. Nenhuma conversão implícita é aplicada à expressão.

3,4) o mesmo que (1) e (2) respectivamente, mas remove qualificadores

### Notas

`typeof` e `typeof_unqual` são coletivamente chamados de _operadores typeof_. Os operadores `typeof` não podem ser aplicados a membros de bit-field. Se o tipo do operando for um tipo variably modified, o operando é avaliado; caso contrário, o operando não é avaliado. O resultado do operador `typeof_unqual` é o tipo não-atômico não qualificado que resultaria do operador `typeof`. O operador `typeof` preserva todos os qualificadores.

### Exemplo

| Esta seção está incompleta
Motivo: nenhum exemplo

### Referências

* Padrão C23 (ISO/IEC 9899:2024):

* 6.7.2.5 Os especificadores typeof (p: 115-118)

### Veja também

[Documentação C++](<#/>) para decltype
---