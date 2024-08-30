É um bloco de código especial dentro de uma classe, designado para inicializar novos objetos. Caracteriza-se por ter o mesmo nome da classe e por não especificar um tipo de retorno, nem mesmo void.

Abaixo, iremos ilustrar uma classe Pessoa, onde a mesma terá os atributos: Nome, CPF e Endereço.

```java
public class Pessoa {
	private String nome;
	private String cpf;
	private String endereco;
	
	public String getNome() {
		return nome;
	}
	public String getCpf() {
		return cpf;
	}
	public String getEndereco() {
		return endereco;
	}
	public void setEndereco(String endereco) {
		this.endereco = endereco;
	}
	//...
	//setters de nome e cpf ?
}
```

Criaremos uma Pessoa, mas como não temos o setter para nome e cpf, este objeto não tem como receber estes valores:

```java
public class SistemaCadastro {
	public static void main(String[] args) {
		//criamos uma pessoa no sistema
		Pessoa marcos = new Pessoa();
		
		//definimos o endereço de marcos
		marcos.setEndereco("RUA DAS MARIAS");
		
		//e como definir o nome e cpf do marcos ?
		
		//imprimindo o marcos sem o nome e cpf
		
		System.out.println(marcos.getNome() + "-" + marcos.getCpf());
	}
}
```

Entrando em cena o construtor, para criar nossos objetos, já com valores requeridos na momento da criação\\instanciação (`new`):

```java
public class Pessoa {
	private String nome;
	private String cpf;
	private String endereco;
	
	// método construtor
	// o nome deverá ser igual ao nome da classe
	public Pessoa (String cpf, String nome) {
		this.cpf = cpf;
		this.nome = nome;
	}
	
	//...
	//getters
	//setters
}
```

Alterando o nosso sistema, para agora criar o objeto com informações já requeridas, conforme definição da ordem dos parâmetros do construtor:

```java
public class SistemaCadastro {
	public static void main(String[] args) {
		//criamos uma pessoa no sistema
		Pessoa marcos = new Pessoa("06724506716","MARCOS SILVA");
		
		//continua ...
		
	}
}
```
