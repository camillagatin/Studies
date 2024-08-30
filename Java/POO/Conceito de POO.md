**Baixo nível**: São linguagens que estão mais próximas, da interpretação da máquina, diante do algoritmo desenvolvido. Exemplo: **Linguagem Assembly e C**.

**Alto nível**: São linguagens que disponibilizam, uma proposta de sintaxe (forma de escrever processos para serem executados pelo computador) mais próxima de interpretação humana. Exemplo: **Java, JavaScript, Python e C++**

Exemplo de um simples `Hello World` em **Assembly** versus **Python**:
```assembly
section	.text

   global _start   

_start: 

   mov	edx, len  

   mov	ecx, msg  

   mov	ebx, 1 

   mov	eax, 4  

   int	0x80   

   mov	eax, 1 

   int	0x80   

section	.data

msg	db	'Hello, world!',0xa

len	equ	$ - msg
```

```python
print('Hello, world!')
```

---
### Programação estruturada

**A programação estruturada** é um [paradigma de programação](https://stringfixer.com/pt/Programming_paradigm), que visa melhorar a clareza, a qualidade e o tempo de desenvolvimento de um [programa de computador,](https://stringfixer.com/pt/Computer_program) fazendo uso extensivo, das construções de fluxo de controle estruturado de seleção ( [if / then / else](https://stringfixer.com/pt/Conditional_(computer_programming)) ) e repetição (while e [for](https://stringfixer.com/pt/For_loop) ), [estruturas de bloco](https://stringfixer.com/pt/Block_(programming)) e [sub](https://stringfixer.com/pt/Subroutines) - [rotinas](https://stringfixer.com/pt/Subroutines) .

O que devemos ter em mente, é que na programação estruturada, implementamos algoritmos com estruturas sequenciais denominados de procedimentos lineares, podendo afetar o valor das variáveis de escopo local ou global em uma aplicação.

### Programação orientada a objetos

POO é um [paradigma de programação](https://pt.wikipedia.org/wiki/Paradigma_de_programa%C3%A7%C3%A3o), baseado no conceito de "[objetos](https://pt.wikipedia.org/wiki/Objeto_(ci%C3%AAncia_da_computa%C3%A7%C3%A3o))", que podem conter [dados](https://pt.wikipedia.org/wiki/Dados) na forma de [campos](https://pt.wikipedia.org/wiki/Campo_(ci%C3%AAncia_da_computa%C3%A7%C3%A3o)), também conhecidos como _atributos_, e códigos, na forma de [procedimentos](https://pt.wikipedia.org/wiki/Procedimento), também conhecidos como [métodos](https://pt.wikipedia.org/wiki/M%C3%A9todo_(programa%C3%A7%C3%A3o)).

O que precisamos entender, é que cada vez mais as linguagens se adequam ao cenário real, proporcionando assim, que o programador desenvolva algoritmos mais próximo de fluxos comportamentais, logo, tudo ao nosso redor é representado como Objeto.

> Enquanto a programação estruturada é voltada a procedimentos e funções, definidas pelo usuário, a programação orientada a objetos é voltada a conceitos, como o de classes e objetos.

