### Condicionais Simples
Quando ocorre uma validação de execução de fluxo, somente quando a condição for positiva, consideramos como uma estrutura Simples, exemplo:
![[Pasted image 20240620174706.png|300]]

---
### Condicionais Composta
Algumas vezes, o nosso programa deverá seguir mais de uma jornada de execução, condionado a uma regra de negócio, este cenário é demoninado Estrutura Condicional Composta. Vejamos o exemplo abaixo:
![[Pasted image 20240620181440.png|300]]

---
### Condicionais encadeadas
Em um controle de fluxo condicional, nem sempre nos limitamos ao se (if) e senão (else), poderemos ter uma terceira, quarta e ou inúmeras condições.
![[Pasted image 20240620184543.png|300]]

---
### Condição ternária
Como vimos em operadores, podemos abreviar nosso algoritmo condicional, refatorando com o conceito de operador ternário. Vamos refatorar os exemplos acima, para ilustrar o poder deste recurso:
```java
// Cenário 1
public class ResultadoEscolar {
	public static void main(String[] args) {
		int nota = 7;
		String resultado = nota >=7 ? "Aprovado" : "Reprovado";
		System.out.println(resultado);
	}
}

// Cenário 2
public class ResultadoEscolar {
	public static void main(String[] args) {
		int nota = 6;
		String resultado = nota >=7 ? "Aprovado" : nota >=5 && nota <7 ? "Recuperação" : "Reprovado";
		System.out.println(resultado);
	}
}

```

---
### Switch Case
A estrutura switch, compara o valor de cada caso, com o da variável sequencialmente e sempre que encontra um valor correspondente, executa o código associado ao caso. Para evitar que as comparações continuem a ser executadas, após um caso correspondente ter sido encontrado, acrescentamos o comando break no final de cada bloco de códigos. O comando break, quando executado, encerra a execução da estrutura onde ele se encontra.
```java
public class SistemaMedida {
	public static void main(String[] args) {
		String sigla = "M";

		switch (sigla) {
		case "P":{
			System.out.println("PEQUENO");
			break;
		}
		case "M":{
			System.out.println("MÉDIO");
			break;
		}
		case "G":{
			System.out.println("GRANDE");
			break;
		}
		default:
			System.out.println("INDEFINIDO");
		}
			
		
	}
}

```

#### Switch Expressions
A partir do Java 14 surgiu outra forma para atribuir os valores sem utilizar o `break `e deixar o código mais legível que é usando a setinha `->`

```java
import java.util.Scanner;

public class HorarioFuncionamento {
	public static void main(String[] args) {
	    Scanner entrada = new Scanner(System.in);

	    System.out.print("Dia da semana (ex: seg, ter, qua, etc): ");
	    String diaSemana = entrada.nextLine();
	    System.out.print("Mês: ");
	    int mes = entrada.nextInt();
	    
	    System.out.printf("Horário de funcionamento: %s%n", switch (diaSemana) {
		    case "seg" -> {
			    if (mes == 12) {
		         yield "08:00 às 16:00";
		         } yield "Fechado";
		        }
		    case "ter", "qua", "qui", "sex" -> "08:00 às 18:00";
		    case "sab", "dom" -> "08:00 às 12:00";
		    default -> "Dia inválido";
		});

    /*
    String horarioFuncionamento = switch (diaSemana) {
      case "seg" -> "Fechado";
      case "ter", "qua", "qui", "sex" -> "08:00 às 18:00";
      case "sab", "dom" -> "08:00 às 12:00";
      default -> "Dia inválido";
    };
    */

    /*
    String horarioFuncionamento;

    switch (diaSemana) {
      case "seg" -> horarioFuncionamento = "Fechado";
      case "ter", "qua", "qui", "sex" -> horarioFuncionamento = "08:00 às 18:00";
      case "sab", "dom" -> {
        horarioFuncionamento = "08:00 às 12:00";
      }
      default -> horarioFuncionamento = "Dia inválido";
    }
    */

    // System.out.printf("Horário de funcionamento: %s%n", horarioFuncionamento);
  }

}
```