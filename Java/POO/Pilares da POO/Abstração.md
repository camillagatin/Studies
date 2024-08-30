>[!warning]
>Para você ser, é preciso você fazer.

Sabemos que qualquer sistema de mensagens instantâneas realiza as mesmas operações de Enviar e Receber Mensagem, dentre outras operações comuns ou exclusivas de cada aplicativo disponível no mercado.

Mas será que as ações realizadas, contém o mesmo comportamento ? Acreditamos que não.

Observem a nova estruturação dos códigos abaixo, com base na implementação apresentada no pilar [[Herança]].

## Serviço Pai
```java
public abstract class ServicoMensagemInstantanea {
	public abstract void enviarMensagem();
	public abstract void receberMensagem();	
}
```

## MSN
```java
public class MSNMessenger extends ServicoMensagemInstantanea{
	@Override
	public void enviarMensagem() {
		System.out.println("Enviando mensagem pelo MSN Messenger");
	}
	@Override
	public void receberMensagem() {
		System.out.println("Recebendo mensagem pelo MSN Messenger");
	}
}
```

## Facebook
```java
public class FacebookMessenger extends ServicoMensagemInstantanea {
	@Override
	public void enviarMensagem() {
		System.out.println("Enviando mensagem pelo Facebook Messenger");
	}
	@Override
	public void receberMensagem() {
		System.out.println("Recebendo mensagem pelo Facebook Messenger");
	}
}
```

## Telegram
```java
public class Telegram extends ServicoMensagemInstantanea {
	@Override
	public void enviarMensagem() {
		System.out.println("Enviando mensagem pelo Telegram");
	}
	@Override
	public void receberMensagem() {
		System.out.println("Recebendo mensagem pelo Telegram");
	}
}

```
