Recebe entrada de dados

```java
import java.util.Scanner;

public class EntradaDeDados {
	public static void main(String[] args) {
		Scanner entrada = new Scanner(System.in);

	    sout.println("Digite o seu nome:");
	    String nome = entrada.nextLine();
	    sout.printf("Oi, %s%n", nome);
  }

}
```

```java
import java.util.Scanner;

public class IndiceMassaCorporal {

	public static void main(String[] args) {
	    Scanner entrada = new Scanner(System.in);

	    System.out.print("Peso: ");
	    int peso = entrada.nextInt();

	    System.out.print("Altura: ");
	    double altura = entrada.nextDouble();

	    // workaround para consumir quebra de linha antes do próximo nextLine
	    entrada.nextLine();

	    System.out.print("Nome: ");
	    String nome = entrada.nextLine();

	    double imc = peso / (altura * altura);

	    System.out.printf("IMC de %s: %.2f%n", nome, imc);
	}

}
```