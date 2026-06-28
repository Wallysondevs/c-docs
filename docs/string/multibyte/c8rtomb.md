# c8rtomb

Definido no cabeçalho [`<uchar.h>`](<#/doc/string/multibyte>)

```c
size_t c8rtomb( char* restrict s, char8_t c8, mbstate_t* restrict ps );  // desde C23
```

Converte um único ponto de código de UTF-8 para uma representação de caractere multibyte estreita.

Se `s` não for um ponteiro nulo e `c8` for a última unidade de código em uma codificação UTF-8 válida de um ponto de código, a função determina o número de bytes necessários para armazenar a representação de caractere multibyte desse ponto de código (incluindo quaisquer sequências de mudança, e levando em consideração o estado de conversão multibyte atual *ps), e armazena a representação de caractere multibyte no array de caracteres cujo primeiro elemento é apontado por `s`, atualizando *ps conforme necessário. No máximo MB_CUR_MAX bytes podem ser escritos por esta função.

Se `c8` não for a unidade de código UTF-8 final em uma representação de um ponto de código, a função não escreve no array apontado por `s`, apenas *ps é atualizado.

Se `s` for um ponteiro nulo, a chamada é equivalente a c8rtomb(buf, u8'\0', ps) para algum buffer interno `buf`.

Se `c8` for o caractere nulo u8'\0', um byte nulo é armazenado, precedido por qualquer sequência de mudança necessária para restaurar o estado de mudança inicial e o parâmetro de estado de conversão *ps é atualizado para representar o estado de mudança inicial.

A codificação multibyte usada por esta função é especificada pela localidade C atualmente ativa.

### Parâmetros

- **s** — ponteiro para o array de caracteres estreitos onde o caractere multibyte será armazenado
- **c8** — a unidade de código UTF-8 a ser convertida
- **ps** — ponteiro para o objeto de estado de conversão usado ao interpretar a string multibyte

### Valor de retorno

O número de bytes armazenados no objeto array (incluindo quaisquer sequências de mudança). Isso pode ser zero quando c8 não é a unidade de código final na representação UTF-8 de um ponto de código.

Se c8 for inválido (não contribui para uma sequência de char8_t correspondente a um caractere multibyte válido), o valor da macro [EILSEQ](<#/doc/error/errno_macros>) é armazenado em [errno](<#/doc/error/errno>), ([size_t](<#/doc/types/size_t>))-1 é retornado, e o estado de conversão é não especificado.

### Notas

Chamadas para `c8rtomb` com um argumento de ponteiro nulo para s podem introduzir uma condição de corrida (data race) com outras chamadas para `c8rtomb` com um argumento de ponteiro nulo para s.

### Exemplo

| Esta seção está incompleta
Razão: sem exemplo

### Ver também

[ mbrtoc8](<#/doc/string/multibyte/mbrtoc8>)(C23) | converte um caractere multibyte estreito para codificação UTF-8
(função)
[Documentação C++](<#/>) para c8rtomb