# fflush

Definido no cabeçalho [`<stdio.h>`](<#/doc/io>)

```c
int fflush( FILE* stream );
```

Para fluxos de saída (e para fluxos de atualização nos quais a última operação foi de saída), escreve quaisquer dados não gravados do buffer do fluxo para o dispositivo de saída associado.

Para fluxos de entrada (e para fluxos de atualização nos quais a última operação foi de entrada), o comportamento é indefinido.

Se stream for um ponteiro nulo, todos os fluxos de saída abertos são descarregados (flushed), incluindo aqueles manipulados dentro de pacotes de biblioteca ou que não são diretamente acessíveis ao programa.

### Parâmetros

- **stream** — o fluxo de arquivo a ser gravado

### Valor de retorno

Retorna zero em caso de sucesso. Caso contrário, [EOF](<#/doc/io>) é retornado e o indicador de erro do fluxo de arquivo é definido.

### Notas

POSIX [estende a especificação de fflush](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/fflush.html>) definindo seus efeitos em um fluxo de entrada, desde que esse fluxo represente um arquivo ou outro dispositivo pesquisável (seekable): nesse caso, o ponteiro de arquivo POSIX é reposicionado para corresponder ao ponteiro de fluxo C (o que efetivamente desfaz qualquer buffer de leitura) e os efeitos de qualquer [ungetc](<#/doc/io/ungetc>) ou [ungetwc](<#/doc/io/ungetwc>) que ainda não foram lidos de volta do fluxo são descartados.

A Microsoft também estende a especificação de fflush definindo seus efeitos em um fluxo de entrada: no Visual Studio 2013 e anteriores, ele [descartava o buffer de entrada](<https://docs.microsoft.com/en-us/previous-versions/visualstudio/visual-studio-2013/9yky46tz\(v=vs.120\)>), no Visual Studio 2015 e mais recentes, ele [não tem efeito, os buffers são retidos](<https://msdn.microsoft.com/en-us/library/9yky46tz.aspx>).

### Referências

* Padrão C23 (ISO/IEC 9899:2024):

* 7.21.5.2 A função fflush (p: TBD)

* Padrão C17 (ISO/IEC 9899:2018):

* 7.21.5.2 A função fflush (p: TBD)

* Padrão C11 (ISO/IEC 9899:2011):

* 7.21.5.2 A função fflush (p: 305)

* Padrão C99 (ISO/IEC 9899:1999):

* 7.19.5.2 A função fflush (p: 270-271)

* Padrão C89/C90 (ISO/IEC 9899:1990):

* 4.9.5.2 A função fflush

### Veja também

[ fopenfopen_s](<#/doc/io/fopen>)(C11) | abre um arquivo
(função)
[ fclose](<#/doc/io/fclose>) | fecha um arquivo
(função)
[Documentação C++](<#/>) para fflush