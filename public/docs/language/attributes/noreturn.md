# Atributo C: noreturn, _Noreturn (desde C23)

Indica que a função não retorna.

### Sintaxe

---
`[[` `noreturn` `]]`
`[[` `__noreturn__` `]]`
`[[` `_Noreturn` `]]`
`[[` `___Noreturn__` `]]` | | (obsoleto)

### Explicação

Indica que a função não retorna.

Este atributo se aplica ao nome da função e especifica que a função não retorna pela execução da instrução return ou por atingir o final do corpo da função (ela pode retornar pela execução de [longjmp](<#/doc/program/longjmp>)). O comportamento é indefinido se a função com este atributo realmente retornar. Um diagnóstico do compilador é recomendado se isso puder ser detectado.

Anteriormente, era denotado pela palavra-chave [`_Noreturn`](<#/doc/language/_Noreturn>) até ser descontinuado desde C23 e substituído por este atributo.

### Biblioteca padrão

As seguintes funções padrão são declaradas com o atributo `noreturn` (elas costumavam ser declaradas com o especificador [`_Noreturn`](<#/doc/language/_Noreturn>) até C23):

  * [abort()](<#/doc/program/abort>)
  * [exit()](<#/doc/program/exit>)
  * [_Exit()](<#/doc/program/_Exit>)
  * [quick_exit()](<#/doc/program/quick_exit>)
  * [thrd_exit()](<#/doc/thread/thrd_exit>)
  * [longjmp()](<#/doc/program/longjmp>)

### Veja também

[Documentação C](<#/doc/language/_Noreturn>) para _Noreturn
---
[Documentação C++](<#/>) para `[[noreturn]]`