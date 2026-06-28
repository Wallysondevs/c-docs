# Informações de nome de arquivo e linha

Altera o número da linha atual e o nome do arquivo no pré-processador.

### Sintaxe

---
`#line` lineno | (1) |
`#line` lineno `"` filename`"` | (2) |
---

### Explicação

1) Altera o número da linha atual do pré-processador para lineno. Ocorrências da macro `__LINE__` a partir deste ponto serão expandidas para lineno mais o número de linhas de código-fonte reais encontradas desde então.

2) Também altera o nome do arquivo atual do pré-processador para filename. Ocorrências da macro `__FILE__` a partir deste ponto produzirão filename.

Quaisquer tokens de pré-processamento (constantes de macro ou expressões) são permitidos como argumentos para `#line`, desde que se expandam para um inteiro decimal válido, opcionalmente seguido por uma string de caracteres válida.

lineno deve ser uma sequência de pelo menos um dígito decimal (o programa é malformado, caso contrário) e é sempre interpretado como decimal (mesmo que comece com `0`).

Se lineno for `0` ou maior que `32767`(até C99)`2147483647`(desde C99), o comportamento é indefinido.

### Observações

Esta diretiva é usada por algumas ferramentas de geração automática de código que produzem arquivos-fonte C a partir de um arquivo escrito em outra linguagem. Nesse caso, as diretivas `#line` podem ser inseridas no arquivo C gerado, referenciando os números de linha e o nome do arquivo-fonte original (editável por humanos).

O número da linha que segue a diretiva `#line __LINE__` é não especificado (existem dois valores possíveis para os quais `__LINE__` pode se expandir neste caso: número de quebras de linha vistas até agora, ou número de quebras de linha vistas até agora mais a quebra de linha que encerra a diretiva `#line`). Este é o resultado de [DR 464](<https://www.open-std.org/jtc1/sc22/wg14/www/docs/n2257.htm#dr_464>), que se aplica retroativamente.

### Exemplo

Execute este código
```c
    #include <assert.h>
    #define FNAME "test.c"
    int main(void)
    {
    #line 777 FNAME
            assert(2+2 == 5);
    }
```

Saída possível:
```
    test: test.c:777: int main(): Assertion `2+2 == 5' failed.
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

  * 6.10.4 Controle de linha (p: 126)

  * J.1 Comportamento não especificado

  * Padrão C11 (ISO/IEC 9899:2011):

  * 6.10.4 Controle de linha (p: 173)

  * Padrão C99 (ISO/IEC 9899:1999):

  * 6.10.4 Controle de linha (p: 158)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

  * 3.8.4 Controle de linha

### Veja também

[Documentação C++](<#/>) para Informações de nome de arquivo e linha
---