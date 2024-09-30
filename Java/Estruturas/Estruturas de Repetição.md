Laços de repetição, também conhecidos como laços de iteração ou simplesmente loops, são comandos que permitem iteração de código, ou seja, que comandos presentes no bloco sejam repetidos diversas vezes.

---
### For
O comando ``for`` permite que uma variável contadora, seja testada e incrementada a cada iteração, sendo essas informações definidas na chamada do comando. O comando for recebe como entrada uma variável contadora, a condição para continuar a execução e o valor de incrementação.
```java
//estrutura do controle de fluxo for

for (bloco de inicialização; expressão booleana de validação; bloco de atualização)
{
//comando que será executado até que a expressão de validação torne-se falsa 
}
```

```java
    System.out.print("Peso máximo da aeronave: ");
    int pesoMaximo = entrada.nextInt();

    System.out.print("Quantidade de passageiros: ");
    int totalPassageiros = entrada.nextInt();

    int pesoTotalPassageiros = 0;

    for (int passageiroAtual = 1; passageiroAtual <= totalPassageiros; passageiroAtual++) {
      System.out.printf("Peso do passageiro #%d: ", passageiroAtual);
      int pesoPassageiro = entrada.nextInt();

      pesoTotalPassageiros += pesoPassageiro;
    }

    System.out.printf("Peso máximo da aeronave: %d kg%n", pesoMaximo);
    System.out.printf("Peso total dos passageiros: %d kg%n", pesoTotalPassageiros);
    System.out.printf("Situação da aeronave: %s%n", 
        pesoTotalPassageiros > pesoMaximo ? "peso excedido" : "liberada");
  }

}
```

---
### While
O laço `while` determina que, enquanto uma condição for válida, o bloco de código será executado. O laço `while` testa a condição antes de executar o código, logo, caso a condição seja inválida no primeiro teste o bloco nem será executado.
```java
//estrutura do controle de fluxo while

while (expressão booleana de validação)
{
     // comando que será executado até que a expressão de validação torne-se falsa 
}
```

```java
    System.out.print("Peso máximo da aeronave: ");
    int pesoMaximo = entrada.nextInt();

    int pesoTotalPassageiros = 0;
    boolean incluirNovoPassageiro = true;

    while (pesoTotalPassageiros <= pesoMaximo && incluirNovoPassageiro) {
      System.out.print("Peso do passageiro: ");
      int pesoPassageiro = entrada.nextInt();

      pesoTotalPassageiros += pesoPassageiro;

      System.out.print("Incluir novo passageiro? ");
      incluirNovoPassageiro = entrada.nextBoolean();
    }

    System.out.printf("Peso máximo da aeronave: %d kg%n", pesoMaximo);
    System.out.printf("Peso total dos passageiros: %d kg%n", pesoTotalPassageiros);
    System.out.printf("Situação da aeronave: %s%n", 
        pesoTotalPassageiros > pesoMaximo ? "peso excedido" : "liberada");
  }

}
```

---
### Do While
O laço ``do / while``, assim como o laço while, considera que, enquanto uma determinada condição for válida, o bloco de código será executado. Entretanto, ``do / while`` testa a condição após executar o código, sendo assim, mesmo que a condição seja considerada inválida, no primeiro teste o bloco será executado pelo menos uma vez.
```java
//estrutura do controle de fluxo do while

do {
    // comando que será executado até que a expressão de validação torne-se falsa
} while (expressão booleana de validação);
```

```java
    int quantidadeNumeros = 0;

    do {
      System.out.print("Quantidade de números: ");
      quantidadeNumeros = entrada.nextInt();

      if (quantidadeNumeros < 6 || quantidadeNumeros > 15) {
        System.out.println("Quantidade de números deve ser entre 6 e 15.");
      }
    } while (quantidadeNumeros < 6 || quantidadeNumeros > 15);

    int numeroAtual = 1;
    String numerosEscolhidos = "";

    do {
      System.out.printf("Número %d/%d: ", numeroAtual, quantidadeNumeros);
      int numeroEscolhido = entrada.nextInt();

      if (numeroEscolhido < 1 || numeroEscolhido > 60) {
        System.out.println("Número deve ser de 1 a 60");
      } else {
        numerosEscolhidos += numeroEscolhido + " ";
        numeroAtual++;
      }
    } while (numeroAtual <= quantidadeNumeros);

    System.out.printf("Números escolhidos: %s%n", numerosEscolhidos);
  }

}
```

---
#### Break e Continue
O comando `break` interrompe o laço, já o `continue` interrompe somente a iteração atual.

```java
	System.out.print("Peso máximo da aeronave: ");
    int pesoMaximo = entrada.nextInt();

    int pesoTotalPassageiros = 0;

    while (true) {
      System.out.print("Peso do passageiro: ");
      int pesoPassageiro = entrada.nextInt();

      if (pesoTotalPassageiros + pesoPassageiro > pesoMaximo) {
        System.out.println("Não pôde incluir passageiro. Peso excederia o máximo.");
        continue;
      }

      pesoTotalPassageiros += pesoPassageiro;

      System.out.print("Incluir novo passageiro? ");
      if (!entrada.nextBoolean()) {
        break;
      }
    }

    System.out.printf("Peso máximo da aeronave: %d kg%n", pesoMaximo);
    System.out.printf("Peso total dos passageiros: %d kg%n", pesoTotalPassageiros);
    System.out.printf("Situação da aeronave: %s%n", 
        pesoTotalPassageiros > pesoMaximo ? "peso excedido" : "liberada");
  }

}
```