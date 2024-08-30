**Programação orientada a objetos** (**POO**, ou **OOP** segundo as suas siglas em inglês), é um [paradigma de programação](https://pt.wikipedia.org/wiki/Paradigma_de_programa%C3%A7%C3%A3o) baseado no conceito de "[objetos](https://pt.wikipedia.org/wiki/Objeto_(ci%C3%AAncia_da_computa%C3%A7%C3%A3o))", que podem conter [dados](https://pt.wikipedia.org/wiki/Dados) na forma de [campos](https://pt.wikipedia.org/wiki/Campo_(ci%C3%AAncia_da_computa%C3%A7%C3%A3o)), também conhecidos como _atributos_ e códigos, na forma de [procedimentos](https://pt.wikipedia.org/wiki/Procedimento), também conhecidos como [métodos](https://pt.wikipedia.org/wiki/M%C3%A9todo_(programa%C3%A7%C3%A3o)).

Para uma linguagem ser considerada orientada a objetos, esta deve seguir o que denominamos como _**Os quatro pilares da orientação a objetos**_:

- [[Encapsulamento]]: Nem tudo precisa estar visível, grande parte do nosso algoritmo pode ser distribuído em métodos, com finalidades específicas que complementam uma ação em nossa aplicação.
    
    Exemplo: Ligar um veículo, exige muitas etapas para a engenharia, mas o condutor só visualiza a ignição, dar a partida e a _“magia”_ acontece.

- [[Herança]]: Características e comportamentos comuns, podem ser elevados e compartilhados através de uma hierarquia de objetos.
    
    Exemplo: Um Carro e uma Motocicleta possuem propriedades como placa, chassi, ano de fabricação e métodos como acelerar e frear. Logo, para não ser um processo de codificação redundante, podemos desfrutar da herança criando uma classe _**Veículo**_ para que seja herdada por _**Carro**_ e _**Motocicleta**_.

- [[Abstração]]: É a indisponibilidade, para determinar a lógica de um ou vários comportamentos, em um objeto.
    
    Exemplo: _**Veículo**_ determina duas ações como acelerar e frear, logo, estes comportamentos deverão ser _abstratos,_ pois existem mais de uma maneira de se realizar a mesma operação. ver _[[Polimorfismo]]_.

- [[Polimorfismo]]: São as inúmeras maneiras de se realizar uma mesma ação.
    
    Exemplo: Veículo determina duas ações como acelerar e frear, primeiramente, precisamos identificar se estaremos nos referindo a _**Carro**_ ou _**Motocicleta,**_ para determinar a lógica de aceleração e frenagem dos respectivos veículos.

#### Em prática

Para ilustrar a proposta dos Princípios de POO, no nosso cotidiano, vamos simular algumas funcionalidades dos aplicativos de mensagens instantâneas pela internet.

**MSN Messenger** foi um programa de mensagens instantâneas criado pela Microsoft Corporation. O serviço nasceu a 22 de julho de 1999, anunciando-se como um serviço que, permitia falar com uma pessoa através de conversas instantâneas pela internet. Ao longo dos anos, surgiram novos serviços de mensagens pela internet, como **Facebook Messenger** e o **VKontakte Telegram**.
![[Pasted image 20240627215223.png|400]]
Vamos descrever em UML e depois em código, algumas das principais funcionalidades de qualquer serviço de comunicação instantânea pela internet, inicialmente pelo MSN Messenger e depois inserindo os demais, considerando os princípios de POO ([[Encapsulamento]], [[Herança]], [[Abstração]], [[Polimorfismo]]).
![[Pasted image 20240627215253.png|300]]
```java
public class MSNMessenger {
	public void enviarMensagem() {
		System.out.println("Enviando mensagem");
	}
	public void receberMensagem() {
		System.out.println("Recebendo mensagem");
	}
	public void validarConectadoInternet() {
		System.out.println("Validando se está conectado a internet");
	}
	public void salvarHistoricoMensagem() {
		System.out.println("Salvando o histórico da mensagem");
	}
}
```