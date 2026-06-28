# fgetws

Definido no cabeçalho [`<wchar.h>`](<#/doc/string/wide>)

```c
wchar_t* fgetws( wchar_t* str, int count, FILE* stream );  // desde C95
(ate C99)  // ate C99
wchar_t* fgetws( wchar_t* restrict str, int count, FILE* restrict stream );  // desde C99
```

  
Lê no máximo `count - 1` caracteres largos do fluxo de arquivo fornecido e os armazena em `str`. A string larga produzida é sempre terminada em nulo. A análise para se o fim do arquivo (EOF) for encontrado ou se um caractere largo de nova linha for encontrado, caso em que `str` conterá esse caractere largo de nova linha.

### Parâmetros

str  |  \-  |  string larga para onde ler os caracteres   
count  |  \-  |  o comprimento de `str`  
stream  |  \-  |  fluxo de arquivo de onde ler os dados   
  
### Valor de retorno

`str` em caso de sucesso, um ponteiro nulo em caso de erro.

### Exemplo

| Esta seção está incompleta  
Razão: nenhum exemplo   
  
### Referências

  * Padrão C23 (ISO/IEC 9899:2024): 

    

  * 7.29.3.2 A função fgetws (p: TBD) 

  * Padrão C17 (ISO/IEC 9899:2018): 

    

  * 7.29.3.2 A função fgetws (p: TBD) 

  * Padrão C11 (ISO/IEC 9899:2011): 

    

  * 7.29.3.2 A função fgetws (p: 422) 

  * Padrão C99 (ISO/IEC 9899:1999): 

    

  * 7.24.3.2 A função fgetws (p: 367-368) 

### Veja também

[ wscanffwscanfswscanfwscanf_sfwscanf_sswscanf_s](<#/doc/io/fwscanf>)(C95)(C95)(C95)(C11)(C11)(C11) |  lê entrada formatada de caracteres largos de [stdin](<#/doc/io/std_streams>), um fluxo de arquivo ou um buffer   
(função)  
[ fgetwcgetwc](<#/doc/io/fgetwc>)(C95) |  obtém um caractere largo de um fluxo de arquivo   
(função)  
[ fputws](<#/doc/io/fputws>)(C95) |  escreve uma string larga em um fluxo de arquivo   
(função)  
[ getlinegetwlinegetdelimgetwdelim](<#/doc/experimental/dynamic/getline>)(dynamic memory TR) |  lê de um fluxo para um buffer redimensionado automaticamente até o delimitador/fim da linha   
(função)  
[Documentação C++](<#/>) para fgetws