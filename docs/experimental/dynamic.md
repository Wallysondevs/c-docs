# Extensões de memória dinâmica

Extensões à Biblioteca C Parte II: Funções de Alocação Dinâmica, ISO/IEC TR 24731-2:2010, define os seguintes novos componentes para a biblioteca padrão C:

__STDC_ALLOC_LIB__ | constante inteira do tipo long indicando o nível de conformidade
(macro constante) |
Definido no cabeçalho `[`<stdio.h>`](<#/doc/io>)`
[ fmemopen](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/dynamic/fmemopen&action=edit&redlink=1> "c/experimental/dynamic/fmemopen \(page does not exist\)")(dynamic memory TR) | abre um buffer de memória de tamanho fixo como um fluxo de E/S
(função) |
[ open_memstreamopen_wmemstream](<https://en.cppreference.com/mwiki/index.php?title=c/experimental/dynamic/open_memstream&action=edit&redlink=1> "c/experimental/dynamic/open memstream \(page does not exist\)")(dynamic memory TR) | abre um buffer de memória redimensionado dinamicamente como um fluxo de E/S
(função) |
[ asprintfaswprintfvasprintfvaswprintf](<#/doc/experimental/dynamic/asprintf>)(dynamic memory TR) | variantes de [sprintf](<#/doc/io/fprintf>) etc que escrevem em um buffer alocado automaticamente e retornam um ponteiro para ele
(função) |
[ getlinegetwlinegetdelimgetwdelim](<#/doc/experimental/dynamic/getline>)(dynamic memory TR) | lê de um fluxo para um buffer redimensionado automaticamente até o delimitador/fim da linha
(função) |
Definido no cabeçalho `[`<string.h>`](<#/doc/string/byte>)`
[ strdup](<#/doc/experimental/dynamic/strdup>)(dynamic memory TR) | aloca uma cópia de uma string
(função) |
[ strndup](<#/doc/experimental/dynamic/strndup>)(dynamic memory TR) | aloca uma cópia de uma string até o tamanho especificado
(função) |

Esta extensão de biblioteca também introduz o caractere de alocação por atribuição `m` para uso com os especificadores de conversão `%s`, `%[` e `%c` na família de funções [fscanf](<#/doc/io/fscanf>) e [fwscanf](<#/doc/io/fwscanf>).

### Notas

As funções `fmemopen`, `open_memstream`, `open_wmemstream`, `getdelim`, `getline`, `strdup`, `strndup` e as extensões para `fscanf` estão disponíveis em [POSIX (ISO/IEC 9945:2003)](<http://pubs.opengroup.org/onlinepubs/9699919799/>).

As funções `asprintf` e `vasprintf` estão disponíveis na Linux Standard Base (ISO/IEC IS 23360:2006).