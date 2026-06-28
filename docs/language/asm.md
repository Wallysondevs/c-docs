# Assembly inline

Assembly inline (tipicamente introduzido pela palavra-chave `asm`) oferece a capacidade de embutir código-fonte em linguagem assembly dentro de um programa C.

Ao contrário do C++, o assembly inline é tratado como uma extensão em C. Ele é suportado condicionalmente e definido pela implementação, o que significa que pode não estar presente e, mesmo quando fornecido pela implementação, não possui um significado fixo.

### Sintaxe

`asm (` string_literal `)` `;`
| Esta seção está incompleta
Razão: escrever uma nota sobre a sintaxe de assembly estendida do GCC, já que agora é suportada por Intel, IBM, Sun (a partir da v12), etc

### Explicação

Este tipo de sintaxe de assembly inline é aceito pelo padrão C++ e é chamado de _asm-declaration_ em C++. O `string_literal` é tipicamente um pequeno programa escrito em linguagem assembly, que é executado sempre que esta declaração é executada. Diferentes compiladores C possuem regras muito variadas para `asm-declarations`, e diferentes convenções para a interação com o código C circundante.

`asm-declaration` pode aparecer dentro de um bloco (corpo de uma função ou outra instrução composta) e, como todas as outras declarações, esta declaração também pode aparecer fora de um bloco.

### Notas

O MSVC não suporta assembly inline em processadores ARM e x64, e suporta apenas a forma introduzida por `__asm` em processadores x86.

Ao compilar no modo ISO C pelo GCC ou Clang (por exemplo, com a opção `-std=c11`), `__asm__` deve ser usado em vez de `asm`.

### Exemplos

Demonstra dois tipos de sintaxe de assembly inline oferecidos pelo compilador GCC. Este programa funcionará corretamente apenas na plataforma x86-64 sob Linux. Note que o "assembly inline padrão" também é tratado como uma extensão no padrão C.

Execute este código
```c
    #include <stdio.h>
    
    extern int func(void);
    // the definition of func is written in assembly language
    __asm__(".globl func\n\t"
            ".type func, @function\n\t"
            "func:\n\t"
            ".cfi_startproc\n\t"
            "movl $7, %eax\n\t"
            "ret\n\t"
            ".cfi_endproc");
    
    int main(void)
    {
        int n = func();
        // gcc's extended inline assembly
        __asm__ ("leal (%0,%0,4),%0"
               : "=r" (n)
               : "0" (n));
        printf("7*5 = %d\n", n);
        fflush(stdout); // flush is intentional
    
        // standard inline assembly in C++
        __asm__ ("movq $60, %rax\n\t" // the exit syscall number on Linux
                 "movq $2,  %rdi\n\t" // this program returns 2
                 "syscall");
    }
```

Output:
```
    7*5 = 35
```

### Referências

  * C23 standard (ISO/IEC 9899:2024):

    

  * J.5.10 A palavra-chave `asm` (p: A definir)

  * C17 standard (ISO/IEC 9899:2018):

    

  * J.5.10 A palavra-chave `asm` (p: 422)

  * C11 standard (ISO/IEC 9899:2011):

    

  * J.5.10 A palavra-chave `asm` (p: 580)

  * C99 standard (ISO/IEC 9899:1999):

    

  * J.5.10 A palavra-chave `asm` (p: 512)

  * C89/C90 standard (ISO/IEC 9899:1990):

    

  * G.5.10 A palavra-chave `asm`

### Veja também

[Documentação C++](<#/>) para a declaração `asm`
---

### Links externos

1.  | [GCC Inline Assembly HOWTO](<https://www.ibiblio.org/gferg/ldp/GCC-Inline-Assembly-HOWTO.html>)
2.  | [IBM XL C/C++ Inline Assembly](<https://pic.dhe.ibm.com/infocenter/comphelp/v121v141/topic/com.ibm.xlcpp121.aix.doc/language_ref/asm.html>)
3.  | [Intel C++ Inline Assembly](<https://software.intel.com/en-us/cpp-compiler-developer-guide-and-reference-inline-assembly>)
4.  | [Visual Studio Inline Assembler](<https://learn.microsoft.com/en-us/cpp/assembler/inline/inline-assembler.aspx>)
5.  | [Sun Studio 12 Asm Statements](<https://blogs.oracle.com/x86be/entry/gcc_style_asm_inlining_support>)
6.  | [Inline assembly for Itanium-based HP-UX](<https://h21007.www2.hp.com/portal/site/dspp/menuitem.863c3e4cbcdc3f3515b49c108973a801?ciid=4308e2f5bde02110e2f5bde02110275d6e10RCRD>)