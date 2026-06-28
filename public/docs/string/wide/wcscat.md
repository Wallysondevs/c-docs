# wcscat, wcscat_s

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
wchar_t *wcscat( wchar_t *dest, const wchar_t *src );  // desde C95
(até C99)  // até C99
wchar_t *wcscat( wchar_t *restrict dest, const wchar_t *restrict src );  // desde C99
errno_t wcscat_s( wchar_t *restrict dest, rsize_t destsz,
const wchar_t *restrict src );  // desde C11
```

  
1) Anexa uma cópia da string larga apontada por `src` ao final da string larga apontada por `dest`. O caractere largo `src[0]` substitui o terminador nulo no final de `dest`. A string larga resultante é terminada em nulo. O comportamento é indefinido se o array de destino não for grande o suficiente para o conteúdo de `str` e `dest` e o caractere largo nulo terminador. O comportamento é indefinido se as strings se sobrepuserem. 

2) O mesmo que (1), exceto que pode sobrescrever o restante do array de destino (do último caractere escrito até `destsz`) com valores não especificados e que os seguintes erros são detectados em tempo de execução e chamam a função [manipulador de restrição](<#/doc/error/set_constraint_handler_s>) atualmente instalada: 

    

  * `src` ou `dest` é um ponteiro nulo 
  * `destsz` é zero ou maior que RSIZE_MAX/sizeof(wchar_t)
  * não há terminador nulo nos primeiros `destsz` caracteres largos de `dest`
  * ocorreria truncamento (o espaço disponível no final de `dest` não seria suficiente para todos os caracteres largos, incluindo o terminador nulo, de `src`) 
  * ocorreria sobreposição entre as strings de origem e destino 

    Assim como todas as funções com verificação de limites, `wcscat_s` tem sua disponibilidade garantida apenas se __STDC_LIB_EXT1__ for definido pela implementação e se o usuário definir __STDC_WANT_LIB_EXT1__ para a constante inteira 1 antes de incluir [`<wchar.h>`](<#/doc/string/wide>).

### Parâmetros

dest  |  \-  |  ponteiro para a string larga terminada em nulo à qual anexar   
src  |  \-  |  ponteiro para a string larga terminada em nulo da qual copiar   
destsz  |  \-  |  número máximo de caracteres a serem escritos, tipicamente o tamanho do buffer de destino   
  
### Valor de retorno

1) retorna uma cópia de `dest`

2) retorna zero em caso de sucesso, retorna um valor diferente de zero em caso de erro. Além disso, em caso de erro, escreve L'\0' em dest[0] (a menos que `dest` seja um ponteiro nulo ou `destsz` seja zero ou maior que RSIZE_MAX/sizeof(wchar_t)).

### Exemplo

Execute este código
```c
    #include <wchar.h> 
    #include <stdio.h>
    #include <locale.h>
     
    int main(void) 
    {
        wchar_t str[50] = L"Земля, прощай.";
        wcscat(str, L" ");
        wcscat(str, L"В добрый путь.");
        setlocale(LC_ALL, "en_US.utf8");
        printf("%ls", str);
    }
```

Saída: 
```
    Земля, прощай. В добрый путь.
```

### Referências

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.29.4.3.1 A função wcscat (p: 315) 

    

  * K.3.9.2.2.1 A função wcscat_s (p: 466) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.29.4.3.1 A função wcscat (p: 432) 

    

  * K.3.9.2.2.1 A função wcscat_s (p: 642-643) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.24.4.3.1 A função wcscat (p: 378) 

### Veja também

[ wcsncatwcsncat_s](<#/doc/string/wide/wcsncat>)(C95)(C11) |  anexa uma certa quantidade de caracteres largos de uma string larga a outra   
(função)  
[ strcatstrcat_s](<#/doc/string/byte/strcat>)(C11) |  concatena duas strings   
(função)  
[ wcscpywcscpy_s](<#/doc/string/wide/wcscpy>)(C95)(C11) |  copia uma string larga para outra   
(função)  
[Documentação C++](<#/>) para wcscat