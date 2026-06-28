# gets, gets_s

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
char* gets( char* str );
char* gets_s( char* str, rsize_t n );  // desde C11
```

1) Lê de [stdin](<#/doc/io/std_streams>) para o array de caracteres apontado por `str` até que um caractere de nova linha seja encontrado ou o fim do arquivo ocorra. Um caractere nulo é escrito imediatamente após o último caractere lido no array. O caractere de nova linha é descartado, mas não armazenado no buffer.

2) Lê caracteres de [stdin](<#/doc/io/std_streams>) até que uma nova linha seja encontrada ou o fim do arquivo ocorra. Escreve no máximo `n - 1` caracteres no array apontado por `str`, e sempre escreve o caractere nulo terminador (a menos que `str` seja um ponteiro nulo). O caractere de nova linha, se encontrado, é descartado e não conta para o número de caracteres escritos no buffer.

Os seguintes erros são detectados em tempo de execução e chamam a função [constraint handler](<#/doc/error/set_constraint_handler_s>) atualmente instalada:

  * `n` é zero;
  * `n` é maior que `RSIZE_MAX`;
  * `str` é um ponteiro nulo;
  * `_endline_` ou `_eof_` não encontrados após armazenar `n - 1` caracteres no buffer.

Em qualquer caso, `gets_s` primeiro termina de ler e descartar os caracteres de [stdin](<#/doc/io/std_streams>) até o caractere de nova linha, condição de fim de arquivo ou erro de leitura antes de chamar o `constraint handler`.

Assim como todas as funções com verificação de limites (`bounds-checked functions`), `gets_s` só é garantida como disponível se `__STDC_LIB_EXT1__` for definido pela implementação e se o usuário definir `__STDC_WANT_LIB_EXT1__` para a constante inteira `1` antes de incluir [`<stdio.h>`](<#/doc/io>).

### Parâmetros

- **str** — um array de caracteres para onde os caracteres de [stdin](<#/doc/io/std_streams>) serão escritos
- **n** — número máximo de caracteres que podem ser escritos no array apontado por `str`

### Valor de retorno

`str` em caso de sucesso, um ponteiro nulo em caso de falha.

Se a falha foi causada pela condição de fim de arquivo, adicionalmente define o indicador `_eof_` (veja [feof()](<#/doc/io/feof>)) em [stdin](<#/doc/io/std_streams>). Se a falha foi causada por algum outro erro, define o indicador `_error_` (veja [ferror()](<#/doc/io/ferror>)) em [stdin](<#/doc/io/std_streams>).

### Notas

A função `gets()` não realiza verificação de limites (`bounds checking`), portanto, esta função é extremamente vulnerável a ataques de `buffer-overflow`. Ela não pode ser usada com segurança (a menos que o programa seja executado em um ambiente que restrinja o que pode aparecer em `stdin`). Por esta razão, a função foi descontinuada no terceiro corrigendum do padrão C99 e removida completamente no padrão C11. [fgets()](<#/doc/io/fgets>) e `gets_s()` são os substitutos recomendados.

**AVISO: Nunca use `gets()`.

### Referências

  * C23 padrão (ISO/IEC 9899:2024):

    

  * K.3.5.4.1 A função gets_s (p: TBD)

  * C17 padrão (ISO/IEC 9899:2018):

    

  * K.3.5.4.1 A função gets_s (p: TBD)

  * C11 padrão (ISO/IEC 9899:2011):

    

  * K.3.5.4.1 A função gets_s (p: 602-603)

  * C99 padrão (ISO/IEC 9899:1999):

    

  * 7.19.7.7 A função gets (p: 298)

  * C89/C90 padrão (ISO/IEC 9899:1990):

    

  * 4.9.7.7 A função gets

### Veja também

[ scanffscanfsscanfscanf_sfscanf_ssscanf_s](<#/doc/io/fscanf>)(C11)(C11)(C11) | lê entrada formatada de [stdin](<#/doc/io/std_streams>), um fluxo de arquivo ou um buffer
(função)
[ fgets](<#/doc/io/fgets>) | obtém uma string de caracteres de um fluxo de arquivo
(função)
[ fputs](<#/doc/io/fputs>) | escreve uma string de caracteres em um fluxo de arquivo
(função)
[ getlinegetwlinegetdelimgetwdelim](<#/doc/experimental/dynamic/getline>)(TR de memória dinâmica) | lê de um fluxo para um buffer redimensionado automaticamente até o delimitador/fim de linha
(função)
[Documentação C++](<#/>) para gets