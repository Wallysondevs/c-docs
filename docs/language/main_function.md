# Função main

Todo programa C codificado para ser executado em um ambiente de execução hospedado contém a definição (não o protótipo) de uma função chamada `main`, que é o início designado do programa.

---
int `main` `(void)` `{` body `}` | (1) |
int `main` `(` int argc`,` char *argv[]`)` `{` body `}` | (2) |
/* outra assinatura definida pela implementação */ (desde C99) | (3) |

### Parâmetros

- **argc** — Valor não negativo que representa o número de argumentos passados para o programa a partir do ambiente em que o programa é executado.
- **argv** — Ponteiro para o primeiro elemento de um array de argc + 1 ponteiros, dos quais o último é nulo e os anteriores, se houver, apontam para strings que representam os argumentos passados para o programa a partir do ambiente hospedeiro. Se argv[0] não for um ponteiro nulo (ou, equivalentemente, se argc > 0), ele aponta para uma string que representa o nome do programa, que é vazia se o nome do programa não estiver disponível no ambiente hospedeiro.

Os nomes `argc` e `argv` significam "contagem de argumentos" e "vetor de argumentos", e são tradicionalmente usados, mas outros nomes podem ser escolhidos para os parâmetros, assim como declarações de tipo diferentes, mas equivalentes: int main(int ac, char** av) é igualmente válido.

Uma forma comum de main definida pela implementação é int main(int argc, char *argv[], char *envp[]), onde um terceiro argumento, do tipo char**, apontando para [um array de ponteiros para as _variáveis de ambiente de execução_](<https://pubs.opengroup.org/onlinepubs/9699919799/functions/exec.html>), é adicionado.

### Valor de retorno

Se a instrução return for usada, o valor de retorno é usado como argumento para a chamada implícita a [exit()](<#/doc/program/exit>) (veja abaixo para detalhes). Os valores zero e [EXIT_SUCCESS](<#/doc/program/EXIT_status>) indicam terminação bem-sucedida, o valor [EXIT_FAILURE](<#/doc/program/EXIT_status>) indica terminação mal-sucedida.

### Explicação

A função `main` é chamada na inicialização do programa, depois que todos os objetos com duração de armazenamento estática são inicializados. É o ponto de entrada designado para um programa que é executado em um ambiente _hospedado_ (ou seja, com um sistema operacional). O nome e o tipo do ponto de entrada para qualquer programa _autônomo_ (carregadores de boot, kernels de SO, etc.) são definidos pela implementação.

Os parâmetros da forma de dois parâmetros da função main permitem que strings de caracteres multibyte arbitrárias sejam passadas do ambiente de execução (estas são tipicamente conhecidas como _argumentos de linha de comando_). Os ponteiros argv[1] .. argv[argc-1] apontam para os primeiros caracteres de cada uma dessas strings. argv[0] (se não for nulo) é o ponteiro para o caractere inicial de uma string multibyte terminada em nulo que representa o nome usado para invocar o próprio programa (ou, se isso não for suportado pelo ambiente hospedeiro, argv[0][0] é garantido ser zero).

Se o ambiente hospedeiro não puder fornecer letras maiúsculas e minúsculas, os argumentos da linha de comando são convertidos para minúsculas.

As strings são modificáveis, e quaisquer modificações feitas persistem até a terminação do programa, embora essas modificações não se propaguem de volta para o ambiente hospedeiro: elas podem ser usadas, por exemplo, com [strtok](<#/doc/string/byte/strtok>).

O tamanho do array apontado por `argv` é de pelo menos `argc+1`, e o último elemento, `argv[argc]`, é garantido ser um ponteiro nulo.

A função `main` possui várias propriedades especiais:

1) Um protótipo para esta função não pode ser fornecido pelo programa.

2) Se o tipo de retorno da função main for [compatível](<#/doc/language/compatible_type>) com int, então o retorno da chamada inicial a main (mas não o retorno de qualquer chamada subsequente, recursiva) é equivalente à execução da função [exit](<#/doc/program/exit>), com o valor que a função main está retornando passado como argumento (o que então chama as funções registradas com [atexit](<#/doc/program/atexit>), descarrega e fecha todos os streams, e deleta os arquivos criados com [tmpfile](<#/doc/io/tmpfile>), e retorna o controle para o ambiente de execução).

3) Se a função main executa um return que não especifica valor ou, o que é o mesmo, atinge o } de terminação sem executar um return, o status de terminação retornado ao ambiente hospedeiro é comportamento indefinido. | (até C99)
Se o tipo de retorno da função main não for [compatível](<#/doc/language/compatible_type>) com int (por exemplo, void main(void)), o valor retornado ao ambiente hospedeiro é não especificado. Se o tipo de retorno for compatível com int e o controle atingir o } de terminação, o valor retornado ao ambiente é o mesmo que se estivesse executando return 0;. | (desde C99)

### Exemplo

Demonstra como informar um programa sobre onde encontrar sua entrada e onde escrever seus resultados. Invocação: ./a.out indatafile outdatafile

Execute este código
```c
    #include <stdio.h>
    
    int main(int argc, char *argv[])
    {
        printf("argc = %d\n", argc);
        for (int ndx = 0; ndx != argc; ++ndx)
            printf("argv[%d] --> %s\n", ndx, argv[ndx]);
        printf("argv[argc] = %p\n", (void*)argv[argc]);
    }
```

Saída possível:
```
    argc = 3
    argv[0] --> ./a.out
    argv[1] --> indatafile
    argv[2] --> outdatafile
    argv[argc] = (nil)
```

### Referências

* C23 standard (ISO/IEC 9899:2024):

  * 5.1.2.2.1 Program startup (p: TBD)

* C17 standard (ISO/IEC 9899:2018):

  * 5.1.2.2.1 Program startup (p: 10-11)

* C11 standard (ISO/IEC 9899:2011):

  * 5.1.2.2.1 Program startup (p: 13)

* C99 standard (ISO/IEC 9899:1999):

  * 5.1.2.2.1 Program startup (p: 12)

* C89/C90 standard (ISO/IEC 9899:1990):

  * 5.1.2.2 Hosted environment

### Veja também

[Documentação C++](<#/>) para a função `main`
---