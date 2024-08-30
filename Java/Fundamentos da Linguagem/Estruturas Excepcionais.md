#### Exceções
Ao executar o código Java, diferentes erros podem acontecer: erros de codificação feitos pelo programador, erros devido a entrada errada ou outros imprevistos.

Quando ocorre um erro, o Java normalmente para e gera uma mensagem de erro. O termo técnico para isso é: Java lançará uma exceção (jogará um erro).

Uma responsabilidade do desenvolvedor é prever situações e realizar o que denominamos de **[[#Tratamento de Exceções]]**.

##### Exemplos de exceções:

| Entrada               | Valor            | Exceção                          | Causa                                                                                    |
| --------------------- | ---------------- | -------------------------------- | ---------------------------------------------------------------------------------------- |
| Digite seu nome:      | **Camilla**      |                                  |                                                                                          |
| Digite seu sobrenome: | **Gatin**        |                                  |                                                                                          |
| Digite sua idade:     | **vinte e dois** | java.util.InputMismatchException | O programa esperava o valor do tipo numérico inteiro.                                    |
| Digite sua altura:    | **1,65**         | java.util.InputMismatchException | O programa esperava o valor do tipo numérico decimal no formato americano, exemplo: 1.65 |


> [!quote] Lei de Murphy
> A melhor forma de prever, que pode ocorrer uma exceção, é pensar que ela pode ocorrer.

##### Exceções comuns:

| Nome                           | Causa                                                                 |
| ------------------------------ | --------------------------------------------------------------------- |
| java.lang.NullPointerException | Quando tentamos obter alguma informação de uma variável nula.         |
| java.lang.ArithmeticException  | Quando tentamos dividir um valor por zero.                            |
| java.sql.SQLException          | Quando existe algum erro, relacionado a interação com banco de dados. |
| java.io.FileNotFoundException  | Quando tentamos ler ou escrever, em um arquivo que não existe.        |

#### Tratamento de Exceções
A instrução `try`, permite que você defina um bloco de código, para ser testado quanto a erros enquanto está sendo executado.

A instrução `catch`, permite definir um bloco de código a ser executado, caso ocorra um erro no bloco try.

A instrução `finally`, permite definir um bloco de código a ser executado, independente de ocorrer um erro ou não. As palavras-chave `try` e `catch` vem em pares:


```java
// estrutura de um bloco com try e catch

try {
  //  Block of code to try
}
catch(Exception e) { // qual exceção
  //  Block of code to handle errors
}
```

> [!warning]
> O bloco `try` / `catch` pode conter um conjunto de **catchs,** correspondentes a cada exceção **prevista** em uma funcionalidade do programa.

#### Hierarquia das exceções
A linguagem Java, dispõe de uma variedade de classes, que representam exceções e estas classes, são organizadas em uma hierarquia denominadas **Checked and Unchecked Exceptions**.
![[Pasted image 20240623165711.png]]

#### Exceções customizadas
Nós podemos criar nossas próprias exceções, baseadas em regras de negócio e assim melhor direcionar quem for utilizar os recursos desenvolvidos no projeto, exemplo:

~~ver exemplo no vscode (bootcamp java santander)~~
 Imagina que como regra de negócio, para formatar um cep, necessita sempre de ter 8 dígitos, caso contrário, lançará uma exceção que denominamos de **CepInvalidoException**.
- Primeiro criamos nossa exceção: `` public class CepInvalidoException extends Exception {}``
- Em seguida, criamos nosso método de formatação de cep: 
```java
static String formatarCep(String cep) throws CepInvalidoException{
        if(cep.length() != 8)
          throw new CepInvalidoException();
        
          //simulando um cep formatado
          return "23.765-064";
    }
```
