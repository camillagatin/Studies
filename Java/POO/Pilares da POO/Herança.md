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
> Será que todos os sistemas de mensagens, realizam as suas operações de uma mesma maneira? e agora ? este é um trabalho para os pilares [[Abstração]] e [[Polimorfismo]].

