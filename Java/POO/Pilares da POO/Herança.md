> [!warning]
> Nem tudo se copia, às vezes se herda.

Podemos avaliar a importância de compreender os pilares de POO, para ter uma melhor implementação, reaproveitamento e reutilização de código, em qualquer contexto das nossas aplicações.

![[image 1.avif|450]]
## Serviço Pai
```java
//a classe MSNMessenger é ou representa
public class ServicoMensagemInstantanea {
	public void enviarMensagem() {
		//primeiro confirmar se esta conectado a internet
		validarConectadoInternet();
		System.out.println("Enviando mensagem");
		//depois de enviada, salva o histórico da mensagem
		salvarHistoricoMensagem();
	}
	public void receberMensagem() {
		System.out.println("Recebendo mensagem");
	}
	
	//métodos privadas, visíveis somente na classe
	private void validarConectadoInternet() {
		System.out.println("Validando se está conectado a internet");
	}
	private void salvarHistoricoMensagem() {
		System.out.println("Salvando o histórico da mensagem");
	}
}
```

## MSN
```java
public class MSNMessenger extends ServicoMensagemInstantanea{

}
```

## Facebook
```java
public class FacebookMessenger extends ServicoMensagemInstantanea {

}
```

## Telegram
```java
public class Telegram extends ServicoMensagemInstantanea {

}
```

## Computador Pedrinho
```java
public class ComputadorPedrinho {
	public static void main(String[] args) {
		
		MSNMessenger msn = new MSNMessenger();
		msn.enviarMensagem();
		msn.receberMensagem();
		
		FacebookMessenger fbm = new FacebookMessenger();
		fbm.enviarMensagem();
		fbm.receberMensagem();
		
		Telegram tlg = new Telegram();
		tlg.enviarMensagem();
		tlg.receberMensagem();
	}
}
```

> [!info]
> Será que todos os sistemas de mensagens, realizam as suas operações de uma mesma maneira? Este é um trabalho para os pilares [[Abstração]] e [[Polimorfismo]].

---
### [[Unified Modeling Language#Herança|Diagrama de Classes]]
![[heranca.png|400]]
~~(ver projeto banco em algaworks exemplos)~~

---
## Superclasse em Java: A Base da Herança

**O que é uma superclasse em Java?**
Em Java, uma superclasse, também conhecida como classe pai ou classe base, é uma classe que serve como modelo para outras classes. Ela define atributos e métodos que podem ser herdados por suas subclasses. Essa relação entre classes é fundamental para o conceito de herança na programação orientada a objetos.

**Por que usar superclasses?**
* **Reutilização de código:** Ao criar uma superclasse, você define um conjunto de características comuns a várias classes. As subclasses podem herdar essas características, evitando a duplicação de código.
* **Hierarquia de classes:** As superclasses formam uma hierarquia, onde cada classe pode ter uma ou mais subclasses. Essa hierarquia reflete relações "é um" (por exemplo, um cachorro é um animal).
* **Polimorfismo:** A herança permite que objetos de diferentes classes sejam tratados como se fossem de uma classe pai comum, o que é a base do polimorfismo.

**Exemplo:**
```java
class Animal {
    String nome;

    void emitirSom() {
        System.out.println("Fazendo algum som");
    }
}

class Cachorro extends Animal {
    void latir() {
        System.out.println("Au au");
    }
}
```

Neste exemplo:
* `Animal` é a superclasse. Ela define um atributo `nome` e um método `emitirSom()`.
* `Cachorro` é a subclasse. Ela herda todos os atributos e métodos de `Animal` e adiciona um novo método específico: `latir()`.

**Como funciona a herança?**
* **Herdando atributos e métodos:** Uma subclasse herda todos os atributos e métodos não privados da sua superclasse.
* **Sobrescrita de métodos:** Uma subclasse pode sobrescrever um método da superclasse para fornecer uma implementação específica.
* **Construtores:** Os construtores não são herdados. Ao criar um objeto de uma subclasse, o construtor da superclasse é chamado primeiro para inicializar os atributos herdados.

