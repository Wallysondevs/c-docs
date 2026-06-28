# Entrada/saída de arquivo

O cabeçalho `< stdio.h>` fornece suporte genérico para operações de arquivo e oferece funções com capacidades de entrada/saída de caracteres estreitos.

O cabeçalho [`<wchar.h>`](<#/doc/string/wide>) fornece funções com capacidades de entrada/saída de caracteres largos.

Fluxos de E/S são denotados por objetos do tipo [FILE](<#/doc/io/FILE>) que só podem ser acessados e manipulados através de ponteiros do tipo [FILE](<#/doc/io/FILE>)*. Cada fluxo está associado a um dispositivo físico externo (arquivo, fluxo de entrada padrão, impressora, porta serial, etc).

### Tipos

Definido no cabeçalho `<stdio.h>`
---
[ FILE](<#/doc/io/FILE>) | tipo de objeto, capaz de armazenar todas as informações necessárias para controlar um fluxo de E/S em C
(typedef)
[ fpos_t](<#/doc/io/fpos_t>) | tipo de objeto completo não-array, capaz de especificar unicamente uma posição e o estado do analisador multibyte em um arquivo
(typedef)

### Fluxos padrão predefinidos

Definido no cabeçalho `<stdio.h>`
---
[ stdinstdoutstderr](<#/doc/io/std_streams>) | expressão do tipo [FILE](<#/doc/io/FILE>)* associada ao fluxo de entrada
expressão do tipo [FILE](<#/doc/io/FILE>)* associada ao fluxo de saída
expressão do tipo [FILE](<#/doc/io/FILE>)* associada ao fluxo de saída de erro
(macro constante)

### Funções

##### Acesso a arquivos

---
Definido no cabeçalho `<stdio.h>`
[ fopenfopen_s](<#/doc/io/fopen>)(C11) | abre um arquivo
(função)
[ freopenfreopen_s](<#/doc/io/freopen>)(C11) | abre um fluxo existente com um nome diferente
(função)
[ fclose](<#/doc/io/fclose>) | fecha um arquivo
(função)
[ fflush](<#/doc/io/fflush>) | sincroniza um fluxo de saída com o arquivo real
(função)
[ setbuf](<#/doc/io/setbuf>) | define o buffer para um fluxo de arquivo
(função)
[ setvbuf](<#/doc/io/setvbuf>) | define o buffer e seu tamanho para um fluxo de arquivo
(função)
Definido no cabeçalho `[`<wchar.h>`](<#/doc/string/wide>)`
[ fwide](<#/doc/io/fwide>)(C95) | alterna um fluxo de arquivo entre E/S de caracteres largos e E/S de caracteres estreitos
(função)

##### Entrada/saída direta

Definido no cabeçalho `<stdio.h>`
[ fread](<#/doc/io/fread>) | lê de um arquivo
(função)
[ fwrite](<#/doc/io/fwrite>) | escreve em um arquivo
(função)

##### Entrada/saída não formatada

###### Caractere estreito

Definido no cabeçalho `<stdio.h>`
[ fgetcgetc](<#/doc/io/fgetc>) | obtém um caractere de um fluxo de arquivo
(função)
[ fgets](<#/doc/io/fgets>) | obtém uma string de caracteres de um fluxo de arquivo
(função)
[ fputcputc](<#/doc/io/putc>) | escreve um caractere em um fluxo de arquivo
(função)
[ fputs](<#/doc/io/fputs>) | escreve uma string de caracteres em um fluxo de arquivo
(função)
[ getchar](<#/doc/io/getchar>) | lê um caractere de [stdin](<#/doc/io/std_streams>)
(função)
[ getsgets_s](<#/doc/io/gets>)(removido em C11)(C11) | lê uma string de caracteres de [stdin](<#/doc/io/std_streams>)
(função)
[ putchar](<#/doc/io/putchar>) | escreve um caractere em [stdout](<#/doc/io/std_streams>)
(função)
[ puts](<#/doc/io/puts>) | escreve uma string de caracteres em [stdout](<#/doc/io/std_streams>)
(função)
[ ungetc](<#/doc/io/ungetc>) | devolve um caractere a um fluxo de arquivo
(função)

###### Caractere largo

Definido no cabeçalho `[`<wchar.h>`](<#/doc/string/wide>)`
[ fgetwcgetwc](<#/doc/io/fgetwc>)(C95) | obtém um caractere largo de um fluxo de arquivo
(função)
[ fgetws](<#/doc/io/fgetws>)(C95) | obtém uma string larga de um fluxo de arquivo
(função)
[ fputwcputwc](<#/doc/io/fputwc>)(C95) | escreve um caractere largo em um fluxo de arquivo
(função)
[ fputws](<#/doc/io/fputws>)(C95) | escreve uma string larga em um fluxo de arquivo
(função)
[ getwchar](<#/doc/io/getwchar>)(C95) | lê um caractere largo de [stdin](<#/doc/io/std_streams>)
(função)
[ putwchar](<#/doc/io/putwchar>)(C95) | escreve um caractere largo em [stdout](<#/doc/io/std_streams>)
(função)
[ ungetwc](<#/doc/io/ungetwc>)(C95) | devolve um caractere largo a um fluxo de arquivo
(função)

##### Entrada/saída formatada

###### Caractere estreito

Definido no cabeçalho `<stdio.h>`
[ scanffscanfsscanfscanf_sfscanf_ssscanf_s](<#/doc/io/fscanf>)(C11)(C11)(C11) | lê entrada formatada de [stdin](<#/doc/io/std_streams>), um fluxo de arquivo ou um buffer
(função)
[ vscanfvfscanfvsscanfvscanf_svfscanf_svsscanf_s](<#/doc/io/vfscanf>)(C99)(C99)(C99)(C11)(C11)(C11) | lê entrada formatada de [stdin](<#/doc/io/std_streams>), um fluxo de arquivo ou um buffer usando lista de argumentos variáveis
(função)
[ printffprintfsprintfsnprintfprintf_sfprintf_ssprintf_ssnprintf_s](<#/doc/io/fprintf>)(C99)(C11)(C11)(C11)(C11) | imprime saída formatada para [stdout](<#/doc/io/std_streams>), um fluxo de arquivo ou um buffer
(função)
[ vprintfvfprintfvsprintfvsnprintfvprintf_svfprintf_svsprintf_svsnprintf_s](<#/doc/io/vfprintf>)(C99)(C11)(C11)(C11)(C11) | imprime saída formatada para [stdout](<#/doc/io/std_streams>), um fluxo de arquivo ou um buffer usando lista de argumentos variáveis
(função)

###### Caractere largo

Definido no cabeçalho `[`<wchar.h>`](<#/doc/string/wide>)`
[ wscanffwscanfswscanfwscanf_sfwscanf_sswscanf_s](<#/doc/io/fwscanf>)(C95)(C95)(C95)(C11)(C11)(C11) | lê entrada formatada de caracteres largos de [stdin](<#/doc/io/std_streams>), um fluxo de arquivo ou um buffer
(função)
[ vwscanfvfwscanfvswscanfvwscanf_svfwscanf_svswscanf_s](<#/doc/io/vfwscanf>)(C99)(C99)(C99)(C11)(C11)(C11) | lê entrada formatada de caracteres largos de [stdin](<#/doc/io/std_streams>), um fluxo de arquivo ou um buffer usando lista de argumentos variáveis
(função)
[ wprintffwprintfswprintfwprintf_sfwprintf_sswprintf_ssnwprintf_s](<#/doc/io/fwprintf>)(C95)(C95)(C95)(C11)(C11)(C11)(C11) | imprime saída formatada de caracteres largos para [stdout](<#/doc/io/std_streams>), um fluxo de arquivo ou um buffer
(função)
[ vwprintfvfwprintfvswprintfvwprintf_svfwprintf_svswprintf_svsnwprintf_s](<#/doc/io/vfwprintf>)(C95)(C95)(C95)(C11)(C11)(C11)(C11) | imprime saída formatada de caracteres largos para [stdout](<#/doc/io/std_streams>), um fluxo de arquivo ou um buffer usando lista de argumentos variáveis
(função)

##### Posicionamento de arquivo

Definido no cabeçalho `<stdio.h>`
[ ftell](<#/doc/io/ftell>) | retorna o indicador de posição atual do arquivo
(função)
[ fgetpos](<#/doc/io/fgetpos>) | obtém o indicador de posição do arquivo
(função)
[ fseek](<#/doc/io/fseek>) | move o indicador de posição do arquivo para um local específico em um arquivo
(função)
[ fsetpos](<#/doc/io/fsetpos>) | move o indicador de posição do arquivo para um local específico em um arquivo
(função)
[ rewind](<#/doc/io/rewind>) | move o indicador de posição do arquivo para o início em um arquivo
(função)

##### Tratamento de erros

Definido no cabeçalho `<stdio.h>`
[ clearerr](<#/doc/io/clearerr>) | limpa erros
(função)
[ feof](<#/doc/io/feof>) | verifica o fim do arquivo
(função)
[ ferror](<#/doc/io/ferror>) | verifica um erro de arquivo
(função)
[ perror](<#/doc/io/perror>) | exibe uma string de caracteres correspondente ao erro atual em [stderr](<#/doc/io/std_streams>)
(função)

##### Operações em arquivos

Definido no cabeçalho `<stdio.h>`
[ remove](<#/doc/io/remove>) | apaga um arquivo
(função)
[ rename](<#/doc/io/rename>) | renomeia um arquivo
(função)
[ tmpfiletmpfile_s](<#/doc/io/tmpfile>)(C11) | retorna um ponteiro para um arquivo temporário
(função)
[ tmpnamtmpnam_s](<#/doc/io/tmpnam>)(C11) | retorna um nome de arquivo único
(função)

### Constantes de macro

Definido no cabeçalho `<stdio.h>`
---
EOF | expressão constante inteira do tipo int e valor negativo
(macro constante)
FOPEN_MAX | número máximo de arquivos que podem ser abertos simultaneamente
(macro constante)
FILENAME_MAX | tamanho necessário para um array de char para armazenar o nome de arquivo mais longo suportado
(macro constante)
BUFSIZ | tamanho do buffer usado por [setbuf](<#/doc/io/setbuf>)
(macro constante)
_IOFBF_IOLBF_IONBF | argumento para [setvbuf](<#/doc/io/setvbuf>) indicando E/S totalmente armazenada em buffer
argumento para [setvbuf](<#/doc/io/setvbuf>) indicando E/S armazenada em buffer por linha
argumento para [setvbuf](<#/doc/io/setvbuf>) indicando E/S não armazenada em buffer
(macro constante)
SEEK_SETSEEK_CURSEEK_END | argumento para [fseek](<#/doc/io/fseek>) indicando busca a partir do início do arquivo
argumento para [fseek](<#/doc/io/fseek>) indicando busca a partir da posição atual do arquivo
argumento para [fseek](<#/doc/io/fseek>) indicando busca a partir do fim do arquivo
(macro constante)
TMP_MAXTMP_MAX_S(C11) | número máximo de nomes de arquivo únicos que podem ser gerados por [tmpnam](<#/doc/io/tmpnam>)
número máximo de nomes de arquivo únicos que podem ser gerados por tmpnam_s
(macro constante)
L_tmpnamL_tmpnam_s(C11) | tamanho necessário para um array de char para armazenar o resultado de [tmpnam](<#/doc/io/tmpnam>)
tamanho necessário para um array de char para armazenar o resultado de tmpnam_s
(macro constante)

### Referências

  * Padrão C23 (ISO/IEC 9899:2024):

    

  * 7.21 Entrada/saída <stdio.h> (p: TBD)

    

  * 7.29 Utilitários estendidos de caracteres multibyte e largos <wchar.h> (p: TBD)

    

  * 7.31.11 Entrada/saída <stdio.h> (p: TBD)

    

  * 7.31.16 Utilitários estendidos de caracteres multibyte e largos <wchar.h> (p: TBD)

    

  * K.3.5 Entrada/saída <stdio.h> (p: TBD)

  * Padrão C17 (ISO/IEC 9899:2018):

    

  * 7.21 Entrada/saída <stdio.h> (p: TBD)

    

  * 7.29 Utilitários estendidos de caracteres multibyte e largos <wchar.h> (p: TBD)

    

  * 7.31.11 Entrada/saída <stdio.h> (p: TBD)

    

  * 7.31.16 Utilitários estendidos de caracteres multibyte e largos <wchar.h> (p: TBD)

    

  * K.3.5 Entrada/saída <stdio.h> (p: TBD)

  * Padrão C11 (ISO/IEC 9899:2011):

    

  * 7.21 Entrada/saída <stdio.h> (p: 296-339)

    

  * 7.29 Utilitários estendidos de caracteres multibyte e largos <wchar.h> (p: 402-446)

    

  * 7.31.11 Entrada/saída <stdio.h> (p: 456)

    

  * 7.31.16 Utilitários estendidos de caracteres multibyte e largos <wchar.h> (p: 456)

    

  * K.3.5 Entrada/saída <stdio.h> (p: 586-603)

  * Padrão C99 (ISO/IEC 9899:1999):

    

  * 7.19 Entrada/saída <stdio.h> (p: 262-305)

    

  * 7.24 Utilitários estendidos de caracteres multibyte e largos <wchar.h> (p: 348-392)

    

  * 7.26.9 Entrada/saída <stdio.h> (p: 402)

    

  * 7.26.12 Utilitários estendidos de caracteres multibyte e largos <wchar.h> (p: 402)

  * Padrão C89/C90 (ISO/IEC 9899:1990):

    

  * 4.9 ENTRADA/SAÍDA <stdio.h>

    

  * 4.13.6 Entrada/saída <stdio.h>

### Veja também

[documentação C++](<#/>) para entrada/saída de arquivo estilo C
---