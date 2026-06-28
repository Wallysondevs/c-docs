# ungetwc

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
wint_t ungetwc( wint_t ch, FILE *stream );  // desde C95
```

Se `ch` não for igual a WEOF, insere o caractere largo `ch` no buffer de entrada associado ao fluxo `stream` de tal forma que uma operação de leitura subsequente de `stream` recuperará esse caractere largo. O dispositivo externo associado ao fluxo não é modificado.

As operações de reposicionamento de fluxo [fseek](<#/doc/io/fseek>), [fsetpos](<#/doc/io/fsetpos>) e [rewind](<#/doc/io/rewind>) descartam os efeitos de `ungetwc`.

Se `ungetwc` for chamada mais de uma vez sem uma leitura ou reposicionamento intermediário, ela pode falhar (em outras palavras, um buffer de pushback de tamanho 1 é garantido, mas qualquer buffer maior é definido pela implementação). Se múltiplas chamadas bem-sucedidas de `ungetwc` forem realizadas, as operações de leitura recuperam os caracteres largos inseridos de volta na ordem inversa de `ungetwc`.

Se `ch` for igual a WEOF, a operação falha e o fluxo não é afetado.

Uma chamada bem-sucedida a `ungetwc` limpa o flag de status de fim de arquivo [feof](<#/doc/io/feof>).

Uma chamada bem-sucedida a `ungetwc` em um fluxo (seja de texto ou binário) modifica o indicador de posição do fluxo de maneira não especificada, mas garante que, após todos os caracteres largos inseridos de volta serem recuperados com uma operação de leitura, o indicador de posição do fluxo seja igual ao seu valor antes de `ungetwc`.

### Parâmetros

- **ch** — caractere largo a ser inserido de volta
- **stream** — fluxo de arquivo para inserir o caractere largo de volta

### Valor de retorno

Em caso de sucesso, `ch` é retornado.

Em caso de falha, WEOF é retornado e o fluxo fornecido permanece inalterado.

### Referências

* Padrão C11 (ISO/IEC 9899:2011):

  * 7.29.3.10 A função ungetwc (p: 425-426)

* Padrão C99 (ISO/IEC 9899:1999):

  * 7.24.3.10 A função ungetwc (p: 370-371)

### Veja também

[ ungetc](<#/doc/io/ungetc>) | insere um caractere de volta em um fluxo de arquivo
(função)
[ fgetwcgetwc](<#/doc/io/fgetwc>)(C95) | obtém um caractere largo de um fluxo de arquivo
(função)
[Documentação C++](<#/>) para ungetwc