**Palavra-chave `super`:**
A palavra-chave `super` é usada para:
* **Chamar construtores da superclasse:** `super(argumentos)`
* **Acessar membros da superclasse:** `super.metodo()` ou `super.atributo`

**Exemplo com `super`:**
```java
class Cachorro extends Animal {
    String raca;

    Cachorro(String nome, String raca) {
        super(nome); // Chama o construtor da superclasse
        this.raca = raca;
    }
}
```

**Vantagens da herança:**
* **Organização do código:** Cria uma estrutura hierárquica clara para as classes.
* **Reutilização de código:** Evita a duplicação de código.
* **Extensibilidade:** Permite criar novas classes especializadas a partir de classes existentes.
* **Polimorfismo:** Facilita o desenvolvimento de código mais flexível e adaptável.
## Mais Exemplos Usando a Palavra-chave `super` em Java

### 1. Sobrescrita de Métodos e Acesso ao Método Original:
```java
class Animal {
    void emitirSom() {
        System.out.println("Fazendo algum som");
    }
}
```

```java
class Cachorro extends Animal {
    @Override
    void emitirSom() {
        super.emitirSom(); // Chama o método da superclasse
        System.out.println("Au au");
    }
}
```
Neste exemplo, o método `emitirSom()` da classe `Cachorro` sobrescreve o método da classe `Animal`. Ao usar `super.emitirSom()`, chamamos a implementação original da superclasse antes de adicionar o comportamento específico do cachorro.

### 2. Acesso a Atributos da Superclasse:
```java
class Pessoa {
    String nome;

    Pessoa(String nome) {
        this.nome = nome;
    }
}
```

```java
class Estudante extends Pessoa {
    int matricula;

    Estudante(String nome, int matricula) {
        super(nome);
        this.matricula = matricula;
    }

    void mostrarInformacoes() {
        System.out.println("Nome: " + super.nome); // Acessa o atributo nome da superclasse
        System.out.println("Matrícula: " + matricula);
    }
}
```
Aqui, o método `mostrarInformacoes()` da classe `Estudante` acessa o atributo `nome` da superclasse `Pessoa` usando `super.nome`.

### 3. Construtores em Cadeia:
```java
class Forma {
    int lados;

    Forma(int lados) {
        this.lados = lados;
    }
}
```

```java
class Quadrado extends Forma {
    Quadrado(int lado) {
        super(4); // Chama o construtor da superclasse com 4 lados
    }
}
```
Neste caso, o construtor de `Quadrado` chama o construtor de `Forma` para inicializar o número de lados.

### 4. Métodos Estáticos:
**Importante:** Métodos estáticos pertencem à classe, não à instância, portanto, não podem ser acessados diretamente usando `super`. Para acessar um método estático de uma superclasse, você o chama diretamente pelo nome da classe:
```java
class Util {
    static void imprimirMensagem(String msg) {
        System.out.println(msg);
    }
}
```

```java
class MinhaClasse extends Util {
    void meuMetodo() {
        Util.imprimirMensagem("Mensagem da classe Util");
    }
}
```

### Quando usar `super`?
* **Chamar construtores da superclasse:** Para garantir a inicialização correta dos atributos herdados.
* **Sobrescrever métodos:** Para fornecer uma implementação específica de um método herdado.
* **Acessar membros da superclasse:** Quando você precisa usar um membro da superclasse que foi sobrescrito ou quando você deseja acessar um atributo privado da superclasse (embora isso não seja recomendado, pois viola o encapsulamento).
---
## Chamando Método da Superclasse com Super
Conta.java
```java
public void imprimirDemonstrativo() {
        System.out.println();
        System.out.printf("Agência: %d%n", getAgencia());
        System.out.printf("Conta: %d%n", getNumero());
        System.out.printf("Titular: %s%n", getTitular().getNome());
        System.out.printf("Saldo: %.2f%n", getSaldo());
    }
```

ContaEspecial.java
```java
@Override
    public void imprimirDemonstrativo() {
        super.imprimirDemonstrativo(); //chamando da classe Conta
        System.out.printf("Saldo disponível: %.2f%n", getSaldoDisponivel());
    }
```
---
## Invocando construtores da superclasse
```java
public ContaInvestimento() {
		// this();
        super(0); // classe Conta
}
```

