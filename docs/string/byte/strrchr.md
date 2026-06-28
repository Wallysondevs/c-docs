# strrchr

Definido no cabeçalho [`<string.h>`](<#/doc/string/byte>)

```c
char* strrchr( const char* str, int ch );
/*QChar*/* strrchr( /*QChar*/* str, int ch );  // desde C23
```

  
1) Encontra a última ocorrência de ch (após conversão para char como se por (char)ch) na string de bytes terminada em nulo apontada por str (cada caractere interpretado como unsigned char). O caractere nulo terminador é considerado parte da string e pode ser encontrado se a busca for por '\0'.

2) Função genérica de tipo equivalente a (1). Seja `T` um tipo de objeto caractere não qualificado. 

    

  * Se `str` for do tipo const T*, o tipo de retorno é const char*. 
  * Caso contrário, se `str` for do tipo T*, o tipo de retorno é char*. 
  * Caso contrário, o comportamento é indefinido. 

Se uma definição de macro de cada uma dessas funções genéricas for suprimida para acessar uma função real (por exemplo, se (strrchr) ou um ponteiro de função for usado), a declaração de função real (1) torna-se visível.

O comportamento é indefinido se str não for um ponteiro para uma string de bytes terminada em nulo. 

### Parâmetros

str  |  \-  |  ponteiro para a string de bytes terminada em nulo a ser analisada   
ch  |  \-  |  caractere a ser procurado   
  
### Valor de retorno

Ponteiro para o caractere encontrado em str, ou ponteiro nulo se nenhum caractere for encontrado. 

### Exemplo

Execute este código
```
    #include <stdio.h>
    #include <string.h>
     
    int main(void)
    {
        char szSomeFileName[] = "foo/bar/foobar.txt";
        char* pLastSlash = strrchr(szSomeFileName, '/');
        char* pszBaseName = pLastSlash ? pLastSlash + 1 : szSomeFileName;
        printf("Base Name: %s", pszBaseName);
    }
```

Saída: 
```
    Base Name: foobar.txt
```

### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.24.5.5 A função strrchr (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.24.5.5 A função strrchr (p: TBD) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.24.5.5 A função strrchr (p: 368-369) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.21.5.5 A função strrchr (p: 331) 

  * Padrão C89/C90 (ISO/IEC 9899:1990): 

    

  * 4.11.5.5 A função strrchr 

### Veja também

[ strchr](<#/doc/string/byte/strchr>) |  encontra a primeira ocorrência de um caractere   
(função)  
[ strpbrk](<#/doc/string/byte/strpbrk>) |  encontra a primeira localização de qualquer caractere em uma string, em outra string   
(função)  
[Documentação C++](<#/>) para strrchr