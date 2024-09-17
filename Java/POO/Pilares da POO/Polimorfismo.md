>[!warning]
>Um mesmo comportamento, de várias maneiras.

Podemos observar no contexto de [[Abstração]] e [[Herança]], que conseguimos criar uma singularidade estrutural de nossos elementos. Isso quer dizer que, qualquer classe que deseja representar um serviço de mensagens, basta estender a classe `ServicoMensagemInstantanea` e implementar, os respectivos métodos _abstratos_. O que vale reforçar aqui é, cada classe terá a mesma ação, executando procedimentos de maneira especializada.
![[image 2.avif | 450]]
Este é o resultado do que denominamos como, Polimorfismo. Veja o exemplo abaixo:
```java
public class ComputadorPedrinho {
	public static void main(String[] args) {
		
		ServicoMensagemInstantanea smi = null;
		String appEscolhido="???"; 
		
		if(appEscolhido.equals("msn"))
			smi = new MSNMessenger();
		else if(appEscolhido.equals("fbm"))
			smi = new FacebookMessenger();
		else if(appEscolhido.equals("tlg"))
			smi = new Telegram();
		
		smi.enviarMensagem();
		smi.receberMensagem();
	}
}
```

### Modificador protected
O nosso requisito, solicita que além de Enviar e Receber Mensagens, precisamos validar se o aplicativo está conectado a internet (`validarConectadoInternet`) e salvar o histórico de cada mensagem (`salvarHistoricoMensagem`).

Sabemos que cada aplicativo, costuma salvar as mensagens em seus respectivos servidores cloud, mas e quanto validar se está conectado a internet? Não poderia ser um mecanismo comum a todos ? Logo, qualquer classe filha, de **ServicoMensagemInstantanea** poderia desfrutar através de herança, esta funcionalidade.

> [!tip]
> Mas fica a reflexão do que já aprendemos sobre visibilidade de recursos: Com o modificador `private`somente a classe conhece a implementação, quanto que o modificador `public`todos passarão a conhecer. Mas gostaríamos que, somente as classes filhas soubessem. Bem, é ai que entra o modificador `protected`.

``ServicoMensagemInstantanea.java``, ``MSNMessenger.java``, ``FacebookMessenger.java`` e ``Telegram.java`` vão para o pacote ``apps`` e o ``ComputadorPedrinho.java`` em outro pacote.

```java
public abstract class ServicoMensagemInstantanea {
	
	public abstract void enviarMensagem();
	public abstract void receberMensagem();
	
	//mais um método que todos os filhos deverão implementar
	public abstract void salvarHistoricoMensagem();
	
	//somente os filhos conhecem este método
	protected void validarConectadoInternet() {
		System.out.println("Validando se está conectado a internet");
	}	
}
```
---
### Upcasting
É fazer um objeto se passar por um objeto que seja um supertipo dele. Ele sempre funcionará já que todo objeto é completamente compatível com um tipo do qual ele foi derivado. Como sempre pode ser realizado, é possível fazer implicitamente, ou seja, o compilador faz por você quando for necessário.

É muito comum ele ocorrer como parâmetro de um método que usará __polimorfismo__. O chamador manda como argumento um objeto que é o subtipo, o método recebe um parâmetro como se fosse o supertipo, mas funciona como um subtipo. Mas note que o polimorfismo é um mecanismo auxiliar e não ligado diretamente ao _casting_. É considerado uma coerção em tempo de compilação.

Algumas pessoas gostam de chamar de promoção de tipo.

### Downcasting
É quando o objeto se passa como se fosse um subtipo dele. Não há garantias que funcione (pode lançar uma `ClassCastException`, o que obviamente é um erro de programação) e pode haver necessidade de conversões. O compilador só aceita se ele puder provar que o objeto se encaixará perfeitamente e seja de fato aquele objeto. Por isso deve ser explicitado pelo programador quando deseja essa ação. A coerção ocorre em tempo de execução.

Algumas pessoas gostam de chamar de demoção de tipo (apesar de ser um neologismo).

Existe um padrão normalmente usado para evitar a exceção quando não se tem certeza que dará certo:

```java
obj instanceof Tipo ? (Tipo)obj : null
```

Nesse exemplo se o objeto não for do tipo adequado, ele criará um nulo e nem tentará o _cast_. Obviamente que qualquer tentativa de acesso ao objeto gerado será problemático, então é preciso verificar se o objeto é nulo antes de tentar acessá-lo, caso contrário, só trocará de erro.

Exemplos:

```java
class Animal { 
    public void makesNoise() {
        System.out.println("silence");
    }
}
class Dog extends Animal { 
    public void makesNoise() {
        System.out.println("au au");
    }
}
class Cat extends Animal { 
    public void makesNoise() {
        System.out.println("miau");
    }
}
class Ideone {
    public static void main(String[] args) {
        Dog dog = new Dog();      
        Animal animal = new Animal();
        Animal animal2 = new Dog();
        Animal animal3 = new Cat();
        dog.makesNoise();
        animal.makesNoise);
        animal2.makesNoise(); //concretamente é um cachorro
        animal3.makesNoise(); //concretamente é um gato
        System.out.println("-- Castings agora --");
        ((Animal)dog).makesNoise(); //upcasting
        ((Dog)animal2).makesNoise(); //downcasting, funciona
        ((Dog)animal3).makesNoise(); //downcasting, dá erro porque um gato não é um cachorro
        ((Dog)animal).makesNoise(); //downcasting, dá erro aqui
    }
}
```
Quando não há garantias que o objeto terá tudo o que se espera daquele tipo, o _cast_ falhará. É o caso óbvio de um gato tentando se passar por um cachorro. Quando o animal genérico tenta se passar por um cachorro também não dá. Embora coincidentemente nesse exemplo até poderia funcionar, o compilador não pode provar isto. O programador que está vendo todo o código sabe, mas nem sempre ele poderá ver todas as classes. E mais, é possível uma manutenção modificar a classe e o que funcionava deixar de funcionar. Então tem que ir pelo caminho seguro.

De uma maneira geral isto funciona igual em todas as linguagens que possuem herança.

---
