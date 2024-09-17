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
