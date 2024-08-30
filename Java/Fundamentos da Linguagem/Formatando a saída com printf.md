`println` → 'ln = line' já por si só imprime em linhas separadas
`printf` → recebe regrinhas para formatação

```java
public class Formatando {
	public static void main(String[] args) {
		String nome1 = "Thiago";
		System.out.printf("Olá, %s%n", nome1);

		int quantidade = 48;
		sout.printf("Quantidade: %d itens%n", quantidade);

		double peso = 938.22;
		sout.printf("Peso: %10.2f%n", peso);
		// o número antes do ponto é a quatidade de caracteres(espaços em branco)
		// depois do ponto a quantidade de decimais
	}
}
```

==%s==   → representa a variavel de String
==%n==   → quebra a linha
==%d==   → representa a variavel inteiros
==%f==    → representa as variaveis float e double
==%b==   → representa a variavel boolean
==%c==   → representa a variavel char

| Pattern  | Data | `Printf` Output       |
| -------- | ---- | --------------------- |
| '%s'     | Java | 'Java'                |
| '%15s'   | Java | '               Java' |
| '%-15s ' | Java | 'Java               ' |
| '%-15S ' | Java | 'JAVA               ' |
