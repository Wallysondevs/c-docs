# wcsncat, wcsncat_s

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
wchar_t *wcsncat( wchar_t *dest, const wchar_t *src, size_t count );  // desde C95
(até C99)  // até C99
wchar_t *wcsncat( wchar_t *restrict dest,
const wchar_t *restrict src, size_t count );  // desde C99
errno_t wcsncat_s( wchar_t *restrict dest, rsize_t destsz,
const wchar_t *restrict src, rsize_t count );  // desde C11
```

1) Anexa no máximo `count` caracteres largos da string larga apontada por `src`, parando se o terminador nulo for copiado, ao final da string de caracteres apontada por `dest`. O caractere largo src[0] substitui o terminador nulo no final de `dest`. O terminador nulo é sempre anexado no final (portanto, o número máximo de caracteres largos que a função pode escrever é count+1).

O comportamento é indefinido se o array de destino não for grande o suficiente para o conteúdo de `str` e `dest` e o caractere largo nulo terminador.

O comportamento é indefinido se as strings se sobrepuserem.

2) O mesmo que (1), exceto que esta função pode sobrescrever o restante do array de destino (do último caractere largo escrito até `destsz`) e que os seguintes erros são detectados em tempo de execução e chamam a função [manipulador de restrição](<#/doc/error/set_constraint_handler_s>) atualmente instalada:

  * `src` ou `dest` é um ponteiro nulo
  * `destsz` ou `count` é zero ou maior que RSIZE_MAX/sizeof(wchar_t)
  * não há caractere largo nulo nos primeiros `destsz` caracteres largos de `dest`
  * ocorreria truncamento: `count` ou o comprimento de `src`, o que for menor, excede o espaço disponível entre o terminador nulo de `dest` e `destsz`.
  * ocorreria sobreposição entre as strings de origem e destino

Assim como todas as funções com verificação de limites, `wcsncat_s` tem sua disponibilidade garantida apenas se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir `[`<wchar.h>`](<#/doc/string/wide>)`.

### Parâmetros

- **dest** — ponteiro para a string larga terminada em nulo à qual anexar
- **src** — ponteiro para a string larga terminada em nulo da qual copiar
- **count** — número máximo de caracteres largos a copiar
- **destsz** — o tamanho do buffer de destino

### Valor de retorno

1) retorna uma cópia de `dest`

2) retorna zero em caso de sucesso, retorna diferente de zero em caso de erro. Além disso, em caso de erro, escreve L'\0' em dest[0] (a menos que `dest` seja um ponteiro nulo ou `destsz` seja zero ou maior que RSIZE_MAX/sizeof(wchar_t)).

### Notas

Embora o truncamento para caber no buffer de destino seja um risco de segurança e, portanto, uma violação das restrições de tempo de execução para `wcsncat_s`, é possível obter o comportamento de truncamento especificando `count` igual ao tamanho do array de destino menos um: ele copiará os primeiros `count` caracteres largos e anexará o terminador nulo como sempre: wcsncat_s(dst, sizeof dst/sizeof *dst, src, (sizeof dst/sizeof *dst)-wcsnlen_s(dst, sizeof dst/sizeof *dst)-1);

### Exemplo

Execute este código
```c
    #include <wchar.h> 
    #include <stdio.h>
    #include <locale.h>
     
    int main(void) 
    {
        wchar_t str[50] = L"Земля, прощай.";
        wcsncat(str, L" ", 1);
        wcsncat(str, L"В добрый путь.", 8); // only append the first 8 wide chars
        setlocale(LC_ALL, "en_US.utf8");
        printf("%ls", str);
    }
```

Saída possível:
```
    Земля, прощай. В добрый
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018):

    * 7.29.4.3.2 A função wcsncat (p: 315)

    * K.3.9.2.2.2 A função wcsncat_s (p: 466-467)

  * Padrão C11 (ISO/IEC 9899:2011):

    * 7.29.4.3.2 A função wcsncat (p: 432-433)

    * K.3.9.2.2.2 A função wcsncat_s (p: 643-644)

  * Padrão C99 (ISO/IEC 9899:1999):

    * 7.24.4.3.2 A função wcsncat (p: 378-379)

### Veja também

[ wcscatwcscat_s](<#/doc/string/wide/wcscat>)(C95)(C11) | anexa uma cópia de uma string larga a outra
(função)
[ strncatstrncat_s](<#/doc/string/byte/strncat>)(C11) | concatena uma certa quantidade de caracteres de duas strings
(função)
[ wcscpywcscpy_s](<#/doc/string/wide/wcscpy>)(C95)(C11) | copia uma string larga para outra
(função)
[documentação C++](<#/>) para wcsncat