```java
public ContaEspecial() {
		// this();
        super(); // classe Conta
}
```
---
## Criando construtores com parâmetros na superclasse e subclasses
```java
// chamando o construtor da classe mãe
public ContaInvestimento(Titular titular, int agencia, int numero) {
	super(titular, agencia, numero);
}
```

```java
// chamando o construtor da classe mãe
public ContaEspecial(Titular titular, int agencia, int numero, double tarifaMensal) {
        super(titular, agencia, numero);
        this.tarifaMensal = tarifaMensal;
}
```

```java
// construtor
public Conta(Titular titular, int agencia, int numero) {
        this.titular = titular;
        this.agencia = agencia;
        this.numero = numero;
}
```

```java
public class Principal1 {
public static void main(String[] args) {

        Titular titular = new Titular("João da Silva", "12312312300");
        Conta conta1 = new Conta(titular, 1234, 999999);
	}
}
```
---
## Boas práticas: sempre sobrescreva o método Object.toString
Titular.java
```java
@Override
public String toString() {
	return "Titular {" +
	        "nome = '" + nome + '\'' +
	        ", cpf = '" + cpf + '\'' +
	        '}';
}
```

ContaInvestimento.java
```java
@Override
public String toString() {
	return "ContaInvestimento {" +
            "titular = " + getTitular() +
            ", agencia = " + getAgencia() +
            ", numero = " + getNumero() +
            ", valorTotalRendimentos = " + valorTotalRendimentos +
            '}';
}

```

ContaEspecial.java
```java
@Override
public String toString() {
    return "ContaEspecial {" +
            "titular = " + getTitular() +
            ", agencia = " + getAgencia() +
            ", numero = " + getNumero() +
            ", valorTotalRendimentos = " + getValorTotalRendimentos() +
            ", tarifaMensal = " + tarifaMensal +
            ", limiteChequeEspecial = " + limiteChequeEspecial +
            '}';
    }
```

Conta.java
```java
@Override
public String toString() {
    return "Conta {" +
	    "titular = " + titular +
        ", agencia = " + agencia +
        ", numero = " + numero +
       '}';
}
```

Passaporte.java
```java
public record Passaporte(String numero, String pais) {
}
```

Principal.java
```java
public class Principal {

    public static void main(String[] args) {
        Passaporte passaporte = new Passaporte("123456", "Brasil");

        System.out.println(passaporte);
        // record implementa ToString automaticamente
    }

}
```
---
###### Modificador final em classes e métodos
protegendo dados muito sensíveis, para não ser possível sobrescrever
~~(ver projeto banco em algaworks exemplos)~~

---
## Sobrescrevendo o método Object.equals

```java
public class Conta {
    @Override
    public boolean equals(Object obj) {
        /*
        if (this == obj) return true;
        if (obj == null) return false;
        if (this.getClass() != obj.getClass()) return false;

        Conta conta = (Conta) obj;
        if (this.agencia != conta.agencia) return false;
        if (this.numero != conta.numero) return false;
        return true;

		mesma coisa que o debaixo
		*/

		if (this == obj) return true;
		if (obj == null || getClass() != obj.getClass()) return false;
		Conta conta = (Conta) obj;
		return agencia == conta.agencia && numero == conta.numero;
    }

	@Override
	public int hashCode() {
		return Objects.hash(agencia, numero);
	}
}
```

```java
public class Principal {

    public static void main(String[] args) {
        Titular titular = new Titular("João da Silva", "12312312300");
        Conta conta1 = new Conta(titular, 1234, 999999);
        Conta conta2 = new Conta(titular, 1234, 999999);
        ContaEspecial contaEspecial = new ContaEspecial(titular, 1234, 999999, 90);

        System.out.println(conta1.equals(conta2));
        System.out.println(conta1.equals(contaEspecial));
    }

}
```


## Boas Práticas: obedeça o contrato ao sobrescrever o método equals
