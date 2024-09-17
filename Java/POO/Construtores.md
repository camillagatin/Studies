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

---
## Sobrecarga de Construtores
```java
public class Produto {

    static final int QUANTIDADE_ESTOQUE_INICIAL = 100;

    String nome;
    int quantidadeEstoque;

    Produto() {
        this.nome = "Sem nome";
        this.quantidadeEstoque = QUANTIDADE_ESTOQUE_INICIAL;
    }

    Produto(String nome) {
        this.nome = nome;
        this.quantidadeEstoque = QUANTIDADE_ESTOQUE_INICIAL;
    }

    Produto(String nome, int estoqueInicial) {
        this.nome = nome;
        this.quantidadeEstoque = estoqueInicial;
    }

}
```

```java
public class Principal {

    public static void main(String[] args) {
        Produto produto1 = new Produto("Picanha 1kg (peça)");
        Produto produto2 = new Produto("Arroz", 35);
        Produto produto3 = new Produto();

        System.out.println(produto1.nome);
        System.out.println(produto1.quantidadeEstoque);

        System.out.println(produto2.nome);
        System.out.println(produto2.quantidadeEstoque);

        System.out.println(produto3.nome);
        System.out.println(produto3.quantidadeEstoque);
    }

}
```

---
## Boas Práticas: Valide os argumentos de construtores
```java
import java.util.Objects;

public class Produto {

    static final int QUANTIDADE_ESTOQUE_INICIAL = 100;

    String nome;
    int quantidadeEstoque;

    Produto() {
        this.nome = "Sem nome";
        this.quantidadeEstoque = QUANTIDADE_ESTOQUE_INICIAL;
    }

    Produto(String nome) {
        Objects.requireNonNull(nome, "Nome é obrigatório");

        this.nome = nome;
        this.quantidadeEstoque = QUANTIDADE_ESTOQUE_INICIAL;
    }

    Produto(String nome, int estoqueInicial) {
        Objects.requireNonNull(nome, "Nome é obrigatório");

        if (estoqueInicial < 0) {
            throw new IllegalArgumentException("Estoque inicial não pode ser negativo");
        }

        this.nome = nome;
        this.quantidadeEstoque = estoqueInicial;
    }

}
```

```java
public class Principal {

    public static void main(String[] args) {
        Produto produto1 = new Produto("Picanha 1kg (peça)");

        // Exceção em tempo de execução
        Produto produto2 = new Produto(null, -35);

        Produto produto3 = new Produto();

        System.out.println(produto1.nome);
        System.out.println(produto1.quantidadeEstoque);

        System.out.println(produto2.nome);
        System.out.println(produto2.quantidadeEstoque);

        System.out.println(produto3.nome);
        System.out.println(produto3.quantidadeEstoque);
    }

}
```

---
## Encadeamento de chamadas de construtores
```java
import java.util.Objects;

public class Produto {

    static final int QUANTIDADE_ESTOQUE_INICIAL = 100;

    String nome;
    int quantidadeEstoque;

    Produto() {
        this("Sem nome");
    }

    Produto(String nome) {
        this(nome, QUANTIDADE_ESTOQUE_INICIAL);
    }

    Produto(String nome, int estoqueInicial) {
        Objects.requireNonNull(nome, "Nome é obrigatório");

        if (estoqueInicial < 0) {
            throw new IllegalArgumentException("Estoque inicial não pode ser negativo");
        }

        this.nome = nome;
        this.quantidadeEstoque = estoqueInicial;
    }

}
```

```java
public class Principal {

    public static void main(String[] args) {
        Produto produto1 = new Produto("Picanha 1kg (peça)");
        Produto produto2 = new Produto("Arroz", 35);
        Produto produto3 = new Produto();

        System.out.println(produto1.nome);
        System.out.println(produto1.quantidadeEstoque);

        System.out.println(produto2.nome);
        System.out.println(produto2.quantidadeEstoque);

        System.out.println(produto3.nome);
        System.out.println(produto3.quantidadeEstoque);
    }

}
```

---
## [[Unified Modeling Language#Construtores|Diagrama de Classes]]
![[construtores.png]]

---
## Modificadir final em variáveis de instância

```java
import java.util.Objects;
import java.util.UUID;

public class Produto {

    static final int QUANTIDADE_ESTOQUE_INICIAL = 100;

    final String codigo;
    String nome;
    int quantidadeEstoque;

    Produto() {
        this("Sem nome");
    }

    Produto(String nome) {
        this(nome, QUANTIDADE_ESTOQUE_INICIAL);
    }

    Produto(String nome, int estoqueInicial) {
        Objects.requireNonNull(nome, "Nome é obrigatório");

        if (estoqueInicial < 0) {
            throw new IllegalArgumentException("Estoque inicial não pode ser negativo");
        }

        this.nome = nome;
        this.quantidadeEstoque = estoqueInicial;
        this.codigo = UUID.randomUUID().toString();
    }

}
```

```java
public class Principal {

    public static void main(String[] args) {
        Produto produto1 = new Produto("Picanha 1kg (peça)");
        Produto produto2 = new Produto("Arroz", 35);
        Produto produto3 = new Produto();

        System.out.println(produto1.codigo);
        System.out.println(produto1.nome);
        System.out.println(produto1.quantidadeEstoque);

        System.out.println(produto2.codigo);
        System.out.println(produto2.nome);
        System.out.println(produto2.quantidadeEstoque);

        System.out.println(produto3.codigo);
        System.out.println(produto3.nome);
        System.out.println(produto3.quantidadeEstoque);
    }

}
```